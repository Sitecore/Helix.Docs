Module structure
~~~~~~~~~~~~~~~~

Each module has the following structure, note that not all modules will contain all of the elements seen below. Only the elements
that apply to that module should be created, for example not all modules will require serialization or have code that executes on all
of the services.

::

    /…
        /[Module Name]     // Module root folder, named after the module (without prefixes)
            /website       // Houses the website code for the module, for example the Visual Studio project with the website business logic or views.
            /serialization // Contains the serialized data from Sitecore, for example templates, content or security data
            /tests         // Unit or other test types for the module
            /commerce      // Houses the code for the plugin that runs on the Commerce Engine
            /xconnect      // Houses the code for plugins targeting the xConnect website

.. admonition:: Sitecore Helix Examples

    .. figure:: _static/helix-basic-filesystem-structure.png

        Figure: Solution and module structure on disk

