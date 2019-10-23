References from code
~~~~~~~~~~~~~~~~~~~~

In Sitecore solutions, references to templates and fields are among the
most frequent sources of rogue dependencies across modules (see :doc:`/principles/architecture-principles/dependencies`).
Therefore, maintaining tight control over these dependencies is
important in a Sitecore project.

Templates and fields should always be referenced by ID and never by
name. This makes it easier to have editor-friendly names or to change
field names if needed. Furthermore, hardcoded GUIDs tend to stick out in
code and views and therefore makes it easier to detect and avoid
implicit dependencies to templates and fields.

Define constants for a module’s templates in a single static class named
``Templates``. This static class is located in the root namespace for the module.
This makes it easy to explicitly reference a template in the business
logic or views of the module and makes it easier to discover references to a template
or field. The conventions define this as a static class to clearly signal the
``Templates`` type's unique function as a constants holder only, following the
`conventions for Constants in the Microsoft C# Programming Guide <https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/how-to-define-constants>`__.

The ``Templates`` static class should have a nested static class for each template
which each contains an ID member and a nested static class, Fields, which
contains all fields in the template.

.. admonition:: Sitecore Helix Examples

    The following shows the ``Templates`` static class for the *Feature / Basic Content* module in Helix Basic Company.

    .. code-block:: c#

        namespace BasicCompany.Feature.BasicContent
        {
            public static class Templates
            {
                public static class PromoCard
                {
                    public static class Fields
                    {
                        public static readonly ID Link = new ID("{B788E8BC-E944-4A2B-A4BE-3424643D322B}");
                        public static readonly ID Image = new ID("{21249F44-5F0F-4CFA-9474-8D72930D6575}");
                        public static readonly ID Headline = new ID("{4F73C02B-93CC-4C96-B9FF-9D0D8E853ED6}");
                        public static readonly ID Text = new ID("{13EB8DCA-281D-4E75-B6E1-701CA719BCD1}");
                    }
                }

                public static class SectionHeader
                {
                    public static class Fields
                    {
                        public static readonly ID Text = new ID("{59D24D0A-F955-4988-B26F-92039B4DF8BD}");
                    }
                }

                public static class HeroBanner
                {
                    public static class Fields
                    {
                        public static readonly ID Title = new ID("{5179186C-B95E-4E97-95AB-7958721A9AEB}");
                        public static readonly ID Subtitle = new ID("{89B0A8ED-0EE8-4512-B518-AB2C4C2A0B9E}");
                        public static readonly ID Image = new ID("{B5F61442-FF0F-46A5-90A8-D6D387DE24A0}");
                    }
                }

                public static class AccordionItem
                {
                    public static class Fields
                    {
                        public static readonly ID Title = new ID("{5718E787-142B-41D9-B5A1-0B18F45B8236}");
                        public static readonly ID Content = new ID("{45EFE66E-5AD2-4F1D-BAD5-FDF281688681}");
                    }
                }
            }
        }


A ``Templates`` class should never define constants for templates that are
not created in the module itself. In cases where Sitecore Helix conventions
allow a module to reference another (e.g. *Feature* to *Foundation*, or *Project*
to *Feature*), if a module needs to reference a template or field in that module,
it should reference the ``Templates`` static class in that module. Or better yet, that
module could expose an extension method or other means of consuming that template,
to avoid directly referencing the ID constants, as this dependency could make future
refactoring more difficult.

The practice of referencing different fields across modules by their
shared name – an equivalence to *duck typing* – is strongly discouraged.

.. note::
    
    **Duck Typing**

    “If it walks like a duck and it quacks like a duck, then it is a duck”

    https://en.wikipedia.org/wiki/Duck_typing

An often seen Sitecore example of this is to define that any field named
“Title” is used as the header of the page. The problem of this is that
“Title” might have different connotations for different content types.
For an Article, the title is typical headline of the text – and can be
used as the header for the page, but for a person, the Title is
typically their job title and might not make sense as the header of the
page. If modules need to share data, consider using design patterns such
as providers or pipelines to allow one feature to inject content into
another feature.

Since template inheritance in Sitecore can be compared to class
inheritance object-oriented programming, it is important that, when
querying an item’s template, you not use the *equals* operator but
rather an *is* operator.

.. admonition:: Sitecore Helix Examples

    The *is* operator in the Sitecore Item API is the `DescendsFrom`
    method on the `Item` class, which accepts a Template ID. This allows
    you to determine whether an item directly or indirectly inherits from a
    template. You can see this used in Helix Basic Company's `HeaderBuilder`
    class:

    .. code-block:: c#

            // Collect home/root item and its children which are navigable
            var items = new List<Item> { navigationRoot };
            items.AddRange(navigationRoot.Children.Where(item => item.DescendsFrom(Templates.NavigationItem.Id)));

    When querying for a specific base template via Content Search query, you
    will need to enable the ``_templates`` computed field. See the
    ``Sitecore.ContentSearch.[SearchProvider].DefaultIndexConfiguration.AllTemplates.config.example``
    example patches in your Sitecore installation, or the ``Feature.Products.ContentSearch.config``
    in Helix Basic Company.

    With this computed field available, you can map and query it in Content Search code:

    .. code-block:: c#

        var results = context.GetQueryable<ProductSearchQuery>()
            .Where(product => product.Paths.Contains(parent.ID) && product.Templates.Contains(Templates.Product.Id))
            .Select(x => new {
                Uri = x.UniqueId,
                Database = Factory.GetDatabase(x.UniqueId.DatabaseName)
            }).ToList();