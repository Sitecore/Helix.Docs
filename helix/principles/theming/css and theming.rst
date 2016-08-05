CSS and Theming
~~~~~~~~~~~~~~~

The visual design – CSS and script – can be implemented based on the
mark-up frameworks and strategy – either in the foundation module as
part of a general theming approach or individually in the project layer
modules. This allows more individual design per tenant.

.. admonition:: Habitat Example

    The theming in the Habitat example site is primarily based on Bootstrap.
    The module Foundation/Theming implements the base CSS theme based on an
    Atomic Design approach. It references no feature specific mark-up, but
    clearly follows the mark-up defined in the frameworks.

    .. figure:: _static/image41.png
    
        Figure: Atomic Design Sass implementation in Habitat

The Helix approach will often require a close collaboration between
front-end development and Sitecore/.NET development as it requires a
common understanding of the architecture and reasoning behind it. A good
relationship and understanding between the different competencies in the
team is always a thing to strive for.

Avoid at all cost outputting HTML mark-up in code or business logic –
try as much as possible to stick to a single technology – for example
razor views – for mark-up, as this will facilitate management and
increase flexibility immensely.