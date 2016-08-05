Deployment strategy
~~~~~~~~~~~~~~~~~~~

A successful deployment strategy is highly connected with a good
versioning strategy. To consistently run a successful develop, test,
deploy cycle, it is important to be able to consistently version the
full application stack you are running on each environment and to be
able to recreate this across environments.

The modular architecture - as exposed through Helix - is not to be
confused with a modular deployment model where a base version of the
system is deployed and modules are installed on top of it – and where
the product lifecycle of the modules, underlying system and websites on
top of it are independent.

In Helix – as with development and Sitecore generally – it is highly
recommended to follow a strict develop, test and deploy lifecycle for
the whole application. This means that although development of the
individual modules might have different development speeds, the assembly
and versioning of the application stack happen at a particular point in
the application lifecycle, before the deployment onto the environments.
In other words, it is discouraged to do partial deploys of modules or
features from development to production. Deployments should happen on an
application-level scale, which fits with the availability requirements
of the business.

Managing the full application stack - which includes vendor systems such
as SQL Server and Sitecore XP, modules for those systems, and the
underlying operating system - can be handled in a variety of ways. The
best option often depends on the level of automation of the deployment
process. In most cases this is done through documentation. It can also
be handled by manifests that are read by automation systems and that
then automatically pull in the right underlying systems to create the
application stack in the build process. This methodology is done by
popular package systems such as Node/NPM, NuGet, Bower and even the
Sitecore Instance Manager. This methodology can also be employed as part
of your custom build process to build more complete deployment packages.

.. admonition:: Habitat Example

    Habitat leverages a number of package tools including NuGet, Node/npm
    and Bower to pull versioned packages into the build process.

    The internal continuous integration and build server for the Habitat
    project – which is hooked up to the public GitHub repository – is set up
    to create versioned Sitecore packages on nightly builds or releases.
    This means that the full Habitat application with all modules can be
    installed as a single package onto any environment – and thereby it is
    possible to consistently recreate a given version.

    Furthermore, the server fully automated reinstalls the Sitecore IIS
    website on an internal test server as part of the automated build. This
    includes reinstalling a blank Sitecore XP and required modules, and
    installing the Habitat content and application package on top. Even
    though this server is not publicly available as an example, parts of the
    build scripts, specifically the Gulp scripts, for the CI process are in
    the Habitat GitHub repository.

Tools such as Microsoft Team Foundation Server or Octopus Deploy can
help immensely with automating of the build and deployment process and
thereby in securing consistent versioning and deployment across
environments.