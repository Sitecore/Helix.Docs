Structure
~~~~~~~~~

Given the type-centric nature of Sitecore, templates are all maintained
under ``/sitecore/templates`` in the Sitecore content tree, but
implementation specific templates are maintained as part of a module.
Specifically, in the content tree they use the following structure:

::

    /sitecore/templates/[Project|Feature|Foundation]/[Module]

where *Module* is the short name of the module, i.e. without prefixes.

.. admonition:: Sitecore Helix Examples

    .. figure:: _static/basic-company-template-structure.png

        Figure: Module specific template folders in Helix Basic Company

    The root layer folders (Project/Feature/Foundation) are now a
    native part of Sitecore.

