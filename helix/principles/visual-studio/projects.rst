Projects
~~~~~~~~

A Visual Studio solution can host a number of different project types,
such as Web Application projects, unit test projects, Team Development
for Sitecore (TDS) projects, behavioural testing projects, Xamarin
projects, etc., but modules are always grouped by their logical
connection to a module – and never by type.

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

For example, the following VS project contains the unit tests for the
commerce orders feature module:

::

    Sitecore.Feature.Commerce.Orders.Tests