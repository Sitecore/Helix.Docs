Item types
~~~~~~~~~~

The items in your Sitecore databases can be split, for management and
governance purposes, into two main categories: *Content Items* and
*Definition Items*. The categorization determines the process in the
application lifecycle that “owns” the creation and management of the
items, as well as in which direction the items flow: from development,
through to test, through to production – or the opposite.

Although it is not always 100% possible in practice, the better you can
clearly split the Sitecore items in your implementation into these
categories, the easier it will be to manage your implementation through
development, integration and deployment - as well as new features and upgrades.

Definition items
^^^^^^^^^^^^^^^^

Definition items are items that typically define the configuration or
structure of the implementation or which contain metadata for assets in
the solutions. These items are owned, i.e. created and managed, in the
development environment and moved as part of versioned deployments from
development to test to production.

Think for example of a *View Rendering* in Sitecore, which consists of a
Razor view file (.cshtml) and an item somewhere under
``/sitecore/layout/renderings``. Both these pieces together make up the View
Rendering in Sitecore, and they should be managed and versioned together
in the development process. If the filename of the view file changes,
the filename in the Sitecore item needs to change – and these two pieces
need to be deployed in a versioned and consistent process through from
development to test to production. The item itself should never be
changed by editors in production (just as the .cshtml file should never
be changed in production), as the next deployment might overwrite the
production change. The View Rendering item in Sitecore is a therefore a
Definition item.

These item types are typically Definition items:

-  Layout and Rendering items
-  Template and Field items
-  Placeholder setting items
-  Custom field types
-  Lookup items for settings
-  All items in the Core database

.. admonition:: Habitat Example

    Note how in the Habitat example sites, all Feature and Foundation
    modules almost exclusively contain Definition Items. This means that
    when developing or extending modules developers can know that the items
    are managed in the development environment and deployed along with their
    business logic as a part of new versions.

    The Project layer modules on the other hand consist of a majority of
    Content items, which are managed by editors.

Content items
^^^^^^^^^^^^^

Content Items are items which are managed by the editors on the website
and contain content that is output on the sites or channels of the
website, or that are part of shaping the specific user experience of the
pages. Content Items are owned by the production environment, i.e. the
editors and administrators.

An example of a Content Item is a site home page item. Although this
item is often created very early in the initial development process and
deployed into production on the first deploy, the item itself is owned
by the production environment and should never be overwritten by an item
coming from the development or test environments. On the other hand, it
could be very useful to get a snapshot of the Home Page from production
back into the test or even development environments for realistic
testing purposes.

Even if Content Items are owned by the production environment, sometimes
the business logic will have to know about the specifics of these items,
for example their location or type, or the development process might
need to change specific data in them – for example, if business logic
introduces new settings or fields in a template that require initial
values in the content of the sites. Therefore, Content Items can be
split into two sub-categories: items that are created in development and
deployed once into production, and items that are created and managed in
production.