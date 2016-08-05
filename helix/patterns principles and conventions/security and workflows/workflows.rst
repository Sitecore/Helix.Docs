Workflows
~~~~~~~~~

Workflows in Sitecore reflect how editors in an organisation – or tenant
- work with the content. In a multi-tenant scenario, two autonomous
tenants (see 2.8) with different project layer modules, different
content architectures, page types, and sites will often need different
workflows assigned. Therefore, the actual Sitecore workflow definitions
belong in the Project layer modules.

To cater for flexibility across sites and projects, workflows are always
assigned to Page Type or Datasource templates (see 2.5.3). Therefore,
workflows are managed in a Project layer module.

Any custom actions or other business logic extensions to the Sitecore
workflow engine will belong to a foundation or feature layer module.