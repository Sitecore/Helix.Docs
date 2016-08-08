Templates
---------

Items and fields in Sitecore are used for a number of purposes, the most
obvious being to hold content which is presented on the channels and
structuring the information architecture for the sites. But items can
also be used for other purposes such as configuring the business logic
in features or structure the content in with an organisational focus to
make maintenance easier. The use of items - and thereby the template on
which they are based – helps determines the governance model around
them.

Fundamentally it is important that the data structures – i.e. templates
and fields - needed by modules are owned by the module itself, as this
makes it possible to separate the different modules and the
implementation and the logic in them. On the other hand, templates in
Sitecore are also the integration point of the pages and sites in
Sitecore, bringing together content and presentation into pages and the
business information architecture.

The template inheritance technique in Sitecore is instrumental in
allowing this separation of concerns in modules: To allow page types to
derive from the features required and to allow individual renderings to
reference items deriving from the features needed by the renderings. A
correct template structure allows this separation while still allowing
the content structure and management of the content to be designed with
the focus of the owning organisation or specific use case, i.e. with
focus on organisation structure, security, languages, etc.

.. toctree::
    :caption: Topics 
    :titlesonly:

    structure
    inheritance
    template-types
    references