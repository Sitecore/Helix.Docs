Projects
~~~~~~~~

A Visual Studio solution can host a number of different project types,
such as Web Application projects, Commerce Engine plugins, unit test projects, 
Team Development for Sitecore (TDS) projects, behavioural testing 
projects, Xamarin projects, etc., but modules are always grouped 
by their logical connection to a module – and never by type.

Projects are grouped together in a solution by the layer and module to
which they belong.

.. admonition:: Habitat Example

    .. figure:: _static/image16.png
        :scale: 75%

        Figure: Project grouping. Please note that even though the
        SpecFlow (see :doc:`/devops/testing/integration-testing`) projects 
        might test the individual features, they are grouped with the 
        Sitecore.Habitat project because they depend on
        the entire running website, and therefore the Sitecore.Habitat
        module.

A project, and assembly, should be named in a namespace-like fashion
with:

1. The overall customer, partner or solution name
2. The layer (optional for project layer modules)
3. The logical module grouping (optionally)
4. The module name
5. The logical function of the project
6. The target subsystem (optionally)

For example, the following VS project contains the unit tests for the
News feature module:

::

    Sitecore.Feature.News.Tests

Another example would be the following VS projects containing the functionality
required for the Carts plugin that runs on the Commerce Engine and related website code.

::

    Sitecore.Feature.Carts.Engine
    Sitecore.Feature.Carts.Website