Alternate Visual Studio Solution Structures
-------------------------------------------

One of the most common points of feedback on Sitecore Helix regards its
use of Visual Studio Projects to organize and set boundaries between
modules. Concerns about this practice include:

* (Re)build times for large solutions
* The overhead of creating multiple projects and properly organizing
  them when adding a module
* The deployment complexity created by large numbers of assemblies and
  multiple ASP.NET projects
* Management of Sitecore and other external dependencies across many projects,
  especially when upgrading Sitecore dependencies
* Solution load times on underpowered developer hardware
* Disagreement regarding the appropriate use of Visual Studio Projects /
  .NET Assemblies

The result is that some Sitecore solution architects are inclined to structure
their Visual Studio solutions with fewer projects, while still following Sitecore
Helix conventions in .NET namespaces and in the dependencies between classes.
Effectively, modules have "logical" boundaries rather than "physical"
boundaries.

You should apply Sitecore Helix in a way that you see as best for your customer, team,
solution, and requirements -- `it is not a rulebook </introduction/about-this-documentation.html#sitecore-helix-is-not-a-rulebook>`__.
However the reasons for departing from the conventions should be understood, as well
as the potential for accumulating technical debt when doing so. The goals of
`maintainability and long-term value </introduction/why-sitecore-helix>`__ should
drive these decisions.

.. note::
    It is true that adding projects to a Visual Studio solution can increase *Rebuild*
    times due to the overhead in building each project. However build times, with
    well structured dependencies, *can* be lower for large numbers of projects
    because projects that are unchanged do not need to be built - so less overall code
    must be compiled. Having multiple projects in a solution also means that
    MSBuild can use multiple cores when building the solution, because each project's
    compile is single threaded.

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

Recent improvements in the Visual Studio project file format can reduce
the effort required for external dependency management, and potentially improve
build times. `The PackageReference format <https://docs.microsoft.com/en-us/nuget/consume-packages/package-references-in-project-files>`__
for NuGet references is a significant improvement, and can be used with .NET Framework
ASP.NET applications, though with `some limitations <https://github.com/NuGet/Home/issues/5877>`__.
`SDK-style projects <https://docs.microsoft.com/en-us/dotnet/core/tools/csproj#additions>`__
further reduce overhead of the project system, and are being used successfully in the community
with Sitecore projects. However SDK-style projects are not `officially supported <https://github.com/dotnet/project-system/issues/2670>`__
by Microsoft with .NET Framework ASP.NET applications, and thus you may require some MSBuild
expertise on your team if you wish to use them.

Newer versions of Visual Studio are also much better optimized for opening large solutions.
To further improve the performance of Visual Studio and reduce build times, you can
also consider using the `Filtered Solutions <https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019>`__
feature of Visual Studio 2019 to reduce the number of projects open when working
on a particular module.

Finally, you should ensure that there are no MSBuild customizations in place
which force projects to build even if no files have changed. This could include
`BeforeBuild` targets.


The role of Visual Studio projects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Aside from the pragmatic issues, the architectural question at the root of
this decision is the role of a project/assembly in Visual Studio. This is
essentially the subject of Robert C. Martin's *Principles of Package and Component Design*,
which contain the `underlying principles <package-principles>`__ that Sitecore Helix
is based on. Based on these principles, Visual Studio projects form a "physical" boundary
and unit of change for modules in Sitecore Helix.

Martin however makes an assumption that modules (packages) are released / deployed
independently. Due to the versioning and testing complexity this would put on the typical Sitecore
solution, Sitecore Helix actually `discourages partial deploys of modules </devops/deployment/strategy>`__,
meaning that the unit of release is the entirety of the application. While modular deployment may be a
requirement for some very large solutions, if you are not deploying
and versioning these assemblies independently, it is a valid question as to whether
the modules really merit their own Visual Studio projects.

The modular architecture practices of Sitecore Helix though are meant to improve solution
*maintainability* and *dependency management*. It's easier to track and manage the dependencies
to and from a module, as they require an explicit project reference by the developer.
While these are easy enough to add, is an additional step and something that could be easily flagged in a
code review.

