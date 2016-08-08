Integration
~~~~~~~~~~~

Integration is the point where the implementation is combined into a
versioned solution. It is recommended to include as much as possible in
the packages generated in order to allow the deployment process to be as
simple as possible. The packages should include your implementation
specific files, standard Sitecore and other framework files,
configuration files, definition items in the Sitecore databases (see
:doc:`/principles/sitecore-items/item-types`) and any scripts to run during the deployment process. 
By covering as much as possible in this process result in a more simplified
deployment process by detaching the deployment process from your
development tools and repositories. Ideally only the configuration of
the specific environment and roles should happen during the deployment
process.

Depending on your tools stack – version control, configuration
management, item serialization etc. – various tools can help you with
the integration of your modules and solutions into a distributable
package. The format of this package will depend on the deployment
strategy and tools you choose. For example, Team Development for
Sitecore covers the complete application lifecycle from development
through to integration, and supports generation of Sitecore Update and
NuGet packages that can be automatically installed with for example
`Octopus Deploy <https://octopus.com/>`__.

.. admonition:: Habitat Example

    The internal build process used for the Habitat example site runs
    continuous integration and deployment through a TeamCity build server.
    Please note that these tools are publicly available on GitHub.

    The CI process is triggered by each change in the GitHub version control
    system and runs separate builds for each branch and pull request. The
    process executes the following tasks

    1. Restore NuGet packages and other external dependencies
    2. Build using MSBuild
    3. Run Unit and SpecFlow Tests
    4. No packages or assets are created from the CI build.

    The deployment build is triggered nightly on changes to the master
    branch – or can be triggered manually to create official releases or
    special branch releases. The process runs the following tasks:

    1. Restore NuGet packages and other external dependencies
    2. Build using MSBuild
    3. Run Unit tests
    4. Setup a clean Sitecore on the build server
    5. Publish solution to the Sitecore instance using the Gulp build scripts
    6. Create Sitecore package by executing the Sitecore Package Generator
    7. Publish Package to GitHub as a release

    The Sitecore package distributed via the GitHub releases page
    (https://github.com/Sitecore/Habitat/releases).

    Internally in Sitecore, official releases of Habitat and our demo sites
    that are built on Habitat are distributed as Sitecore Instance Manager
    (SIM) packages, which include database backups and analytics data. This
    allows deployment to local machines to happen in a one click process
    through the SIM user interface.

    These SIM packages are created on the build server too using PowerShell
    and the Sitecore Instance Manager command-line interface
    (https://github.com/sitecore/sitecore-instance-manager).