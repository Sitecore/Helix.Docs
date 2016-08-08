Building your solution
~~~~~~~~~~~~~~~~~~~~~~

Building your implementation is typically part of three processes:

Local builds
    which typically happen in Visual Studio and assisted with scripts or tools for deployment onto the local IIS (See :doc:`/devops/development/setting-up`).

Continuous Integration (CI)
    which happens automatically on a build or CI server when someone commits a change to the version control.

Deployment
    or *integration*, which is when the implementation is combined into a distributable package for deployment through the environments.

The continuous integration and deployment builds are very similar as
they most often deal with the combined implementation. This is opposed
to the local builds, where a developer might be working on a single
module or modules logically grouped together in a single Visual Studio
solution (See :doc:`/principles/visual-studio/index`).

.. figure:: _static/image44.png

    Figure: Development, integration and deployment process

Modular architecture is really only focused on the
development process, not the deployment. Do not confuse Helix with a
modular approach to building or running Sitecore environment. In the
integration process (continuous or during deployment builds) the modules
should be combined into a versioned and distributable package that can
be tested and deployed consistently through the environments (see :doc:`/devops/deployment/index`).

It is recommended to run deployment builds – and continuous integration
builds – on a separate build server, using a dedicated build system such
as Microsoft Team Foundation Server, Visual Studio Team Services,
TeamCity, Jenkins, Bamboo, etc. This helps assures a consistent build
and integration process, which is important for quality in the
deliveries and agility in development and support.