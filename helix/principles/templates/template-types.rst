Template types
~~~~~~~~~~~~~~

Now, to separate the purposes of the templates in the solution, we need
to define a number of different logical template types. These templates
types are not represented as such in Sitecore but rather differentiated
by the naming, where they are defined and how they are used in the
system.

Interface template
    Defines an interface for solution logic to work against, for example 
    by defining the fields that are used by a module’s logic or by simply 
    being a template in the template inheritance hierarchy of an item. 
    Can also be referred to as a base template.
Page type template
    Makes up the pages of the website. Derives from interface templates 
    and has a presentation layout.
Datasource template
    Items from this template are referenced by renderings as a datasource. 
    Has no associated layout. Sometimes derives from interface templates.
Settings template
    Used for lookup items for fields or to hold fields to configure the 
    business logic in modules.
Folder templates
    These templates are used for the folder items that make up the 
    scaffolding of the content structure.

====================  =======================  ======================
Template Type         Can have a page layout?  Exists in which layers
====================  =======================  ======================
Interface template    No                       Feature or Foundation
Page type template    **Yes**                  Project
Datasource template   No                       Project or Feature
Settings template     No                       Feature or Foundation
Folder templates      No                       All
====================  =======================  ======================

Interface templates
^^^^^^^^^^^^^^^^^^^

Interface Templates are maintained in the Feature and Foundation modules
and form the base of the content for the solution. They are never
instantiated but are solely used as base templates for Page Type
Templates or Datasource templates. The primary reason for this is that
page items require a layout definition, and a layout definition
inherently contains references to renderings in other features, which
means that templates defined in one feature will start referencing other
features, thus breaking the architectural principles, creating
dependencies and ultimately leading to higher coupling and less
flexibility and stability in the solution (see :doc:`/principles/architecture-principles/dependencies`).

Interface templates are prefixed with an underscore (\_) to signify that
they are interface templates and cannot be instantiated as items.

Interface templates can have an associated Standard Values item – given
that the module in which they are created wants to set universal
standards for the fields. Be aware that this standard value is universal
and will be applied across all inheriting templates, sites and tenants.

.. admonition:: Habitat Example

    Examples of Interface Templates in Habitat are present in almost all
    Feature modules, for example in the Sitecore.Feature.Navigation module
    where the \_Navigable template makes a page part of the navigation
    structure of the site.

    .. figure:: _static/image24.png

        Figure: Interface templates in the Navigation Module in Habitat

Fields
''''''

The content fields for business and presentation logic all live in
Interface Templates – never in Page Type templates or Datasource
Templates. Therefore, these content fields live with the logic that use
them (see :doc:`/principles/templates/references`).

Since fields and templates should always be referred to by ID and not by
name (see :doc:`/principles/templates/references`), try to be as descriptive and editor friendly as
possible when choosing a field name. Even though the item used to define
a field has a Title field that can be used to specify an editor-friendly
name for the field, it is common that this configuration option is not
used. This means that the actual fieldname is presented to the editor.
Therefore, avoid CamelCasing or AbbevInFldNames as this is not
considered editor friendly – in other words, always prioritize the
editor experience over technical considerations.

See more about fields and language support in :doc:`/principles/language-support/index`

Page Type Templates
^^^^^^^^^^^^^^^^^^^

Because of the flexible nature of the page layout in Sitecore, it can be
challenging to determine how many actual page types a site will require.
Theoretically a site could consist of a single page type, but with
enough flexibility in the layout and datasources to cater for any type
of page or content. This will greatly increase flexibility for the site
editor, but would also require more work when adding simple content
pages such as a news article. Alternately you could also configure a
very elaborate set of page types with all necessary permutations of
content and layouts, thereby making it easy for editors to create and
edit new pages and perhaps also increasing consistency in the overall
look and feel of the website.

Although there is no fixed result, the best option often lies somewhere
in between these two examples. A good rule of thumb is to create page
types based on the maturity and workflow of the editors, the information
architecture of the websites, as well as the main entities of content.
Page Type Templates are mainly used to assert consistency in the pages,
to facilitate management, and to force stringent information
architecture by defining insert options.

For example, it might be beneficial to define page types for the home
pages, sections, campaign landing pages etc. of the website in order to
define and maintain the overall hierarchy of the website. The leaf nodes
of the website will most likely be Article or common Content Pages, or
some of the more specialized News, Event, Product, etc. pages.

Furthermore, by defining very specialized pages, such as login,
registration, forgot password etc., as actual page types as opposed to
generic service pages, it can make it easier to maintain a consistent
look and feel for these pages with the other page types.

The architecture of Helix makes this kind of flexibility possible by
allowing you to define your page type and datasource structure
independently of the features, and the primary instrument in this
flexibility in template inheritance.

Interface templates and template inheritance in Sitecore can be compared
to multi-class inheritance object-oriented programming, such as C++. In
this type of programming, classes define the data they need and the
business logic to manipulate or present it. Another class can then
derive from multiple classes to inherit multiple capabilities from them.

In the same manner, a Page Type Template in Sitecore can derive from
multiple Interface Templates to inherit their data and use the
renderings (business logic) in its layout.

