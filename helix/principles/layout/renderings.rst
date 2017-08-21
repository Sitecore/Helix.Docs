Renderings
~~~~~~~~~~

Renderings, whether they are Controller or View Renderings typically
belong to the *Feature* layer modules as they are connected to business
features in the solution.  

Only sub-layout style renderings, i.e. view renderings with no business logic
but purely mark-up structure and placeholders, should occur in the
*Project* layer. Any controller renderings in project modules are
typically an example of business logic creeping into the project layer,
which should always be avoided.

In rare occasions renderings can occur in the *Foundation* layer, although this should generally be avoided. 
Examples could be a rendering which purely output metadata on the page or is only executing business logic.

Design for simplicity
---------------------

When designing your business-centric feature modules, keep in mind that
you are designing and implementing for maintainability and simplicity, not for
reusability. This means that you should keep focus on simplicity in the
razor views and avoid advanced configuration options. In other words, if
multiple variations of a view are required, prioritize the simplicity of
creating another view with alternate markup as opposed to coming up with
an elaborate mechanism for a generic view generating different sets of
markups.

For discoverability and simplicity, the naming of view files and the
rendering items in Sitecore should align as much as possible. This said,
the name of the Rendering item in Sitecore should be as editor-friendly
as possible – even if it differs from the actual filename. Generally,
throughout Sitecore you avoid using CamelCasingInNames or AbbevInNames
as it not considered editor friendly – in other words, in Sitecore
always favour the editor experience over the technical aspects.

Partial views should be prefixed with underscore (\_) to separate them
from the views references through Sitecore items or controllers.

Place view rendering files in subfolders under /views named after the
module to which they belong, for example /views/navigation/menu.cshtml
for the Feature layer Navigation module. In the case of Controller
Renderings, follow the standard ASP.NET MVC conventions for working with
razor views and Areas if these apply to your project.
