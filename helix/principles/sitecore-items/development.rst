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

Now, for connecting items with modules in Sitecore, we use a basic
convention-based approach, where Definition Items are placed in folders
according to which the layers and module they belong to. This applies to
the items that belong to the typical configuration areas in Sitecore
such as:

* /sitecore/templates/[*Project\|Feature\|Foundation*]/[*Module*]
* /sitecore/system/Settings/[*Project\|Feature\|Foundation*]/[*Module*]
* /sitecore/layout/renderings/[*Project\|Feature\|Foundation*]/[*Module*]
* /sitecore/layout/layouts/[*Project\|Feature\|Foundation*]/[*Module*]
* /sitecore/layout/placeholder settings/[*Project\|Feature\|Foundation*]/[*Module*]
* /sitecore/layout/models/[*Project\|Feature\|Foundation*]/[*Module*]

.. admonition:: Habitat Example

    .. figure:: _static/image18.png

        Figure: Rendering items in the Feature/Accounts module

    .. figure:: _static/image19.png

        Figure: Template items in the Feature/Accounts module

Versioning items in modules
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Managing the Definition Items along with the business logic that uses
them poses a technical challenge, as the items are physically stored in
the Sitecore SQL databases while the business logic in code files are
stored on disk. For this challenge, the Sitecore concept of
serialization comes in handy.

Serialization allows items in the databases (typically in the Master and
Core database) to be written to disk in a text-based format and
subsequently restored into a database.

The Helix conventions define that serialized items should be versioned
as part of the owning module, next to the code and project files. Place
the serialized items on disk in a subfolder beneath the module:

/src/[*Foundation\|Feature\|Project*]/[*Module*]/serialization

Sitecore supports serialization through the developer toolbar in the
Content Editor, but this mechanism will by default serialize items to a
single location on disk – and it therefore not directly compliant with
the Helix modular architecture. Serialization is also supported through
the package generation tools.

Both these approaches are very manual in nature, and can be inefficient
to use with the Helix methodology. It is therefore recommended to look
into the third party tools available for item serialization, for example
`Team Development for Sitecore`_ or Unicorn_.

.. _Team Development for Sitecore: http://www.teamdevelopmentforsitecore.com/
.. _Unicorn: https://github.com/kamsar/Unicorn

.. admonition:: Habitat Example

    The default repository for the Habitat example site uses Unicorn for
    serialization. The Foundation/Serialization module imports the required
    NuGet packages and configures the module for the other modules in the
    implementation. Each module then subsequently configures Unicorn to
    serialize the relevant items into the /serialization subfolder for the
    module. Please refer to the Unicorn documentation for more information
    on using Unicorn.

    .. figure:: _static/image20.png

        Figure: Serialized items for the Feature/Navigation module

    The following shows the Unicorn configuration for the Feature/Navigation module of Habitat

    .. code-block:: xml

        <configuration xmlns:patch="http://www.sitecore.net/xmlconfig/">
        <sitecore>
            <unicorn>
            <configurations>
                <configuration name="Feature.Navigation" description="Feature Navigation" dependencies="Foundation.Serialization,Foundation.Indexing" patch:after="configuration[@name='Foundation.Serialization']">
                <targetDataStore physicalRootPath="$(sourceFolder)\feature\navigation\serialization" type="Rainbow.Storage.SerializationFileSystemDataStore, Rainbow" useDataCache="false" singleInstance="true" />
                <predicate type="Unicorn.Predicates.SerializationPresetPredicate, Unicorn" singleInstance="true">
                    <include name="Feature.Navigation.Templates" database="master" path="/sitecore/templates/Feature/Navigation" />
                    <include name="Feature.Navigation.Renderings" database="master" path="/sitecore/layout/renderings/Feature/Navigation" />
                </predicate>
                <roleDataStore type="Unicorn.Roles.Data.ReverseHierarchyRoleDataStore, Unicorn.Roles" physicalRootPath="$(sourceFolder)\feature\navigation\roles" singleInstance="true"/>
                <rolePredicate type="Unicorn.Roles.RolePredicates.ConfigurationRolePredicate, Unicorn.Roles" singleInstance="true">
                    <include domain="modules" pattern="^Feature Navigation .*$" />
                </rolePredicate>
                </configuration>
            </configurations>
            </unicorn>
        </sitecore>
        </configuration>

.. admonition:: Habitat Example

    Hedgehog Development, the company behind Team Development for Sitecore
    (TDS), maintains a separate branch for TDS and Habitat. Please refer to
    this branch, TDS documentation and support for more information on using
    Helix and Habitat with TDS.
    https://github.com/HedgehogDevelopment/Habitat/tree/TDS.

        .. figure:: _static/image21.png

            Figure: The Feature/Navigation module using Team Development for Sitecore

