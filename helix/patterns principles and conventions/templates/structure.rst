Structure
~~~~~~~~~

Given the type-centric nature of Sitecore, templates are all maintained
under /sitecore/templates in the Sitecore content tree, but
implementation specific templates are maintained as part of a module.
Specifically, in the following structure:

    /sitecore/templates/[Project\|Feature\|Foundation]/[*module*]

where module is the short name of the module, i.e. without prefixes.

.. admonition:: Habitat Example

    .. figure:: _static/image22.png

        Figure: Module specific template folders in Habitat

    Since the root layer folders (Project/Feature/Foundation) are not a
    native part of Sitecore, these folders are created by the
    Foundation/Serialization module.

