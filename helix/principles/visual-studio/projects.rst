Projects
~~~~~~~~

A Visual Studio solution can host a number of different project types,
such as Web Application projects, unit test projects, Commerce Engine plugins,
Sitecore TDS projects, behavioural testing projects, Xamarin
projects, etc., but modules are always grouped by their logical connection to 
a module – and never by type.

Projects are grouped together in a solution by the layer and module to
which they belong.

.. admonition:: Sitecore Helix Examples

    .. figure:: _static/basic-company-navigation-module.png

        Figure: Navigation module in Helix Basic Company with website,
        TDS, and unit test Visual Studio projects.

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

    Sitecore.Feature.Carts.Commerce
    Sitecore.Feature.Carts.Website
