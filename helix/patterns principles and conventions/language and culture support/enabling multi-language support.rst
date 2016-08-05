Enabling multi-language support
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Language support includes having all content on your sites and channels
provided through Sitecore, including main page content, related content,
headings, labels, metadata etc.

Remember to set up site metadata to reflect the context language and
culture, and that all number and date formats follow the format of the
context culture.

Consider Right-To-Left language support both in the content and visual
design implementation.

It is generally recommended not to mark fields as shared or unversioned
unless carefully thought through in a language and culture context.
Consider that some fields, such as image fields have metadata which
should be translated and list fields can have different sort orders
depending on language.

Languages are defined on a global implementation-scope level in Sitecore
and thus all sites and tenants will have the same languages installed.
In a multi-tenant and multi-site scenario (see 2.8) consider adding
business logic to make languages and cultures configurable by site and
tenant.

Habitat Example

Habitat relies on the standard Sitecore language support, but includes a
Feature layer module which allows individual sites to define the
languages they support. This will determine the languages shown to the
site visitor in the language selection dropdown.

    |image35|

    Figure 38: Language feature in Habitat