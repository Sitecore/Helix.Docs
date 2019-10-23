Managing items in development
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Since Definition Items and some Content Items in Sitecore are created
and managed in the development environment and, given the Common Closure
Principle (*“what changes together should live together”*), we need not
only to make it obvious which items in Sitecore belong to which modules,
but also to manage and version the items alongside the code in these
modules.

Associating items with modules
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For connecting items with modules in the Sitecore tree, we use a basic
convention-based approach, where Definition Items are placed in folders
according to which the layers and module they belong to. This applies to
the items that belong to the typical configuration areas in Sitecore
such as:

* ``/sitecore/templates/[Project|Feature|Foundation]/[Module]``
* ``/sitecore/layout/renderings/[Project|Feature|Foundation]/[Module]``
* ``/sitecore/layout/layouts/[Project|Feature|Foundation]/[Module]``
* ``/sitecore/layout/placeholder settings/[Project|Feature|Foundation]/[Module]``

.. admonition:: Sitecore Helix Examples

    .. figure:: _static/basic-company-basic-content-rendering-items.png

        Figure: Rendering items in the Helix Basic Company *Feature/Basic Content* module

    .. figure:: _static/basic-company-basic-content-template-items.png

        Figure: Template items in the Helix Basic Company *Feature/Basic Content* module

Versioning items in modules with Sitecore TDS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Managing the Definition Items along with the business logic that uses
them poses a technical challenge, as the items are physically stored in
the Sitecore SQL databases while the business logic in code files are
stored on disk. For this challenge, the Sitecore concept of
serialization comes in handy.

Serialization allows items in the databases (typically in the Master and
Core database) to be written to disk in a text-based format and
subsequently restored into a database. Sitecore provides the
`Sitecore TDS <https://www.teamdevelopmentforsitecore.com/TDS-Classic>`__
Visual Studio plugin which allows you to serialize and source control
Sitecore items within a Visual Studio project.

The Helix conventions define that serialized items should be versioned
as part of the owning module, next to the code and project files. Place
the serialized items on disk in a subfolder beneath the module. When using
Sitecore TDS, the recommended folder structure is:

::

    /src
        /[Foundation|Feature|Project]
            /[Module Name]
                /tds
                    /master
                        /[Module].Master.scproj     // TDS project for the 'master' database (if needed)
                    /core       
                        /[Module].Core.scproj       // TDS project for the 'core' database (if needed)


.. note::

    The use of *tds* for the folder name (versus e.g. *serialization*) is in part
    to reduce the filesystem characters consumed by the convention, which can contribute to
    challenges with long filesystem paths on Windows.

When placing the TDS projects within your Visual Studio solution for a module, always place
them within the solution folder for the associated module.

Sitecore TDS includes a number of features to assist when working across multiple
Helix modules in a Visual Studio Solution. See `Sitecore TDS documentation <http://hedgehogdevelopment.github.io/tds/>`__
for information on `Global Configuration <http://hedgehogdevelopment.github.io/tds/chapter4.html#global-config>`__,
`Multi-Project Properties <http://hedgehogdevelopment.github.io/tds/chapter4.html#multi-project-properties>`__,
`Sync All Projects <http://hedgehogdevelopment.github.io/tds/chapter4.html#sync-all-projects-using-history-window>`__,
`Quick Push <http://hedgehogdevelopment.github.io/tds/chapter4.html#quick-push-items>`__, and more.

.. admonition:: Sitecore Helix Examples

    The TDS version of Helix Basic Company uses Sitecore TDS to manage Sitecore items
    for each module.

    .. figure:: _static/basic-company-tds-projects.png

        Figure: TDS projects in the Helix Basic Company - TDS solution.

    .. figure:: _static/basic-company-tds-filesystem.png

        Figure: TDS filesystem folders in the Helix Basic Company - TDS solution.    

Versioning items in modules with Unicorn
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When using the open source `Unicorn <https://github.com/SitecoreUnicorn/Unicorn>`__ utility
to serialize items, the convention for filesystem organization of items in a module is:

::

    /src
        /[Foundation|Feature|Project]
            /[Module Name]
                /serialization
                    /[predicate]        // e.g. 'templates' in master
                    /[predicate]        // e.g. 'renderings' in master
                    /[predicate]        // e.g. 'buttons' for Experience Editor buttons in core

Typically a  *Foundation/Serialization* module will contain the needed base Unicorn
references and configuration, and each module with items will define its own Unicorn configuration.

Unicorn's configuration system includes a concept of *abstract* configurations with built-in
variables replacement for Helix ``$(layer)`` and ``$(module)`` names. For more information,
see `Unicorn Documentation <https://github.com/SitecoreUnicorn/Unicorn>`__.

.. admonition:: Sitecore Helix Examples

    The Unicorn version of Helix Basic Company uses Unicorn to manage Sitecore items
    for each module.

    .. figure:: _static/basic-company-unicorn-filesystem.png

        Figure: Serialized items for the *Feature/Basic Content* module

    The base abstract configuration from the *Foundation/Serialization* module is:

    .. code-block:: xml

        <configuration xmlns:patch="http://www.sitecore.net/xmlconfig/">
            <sitecore>
                <unicorn>
                    <configurations>
                        <configuration name="Foundation.Serialization.Base" abstract="true">
                            <targetDataStore physicalRootPath="$(sourceFolder)\$(layer)\$(module)\serialization" />
                            <predicate type="Unicorn.Predicates.SerializationPresetPredicate, Unicorn" singleInstance="true">
                            </predicate>
                            <syncConfiguration type="Unicorn.Loader.DefaultSyncConfiguration, Unicorn" singleInstance="true" updateLinkDatabase="false" updateSearchIndex="true" maxConcurrency="1" />
                        </configuration>
                    </configurations>
                </unicorn>
            </sitecore>
        </configuration>

    It can then be used to minimize the configuration in other modules, e.g. the *Feature/Basic Content* module:

    .. code-block:: xml

        <configuration xmlns:patch="http://www.sitecore.net/xmlconfig/">
            <sitecore>
                <unicorn>
                    <configurations>
                        <configuration name="Feature.BasicContent" extends="Foundation.Serialization.Base" description="BasicContent definition items" dependencies="Foundation.*" patch:after="configuration[@name='Foundation.Serialization.Base']">
                            <predicate>
                                <include name="templates" database="master" path="/sitecore/templates/Feature/BasicContent" />
                                <include name="renderings" database="master" path="/sitecore/layout/renderings/Feature/BasicContent" />
                                <include name="buttons" database="core" path="/sitecore/content/Applications/WebEdit/Custom Experience Buttons/BasicContent" />
                            </predicate>
                        </configuration>
                    </configurations>
                </unicorn>
            </sitecore>
        </configuration>