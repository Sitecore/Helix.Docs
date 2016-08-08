Placeholders
~~~~~~~~~~~~

Placeholders in Sitecore allow the dynamic assembly of page layouts
either by allowing the editors to design specific pages, or by allowing
administrators to create predefined variations of layouts on Page Type
templates (see :doc:`/principles/templates/template-types`). Most often, placeholders are contained in the
layouts and sub-layouts in the Project layer modules. In rare cases
renderings in feature or foundation modules can contain placeholders,
for example when dealing with elastic or composite page components such
as tabs, accordions, carousels etc.

The actual conventions for placeholders and placeholder definitions are
very project specific, as they affect the dynamic page layouts (which
renderings can go where on the page) and the visual design of the pages
(how will renderings change appearance based on where they are placed).

Keep in mind that placeholders are not only used by editors to
dynamically design pages, but also allow developers to create variations
of pages merely by reconfiguring a Page Type template. Therefore you
should favor the dynamic constructing the page layout with many
placeholders and renderings, but ensure that you keep a consistent
visual design and coherent user experience by controlling the page
layout editing with security or by marking placeholders as non-editable.
This practice will greatly increase the flexibility and simplicity of
creating new page types and layouts as it reduces the need for
development.

.. admonition:: Habitat Example

    Even though the header of the Habitat example site is relatively static
    across the page types, it still contains around 10 placeholders - most
    of them marked as non-editable and thus only configurable by a
    developer. This makes it possible to reconfigure the header and reuse
    the renderings in the header for other site variations in a multi-site
    scenario or page variations such as campaign landing pages or commerce
    check-out pages.

    .. figure:: _static/image35.png

        Figure: Example of a header placeholder from Habitat

Define Placeholder definitions in the Project layer modules, as they
will need to reference the renderings from the feature modules. This
also allows multi-tenant scenarios where each tenant defines its own
unique mark-up and site structure.