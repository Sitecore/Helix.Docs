..  OUTLINE
    * Why alternate structures?
        * Build Times
        * Module Creation Overhead
        * Deployment Requirements
        * Reuse Requirements
    * Are you addressing the right problem?
        * Are your features too granular?
            * Atomic design
        * Projects you don't need
        * Can you improve your tooling?
            * Module template tooling
            * Old Habitat gulpfile was slow
            * Investigate new SDK project format
            * Visual Studio 2019 improvements
    * What is the role of a Visual Studio project?
        * Unit of release vs unit of maintenance
        * Physical vs logical boundaries
    * Consolidated Solution Architecture Options
        * Services/Targets and Consolidated Projects
        * Project per Layer
        * Feature Groups
        * Project per Target
    * Does Sitecore Helix really allow this?
        * Not a rulebook
    * Helix Basic Company Example

Alterate Visual Studio Solution Structures
------------------------------------------

One of the most common points of feedback on Sitecore Helix regards its
use of Visual Studio Projects to organize and set boundaries between
modules. Concerns about this practice include:

* Build times for large solutions
* The overhead of creating multiple projects and properly organizing
  them when adding a module
* The deployment complexity created by large numbers of assemblies and
  multiple ASP.NET projects
* Disagreement regarding the appropriate use of Visual Studo Projects /
  .NET Assemblies

The result is that some Sitecore solution architects are inclined to structure
their Visual Studio solutions with fewer projects, while still following Sitecore
Helix conventions in .NET namespaces and in the dependencies between classes.
Effectively, thus modules have "logical" boundaries rather than "physical"
boundaries.

You should apply Sitecore Helix in a way that you see as best for your customer,
solution, and requirements -- `it is not a rulebook </introduction/about-this-documentation.html#sitecore-helix-is-not-a-rulebook>`__.
However the reasons for departing from the conventions should be understood, as well
as the potential for accumulating technical debt when doing so. The goals of
`maintainability and long-term value </introduction/why-sitecore-helix>`__ should
drive these decisions.


Are you solving the right problem?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If slow builds or the overhead of creating new Visual Studio projects are
the main concern with the conventional Sitecore Helix project architecture,
you might first consider whether misapplication of the Sitecore
Helix Practices is actually the root of the issue, or whether better tooling
might resolve the concern.

Are your modules too granular?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
In Sitecore Helix, `the scope of a module should be a business domain </principles/architecture-principles/modules>`__.
A common mistake when applying the practices is to define modules based on
Atomic Design, with modules defined for individual controls rather than for
related business features and responsibilities. This can quickly grow the number
of Visual Studio projects in a solution and make them unmanagable. Ensure your modules
are appropriately scoped. Controls and functionality that change together
should be packaged together.

Does your solution contain projects you do not need?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Does your solution contain empty unit test projects for one or more modules? This might
be the case for simple modules which only contain configuration and/or View renderings.
These add no value and unecessarily slow down your builds.

The same applies for TDS projects with no items. If these exist only to build/deploy a module,
consider a single build-only TDS project with `multiple Source Web Projects <http://hedgehogdevelopment.github.io/tds/chapter4.html#general>`__.

.. admonition:: Sitecore Helix Examples

    The TDS version of Helix Basic Company uses a single TDS project for
    file copy / packaging, and additional TDS projects as-needed within each module.
    It also only has test projects for modules with testable logic.

    .. figure:: _static/basic-company-projects.png
        :scale: 75%

Are there inefficiencies in your build scripts?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Previous versions of Sitecore Habitat included gulp scripts which built each
Visual Studio project individually, rather than the entire solution at once.
This could lead to much slower builds as project dependencies could be built
more than once. Ensure your build scripts target the VS Solution or a single
"root-level" project.

.. admonition:: Sitecore Habitat

    Newer versions of `Sitecore Habitat <https://github.com/Sitecore/Habitat>`__
    have an updated ``gulpfile`` which targets the entirety of the Visual Studio
    Solution for builds.

    .. code-block:: js

        gulp.task("Publish-All-Projects",
            function(callback) {
                var msbuild = new _msbuild(callback);
                msbuild.solutionName = config.solutionName + '.sln';
                var overrideParams = [];
                overrideParams.push('/p:Configuration=' + config.buildConfiguration);
                overrideParams.push('/p:DeployOnBuild=true');
                overrideParams.push('/p:DeployDefaultTarget=WebPublish');
                overrideParams.push('/p:WebPublishMethod=FileSystem');
                overrideParams.push('/p:DeleteExistingFiles=false');
                overrideParams.push('/p:publishUrl=' + config.websiteRoot);
                overrideParams.push('/m');
                overrideParams.push('/restore');
                msbuild.config('overrideParams', overrideParams);
                msbuild.config('version', config.buildToolsVersion);
                msbuild.build();
            });

    You can alternatively use Sitecore TDS or Helix Publishing Pipeline
    for local deployments, as seen in the new Sitecore Helix Examples.


Are there other tooling improvements which can help?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If your primary concern is the overhead of creating projects which follow
the Sitecore Helix conventions (naming, filesystem structure, etc.), then
you might consider some of the community tools which make this easier by
providing project "templates" which save you some clicks. Take care when
using these however that you remove any generated projects
`which the module does not need <#does-your-solution-contain-projects-you-do-not-need>`__.

To improve the performance of Visual Studio and reduce build times, you can
also consider using the `Filtered Solutions <https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019>`__
feature of Visual Studio 2019 to reduce the number of projects open when working
on a particular module.


The Role of Visual Studio Projects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Aside from the pragmatic issues, the architectural question at the root of
this decision is the role of a project/assembly in Visual Studio. This is in
fact the subject of Robert C. Martin's *Principles of Package and Component Design*,
which contain the `underlying principles <package-principles>`__ that Sitecore Helix
is based on. Based on these principles, Visual Studio projects form a "physical" boundary
and unit of change in Sitecore Helix.

Martin however makes an assumption that modules (packages) are released / deployed
independently. Due to the versioning and testing complexity this would put on the typical Sitecore
solution, Sitecore Helix actually `discourages partial deploys of modules </devops/deployment/strategy>`__,
meaning that the unit of release is the entirety of the application. If we are not deploying
and versioning these assemblies independently, it is a valid question as to whether
the modules really merit their own Visual Studio projects.

The modular architecture practices of Sitecore Helix though are meant to improve solution
*maintainability* and *long-term value*. The convention of using a separate web application
project for each module (which deploys to Sitecore CM/CD) means that all the code and
configuration related to a module are located in one place. Combine that with the module
filesystem and solution folder structure, and you also have the items, tests, and other related
code for that module. Practically, it's very easy for a future developer to find/discover
the code related to a desired system change. It's also easier to track and manage the dependencies
to and from that module.

It is true that `FxCop rules <https://www.teamdevelopmentforsitecore.com/Blog/sitecore-helix-fxcop-rules>`__
can be used to enforce Sitecore Helix dependency rules without separate projects, effectively giving you a
"logical" boundary between modules to help enforce dependencies. However the loss of *Common Closure*
and the potential maintenance impact should definitely be considered in taking this approach.


How many projects to use when consolidating
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Does Sitecore Helix really allow this?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. admonition:: Sitecore Helix Examples