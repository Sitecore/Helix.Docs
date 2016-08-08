Layouts and sub layouts
~~~~~~~~~~~~~~~~~~~~~~~

Sitecore Layouts and Sub-layouts are in Helix primarily used to
structure the pages with the outer HTML mark-up.

Avoid statically binding renderings in sub-layouts, but rather bind all
renderings to layouts via layout definitions and placeholders. Static
binding will make the page and solution structure less flexible and
introduces multiple maintenance methodologies. Although you might end up
with longer lists of renderings in your layout definitions, the
centralised Page Type templates (see :doc:`/principles/templates/template-types`) and single layout
management methodology will prove more maintainable and flexible in the
long run.

.. admonition:: Habitat Example

    .. figure:: _static/image30.png

        Figure: Habitat home page layout definition

As layouts and sub-layouts (in MVC defined as View Renderings) typically
control the overall page design and therefore contain very site or
project specific mark-up, they belong in Project layer modules.

Reduce the number of layouts and sub-layouts by dynamically assembling
the pages in layout definitions and controlling assets such as scripts
and CSS on pages using asset management techniques (see :doc:`/principles/theming/index`). In some
scenarios, for example when implementing adaptive design using the
Devices in Sitecore, multiple layouts can be required, but in most
scenarios a single layout per site type or project module is sufficient.

Having elastic page layouts, i.e. page layouts that at editing time can
vary in structure, can reduce the need for sub-layouts quite
considerably and should be considered for all projects. Elastic layouts
are typically achieved through the use of dynamic placeholders, i.e.
allowing the number of placeholders of a page to vary and thereby
allowing an editor to construct page variations at will. Note that the
Sitecore Experience Platform does not provide support for dynamic
placeholders out of the box, but there are multiple variations available
as open source or through the Sitecore marketplace, for example
https://marketplace.sitecore.net/en/Modules/I/Integrated_Dynamic_Placeholders.aspx

.. admonition:: Habitat Example

    The Sitecore Habitat example site contains only a single layout for all
    page types – defined in the Habitat Project layer module - and few
    sub-layouts needed for consistent headers and footers across pages –
    defined in the Common Project layer module.

    .. figure:: _static/image31.png

        Figure: Habitat sub-layouts defined as View Renderings in the
        Project/Common module

    .. code-block:: html

        @using Sitecore.Foundation.Assets
        @using Sitecore.Foundation.Assets.Models
        @using Sitecore.Foundation.SitecoreExtensions.Extensions
        @using Sitecore.Mvc.Analytics.Extensions
        @inherits WebViewPage
        @{
            Layout = null;
        }
        <!DOCTYPE html>
        <!--[if IE 9]><html lang="en" class="ie9 no-js"><![endif]-->
        <!--[if !IE]><!-->
        <html lang="@Sitecore.Context.Language.CultureInfo.TwoLetterISOLanguageName">
        <!--<![endif]-->
            <head>
                <meta charset="utf-8" />
                <meta http-equiv="X-UA-Compatible" content="IE=edge">
                <meta http-equiv="Content-type" content="text/html; charset=utf-8">
                <meta content="width=device-width, initial-scale=1.0" name="viewport" />
                @if (!Sitecore.Context.PageMode.IsExperienceEditor)
                {
                    @Html.Sitecore().Placeholder("head")
                }
                <!-- Latest compiled and minified JavaScript -->
                @RenderAssetsService.Current.RenderScript(ScriptLocation.Head)
                @RenderAssetsService.Current.RenderStyles()
                @Html.Sitecore().VisitorIdentification()
            </head>
            <body class="header-static @(Sitecore.Context.PageMode.IsNormal ? "" : (Sitecore.Context.PageMode.IsExperienceEditor ? "pagemode-edit" : "pagemode-preview"))">
                <div id="main-container">
                    <header class="header-static">
                        @Html.Sitecore().Placeholder("header-top")

                        @Html.Sitecore().Placeholder("navbar")
                    </header>
                    <main role="main">
                        @Html.Sitecore().Placeholder("page-layout")
                    </main>
                    <footer>
                        @Html.Sitecore().Placeholder("footer")
                    </footer>

                    @Html.Sitecore().Placeholder("page-sidebar")
                </div>
                @RenderAssetsService.Current.RenderScript(ScriptLocation.Body)
            </body>
        </html>

    The Habitat example site uses the DynamicPlaceholders.Mvc package
    available through NuGet
    (https://www.nuget.org/packages/DynamicPlaceholders.Mvc/) to allow
    elastic page layouts.