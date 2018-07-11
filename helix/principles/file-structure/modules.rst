Module structure
~~~~~~~~~~~~~~~~

Each module has the following structure, note that not all modules will contain all of the elements:

::

    /…
        /[Module Name]     // Module root folder, named after the module (without prefixes)
            /website       // Houses the website code for the module, for example the Visual Studio project with the website business logic or views.
            /serialization // Contains the serialized data from Sitecore, for example templates, content or security data
            /tests         // Unit or other test types for the module
            /engine        // Houses the code for the plugin that runs on the Commerce Engine

.. admonition:: Habitat Example

    .. figure:: _static/image17.png

        Figure: Solution and module structure on disk

