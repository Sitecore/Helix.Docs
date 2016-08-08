Solution structure
~~~~~~~~~~~~~~~~~~

For maximum discoverability, the structure of the Visual Studio solution
must represent the layer and module structure, i.e. have solution
folders for Project, Feature and Foundation layers and separate solution
folders for each module. If there are any additional grouping of
modules, these can have their own solution folders.

The VS solution can have other solution folders (beyond Project, Feature
and Foundation) in the root of the solution, to increase discoverability
for specific files. However, these folders will never represent new
layers and must not contain any module projects.

.. admonition:: Habitat Example

    .. figure:: _static/image13.png
        :scale: 75%

        Figure: Habitat solution with feature and foundation modules

    .. figure:: _static/image14.png
        :scale: 75%

        Figure: Demo solution with specific feature and foundation modules
        
    .. figure:: _static/image15.png
        :scale: 75%

        Figure: Simple demo solution without feature or foundation modules