The convention of using a separate web application
project for each module (which deploys to Sitecore CM/CD) also means that all the code and
configuration related to a module are located in one place. Combine that with the module
filesystem and solution folder structure, and you also have the items, tests, and other related
code for that module. Practically, it's very easy for a future developer to find/discover
the code related to a desired system change. 

It is true that `FxCop rules <https://www.teamdevelopmentforsitecore.com/Blog/sitecore-helix-fxcop-rules>`__
can be used to enforce Sitecore Helix dependency rules without separate projects, effectively giving you a
"logical" boundary between modules to help enforce dependencies. However the loss of physical *Common Closure*
and the potential maintenance impact should still be considered when taking this approach.


How to structure when consolidating
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

How you consolidate the projects in your solution will ultimately depend on
the issue(s) you are attempting to address, and your view on the purpose and role
of Visual Studio projects.

* You may group Features into combined projects based on the concept of
  `Feature Groups </principles/architecture-principles/modules.html#groups>`__. This will
  reduce the number of projects but **care must be taken to avoid dependencies** between
  Features in a group. A Feature Group is merely a logical grouping of modules and
  does not affect Sitecore Helix conventions around Feature-to-Feature references.
* You may place an entire Layer into its own project as a "logical" grouping of modules.
  This benefits the Feature Layer most, as it should contain far more modules than other layers.
  Consolidating the Project Layer likely provides little benefit due to the number of modules, and
  may create confusion around the composition of each Project Module. You should
  take care when consolidating the Foundation Layer as well, as the allowance for
  Foundation-to-Foundation references means that these dependencies need to be closely
  monitored and managed.
* You can place all the code for a single deployment target (e.g. main Sitecore website CM/CD code)
  into a single assembly. This would be the most extreme example of treating a
  Visual Studio project as a unit of *deployment*. Your boundaries between Sitecore
  Helix modules becomes entirely logical, and Common Closure is lost to a large degree.
* You can split out modules as needed for reuse. This could be a requirement in organizations
  with multiple Sitecore deployments and a common shared code base. However in this case you
  likely should be independently managing and versioning these modules, and distributing them
  to other solutions via NuGet.

In all of the approaches above, you will need to consider the structure of your tests,
serialized items, and projects for `additional Sitecore services </principles/services/index>`__
as well. At the very least you should aim to retain the "logical" boundaries betweeen modules
by mirroring the filesystem and namespace structure within each of these.

It's strongly recommended that you use tools such as `FxCop rules <https://www.teamdevelopmentforsitecore.com/Blog/sitecore-helix-fxcop-rules>`__
and `Sitecore TDS Validation <https://www.hhogdev.com/help/tds/propvalidation>`__ to enforce
dependency rules between your modules if you consolidate Visual Studio projects in any
way.


Does Sitecore Helix really allow this?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Sitecore Helix is not a rulebook </introduction/about-this-documentation.html#sitecore-helix-is-not-a-rulebook>`__.
You should be pragmatic about applying its conventions rather than religious. When
deviating from them however, you should always:

* Understand why, understand the positive and negative impact of doing so,
  and anticipate the technical debt you may be accumulating.
* Document the deviation and alternative convention(s).
* Ensure you are still striving for `maintainability and long-term value </introduction/why-sitecore-helix>`__.

.. note::

    **Tracking Sitecore Helix Deviations**

    Any time you deviate from standard Sitecore Helix conventions, it's a good practice
    to document your reasons for doing so, what your solution-specific conventions
    are, and what the resulting technical debt may be. This documentation should be placed
    in the repository itself in a ``README``, ``Helix.md``, or similar document.


Consolidated Projects Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. admonition:: Sitecore Helix Examples - TDS Consolidated

    The *consolidated* version of Helix Basic Company demonstrates the extreme
    example of using a single web application project for the entirety of the
    solution.

    .. figure:: _static/basic-company-consolidated-solution.png

            Figure: Solution structure for Helix Basic Company - TDS Consolidated

    Note that additional projects are needed for tests and serialized items. A
    consolidated structure with Unicorn would similarly need a separate filesystem location
    for all serialized items. Also notice that even within the Web project, the module
    configuration files are intermixed.

    It is ultimately the responsibility of the Solution Architect to weigh this loss of
    "Common Closure" and potential maintenance impact, vs potential improvement in build
    times, deployment, etc.