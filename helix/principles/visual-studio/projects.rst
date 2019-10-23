Projects
~~~~~~~~

A Visual Studio solution can host a number of different project types,
such as Web Application projects, unit test projects, Sitecore
TDS projects, behavioural testing projects, Xamarin
projects, etc., but modules are always grouped by their logical
connection to a module – and never by type.

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

For example, the following VS project contains the unit tests for the
commerce orders feature module:

::

    Sitecore.Feature.Commerce.Orders.Tests