Page Type templates are only ever present in the Project layer, as these
are the integration points for the functionality in feature and
foundation modules. Page Type Templates are therefore maintained in a
common folder for a Project, equivalent to a site type. Each page in a
site of the given Project type are instances of a Page Type template.
This is actually very handy as all page types of a site are maintained
in a single location, which can make it easier to manage site-wide
changes to all page types.

Page Type templates typically have standard values that set up the page
type for all sites of the given project.

Page Type templates typically never have fields since there is never any
feature-specific business logic in the project layer that can leverage
these fields. These templates will get their content fields from the
Interface templates from which they derive.

.. admonition:: Habitat Example

    .. figure:: _static/image25.png

        Figure: Page Type Templates of the Habitat website

Datasource template
^^^^^^^^^^^^^^^^^^^

Datasource templates are used as the `Datasource Template` in Sitecore renderings.
They do not have any renderings themselves and are therefore used for items that
are not part of the page or navigation structure of the website.

The layer and inheritance structure of Datasource templates depends on the
requirements of your solution. If there is a requirement for project-specific
Standard Values or project-specific workflow, you may wish to use an Interface
template in your Feature and create a Datasource template in the Project
layer. In this case your Datasource template would not have its own fields.

In most cases however, you may not need a separate Interface template,
and you can create a Datasource template, with its required fields, directly in
your Feature.

.. admonition:: Habitat Example

    Because of the multi-site/multi-tenant nature of the Habitat project,
    the Datasource templates in Habitat are maintained in the Common Project
    layer module. This allows multiple project layer modules and sites (such
    as the Habitat site) to use these templates. This does not however stop
    a Project layer module from overriding one of the Common Datasource
    Templates and adding more or another functionality to it.

    .. figure:: _static/image26.png

        Figure: Datasource Templates in Habitat managed in the
        Project.Common module

.. admonition:: Helix Basic Company

    Because Helix Basic Company represents a simpler use case, it does
    not make use of Interface templates for its datasources.

Given the loose coupling and inheritance structure of the templates,
renderings typically are unaware of whether the context item they are
rendering is a Datasource or Page Type template. This allows the
functionality of feature modules to be used in a wide variety of ways
across Project layer modules.

Settings templates
^^^^^^^^^^^^^^^^^^

Settings templates can be managed in all business logic modules, for
example Foundation and Feature layer modules, and are for any
configuration settings (global or site-specific) needed by the module.
Unlike Interface Templates, these templates are often not used by
Project Layer modules as base templates, but are instantiated in the
content tree (or under /sitecore/system) directly from the template
defined in the module.

Depending on how dynamic the configuration needs to be, settings can be
single items with predefined template with fields for the configuration
data – or it can be an item structure where each item under a setting
root holds the configuration settings, like key/value pairs.

To avoid coupling and to encourage greater flexibility, avoid reusing
Settings templates across modules. Each module should define its own
Settings templates and settings structure, even if two modules use the
same technique for settings (for example Key/Value pairs).

Good Helix practice is to store global implementation-wide settings
under /sitecore/system/settings/*[Layer]*, as some settings can be
confusing for the low maturity editor personas - but always carefully
consider the maturity of the user managing the settings before deciding.
For example, /sitecore/system is not generally available to the average,
low maturity, editor and thus settings which are managed by this persona
should be placed as close to the content as possible, for example under
/sitecore/content/settings.

If there are settings that are tenant or site specific, they should be
stored either under a site or tenant related item under
/sitecore/system/settings or directly under the tenant or site in the
content tree.

It is also considered good practice to allow low maturity editors to use
the Experience Editor to manage the entire experience – including
settings. Consider implementing feature specific Experience Editor
extensions to allow for this.

Avoid storing environment specific settings in Sitecore. In order to
move Sitecore content items freely between environments (for example on
deployment to production or when testing with product data) these
settings should reside in for example .config files. If there is a need
for administrators to manage these types of settings, settings in
Sitecore can point to different .config file settings for example
<connectionStrings> or <sitecore><settings>.

.. admonition:: Habitat example

    .. figure:: _static/image27.png
        
        Figure: The background type Settings Templates for the Media
        Feature module in Habitat

Folder templates
^^^^^^^^^^^^^^^^

Folder templates are the templates that make up the content structure
outside the actual website structure, for example in datasource
repositories, settings, etc.

Avoid using the Folder template provided with Sitecore
(/sitecore/templates/common/folder). Instead, have each module define
its own folder templates. This will allow greater flexibility for
example in insert options and the content structure and provide better
user friendliness, for example, in icons.

.. admonition:: Habitat example

    .. figure:: _static/image28.png

        Figure: The datasource folder templates defined in the Common
        project in Habitat

    .. figure:: _static/image29.png

        Figure: The Habitat datasource repository using different folder
        templates

Rendering parameters templates
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In Sitecore, templates used for rendering parameters must derive from
the Standard Rendering Parameters (as opposed to the Standard Template).

In Helix rendering parameters templates should be prefixed with
ParametersTemplate\_ to distinguish them from the other template types.