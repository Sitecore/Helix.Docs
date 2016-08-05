Rendering parameters
~~~~~~~~~~~~~~~~~~~~

Rendering parameter templates are managed in the same module as the code
that uses them, either in the feature module where the rendering and
controller logic resides or in a foundation level module. In the latter
case a rendering parameters template in a feature module can derive from
one or more rendering parameters templates from foundation modules and
include all parameters in the rendering. If the rendering parameters
template reference any setting items, make sure that the items along
with their templates reside in the same module (or in a lower layer
module) as the parameters template itself.

Please, consider carefully what configuration of the rendering belongs
in the datasource or on the context page, as opposed to the rendering
parameters. Rendering parameters are generally considered less editor
friendly than content fields and are often restricted to administrators,
but it is possible through rendering parameters to preconfigure a number
of compatible renderings – which makes the rendering parameters both
accessible and very user friendly.

Consider using Field Editor buttons for managing those hidden fields in
the Experience Editor
(http://www.nonlinearcreations.com/Digital/how-we-think/articles/2016/03/Sitecore-8-and-8-1-How-to-add-a-Field-Editor-Button-to-a-component-in-Experience-Editor-Mode.aspx).

.. admonition:: Habitat Example

    Habitat has many examples of Rendering Parameters applied throughout the
    solution, for example, many renderings use the
    *ParametersTemplate\_HasBackground* template to render different
    background colours and images for the rendering.

    Habitat also has an example of a general Field Editor button
    (implemented in the Foundation.FieldEditor module) which makes it
    possible to edit all fields in a datasource item from the Experience
    Editor.