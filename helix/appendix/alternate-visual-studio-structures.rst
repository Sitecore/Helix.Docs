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
    * Enforcing logical boundaries without VS Projects
        * TDS Validation
        * FxCop
        * Code Reviews
    * Consolidated Solution Architecture Options
        * Services/Targets and Consolidated Projects
        * Project per Layer
        * Feature Groups
        * Project per Target
    * Does Sitecore Helix really allow this?
        * Not a rulebook
    * What are the potential impacts?
        * Technical debt
        * Common closure - maintenance / finding things
        * Tracking dependencies, especially the soft ones
        * Independent release / reuse (only an issue if really needed!)
    * Helix Basic Company Example

Alterate Visual Studio Solution Structures
------------------------------------------

One of the most common points of feedback on Sitecore Helix regards its
use of Visual Studio Projects to organize and set boundaries between
modules. Concerns about this practice include:

* Excessive build times for large solutions
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

Ultimately there is a need and allowance for pragmatism when applying Sitecore
Helix conventions -- `it is not a rulebook </introduction/about-this-documentation.html#sitecore-helix-is-not-a-rulebook>`__.
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
lorem ipsum

Does your solution contain projects you do not need?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
lorem ipsum

* **Are there inefficiencies in your build scripts?**

  lorem ipsum

* **Are there other tooling improvements which can help?**

  lorem ipsum