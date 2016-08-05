References from code
~~~~~~~~~~~~~~~~~~~~

In Sitecore solutions, references to templates and fields are among the
most frequent sources of rogue dependencies across modules (see 2.1.1).
Therefore, maintaining tight control over these dependencies is
important in a Sitecore project.

Templates and fields should always be referenced by ID and never by
name. This makes it easier to have editor-friendly names or to change
field names if needed. Furthermore, hardcoded GUIDs tend to stick out in
code and views and therefore makes it easier to detect and avoid
implicit dependencies to templates and fields.

Define constants for a module’s templates in a single struct named
Templates. This struct is located in the root namespace for the module.
This makes it easy to explicitly reference a template in the business
logic or views and makes it easier to discover references to a template
or field. The conventions define this as structs to clearly signal the
Templates type’s unique function as a constants holder only.

Each Templates struct should have a nested struct for each template
which each contains an ID member and a nested struct, Fields, which
contains all fields in the template.

.. admonition:: Habitat Example

    The following shows the Templates struct for
    Sitecore.Feature.Navigation:

    .. code-block:: c#

        namespace Sitecore.Feature.Navigation
        {
            using Sitecore.Data;

            public struct Templates
            {
                public struct NavigationRoot
                {
                    public static readonly ID ID = new ID("{F9F4FC05-98D0-4C62-860F-F08AE7F0EE25}");
                }

                public struct Navigable
                {
                    public static readonly ID ID = new ID("{A1CBA309-D22B-46D5-80F8-2972C185363F}");

                    public struct Fields
                    {
                        public static readonly ID ShowInNavigation = new ID("{5585A30D-B115-4753-93CE-422C3455DEB2}");
                        public static readonly ID NavigationTitle = new ID("{1B483E91-D8C4-4D19-BA03-462074B55936}");
                    }
                }

                public struct Link
                {
                    public static readonly ID ID = new ID("{A16B74E9-01B8-439C-B44E-42B3FB2EE14B}");

                    public struct Fields
                    {
                        public static readonly ID Link = new ID("{FE71C30E-F07D-4052-8594-C3028CD76E1F}");
                    }
                }

                public struct LinkMenuItem
                {
                    public static readonly ID ID = new ID("{18BAF6B0-E0D6-4CCE-9184-A4849343E7E4}");

                    public struct Fields
                    {
                        public static readonly ID Icon = new ID("{2C24649E-4460-4114-B026-886CFBE1A96D}");
                        public static readonly ID DividerBefore = new ID("{4231CD60-47C1-42AD-B838-0A6F8F1C4CFB}");
                    }
                }
            }
        }


A templates class should never define constants for templates that are
not created in the module itself. If a module needs to reference a
template or field in another module, it should reference the Templates
struct in that module.

The practice of referencing different fields across modules by their
shared name – an equivalence to *duck typing*\  [5]_ – is discouraged.
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

.. admonition:: Habitat Example

    The *is* operator is not native to Sitecore items and templates.
    Sitecore Habitat introduces the IsDerived extension method for the Item
    class. This method is located in the
    Sitecore.Foundation.SitecoreExtensions.Extensions.ItemExtensions class.