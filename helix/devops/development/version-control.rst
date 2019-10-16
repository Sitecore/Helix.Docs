Version Control
~~~~~~~~~~~~~~~

Throughout the development phase, the single source of truth should be
your version control system. In order to integrate and build versions of
your implementation across environments in a consistent and automated
fashion, you should strive to keep everything that your toolset needs in
the version control system. This does not in any way mean that all
files, frameworks and data need to be versioned, but rather that your
version control repository should have enough information to restore a
given version of your implementation.

This ambition assures that you consistently organise and version files,
frameworks and data together that belong together, so the individual
parts have less of a chance of getting out of sync with others.

The parts you should look to store together in your version control
system of choice include, but are not limited to: source code, tests
scripts, configuration files, Sitecore definition items, and build
scripts package manifests.

Some types of data can be harder to version control than others – for
example Sitecore items – (see :doc:`/principles/sitecore-items/index`). Finding tools to manage all types of
data through version control should be a priority as it will greatly
diminish the risk of manual errors and inconsistent deployments.

Versioning external requirements 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Keep in mind that your version control is not an integration
environment. In order to improve your maintenance and to better upgrade
and control the various parts of your solution, limit your version
control system to only contain the implementation additions and changes.
As much as possible, avoid adding standard frameworks and standard files
to version control. This includes the implementation web.config and
standard Sitecore config files (see :doc:`/principles/configuration/managing-config-files`).

There are a number of package managers, for example NuGet, Bower,
node/npm, that are useful to help install and integrate external
frameworks for different purposes. These all largely use the same
approach. They require a manifest file that points to the required
versioned packages. This manifest can be versioned alongside your
implementation specific files to allow your system to pull in the
packages from external repositories.

.. admonition:: Habitat Example

    Habitat uses NuGet packages for .NET dependencies and Bower for
    front-end technologies. The build system in Habitat is based on gulp and
    node.js, and therefore uses the node.js Package Manager (npm) for build
    script dependencies.

Some external dependencies, for example Sitecore itself, cannot
immediately be integrated via a standard package manager such as NuGet –
or might require custom configuration to be integrated correctly. For
this purpose, consider building custom scripts that automate the
integration or configuration of the dependencies. Remember to version
these scripts (either in the version control system itself or through a
package manager manifest) as part of your implementation.

.. admonition:: Habitat Example

    Build scripts in Habitat are versioned as part of the implementation,
    and have a simple task for pulling in Sitecore dependent assemblies for
    the build.

Note that there are approaches to adding the Sitecore assemblies to a
local NuGet repository. One option is to use the Sitecore Instance
Manager
(https://marketplace.sitecore.net/en/Modules/Sitecore_Instance_Manager.aspx).

Environment specific settings
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Generally, be careful about storing environment specifics in version
control, as version control tools are typically used exclusively in
the development process, and not during deployment or system
configuration. Having a too rigid process for deploying environment
specific changes (for example connection strings for new servers etc.)
might lead to changes directly in production environments –
circumventing processes altogether. Therefore, pay close attention to
who “owns” the environments and where these environment specific
settings then go.

For example: Consider an implementation team that consists of a
development team, a QA team and an IT admin team, . The development team
owns the individual development machines, CI environment and even the QA
environment, whereas the IT admin team owns the pre-production/staging
test servers and the production environment. If an emergency arises and
the IT team needs to switch a server (SQL, CDN, etc.), they must ask the
development team to make the change. This creates a bottleneck.
Therefore, the settings specific to the production environment , such as
those that live in the web.config, should not be maintained through the
development team tools, but rather through the IT admin tools.

Please note that – although confusing – this does not apply to the 
Environment definitions that form part of Sitecore Experience Commerce
which should certainly be included in Source Control.