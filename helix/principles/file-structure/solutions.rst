Solution structure
~~~~~~~~~~~~~~~~~~

A single solution has a fixed folder structure on disk:

.. code-block:: c#

    /                                           // Solution root folder, contains the Visual Studio solution and other solution manifest or configuration files   |
        /src                                    // The root of the solution source (always *src*)                                                                 |
            /[*Feature\|Foundation\|Project*]   // Layer folder (ONLY *Project* or *Foundation* or *Feature*)                                                     |
                /[*Module Group*]               // Optional logical grouping of modules                                                                           |
                    /[*Module Name*]            // Module folder                                                                                                  |
        /[…]                                    // Other global solution folders, for example external references/modules or build and deployment scripts         |
