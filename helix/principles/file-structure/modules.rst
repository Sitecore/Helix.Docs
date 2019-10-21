Module structure
~~~~~~~~~~~~~~~~

Each module has the following structure:

::

    /…
        /[Module Name]     // Module root folder, named after the module (without prefixes)
            /code          // Houses the main code for the module, for example the Visual Studio project with the module business logic or views.
            /serialization // Contains the serialized data from Sitecore, for example templates, content or security data
            /tests         // Unit or other test types for the module

.. admonition:: Sitecore Helix Examples

    .. figure:: _static/helix-basic-filesystem-structure.png

        Figure: Solution and module structure on disk

