Tenants
~~~~~~~

Tenants are groupings in the business organisation that need freedom and
autonomy to define and manage their own sites, channels and data, while
at the same time desire or require the ability to share with other
tenants. For example, this could be multiple departments in an
organisation with separate websites, but a willingness to collectively
define and share the features available on these sites in order to
reduce the cost of development and maintenance.

Multi-tenancy in Sitecore is primarily about creating a governance model
and technical architecture that support different requirements and
decision models.

Helix suits this scenario perfectly, as it defines a common feature and
foundation layer in the implementation, but allows multiple project
layer modules – one per tenant – that bring these features together.
Tenants can even define and implement new business specific features,
new modules, which are only used in their project layer module – and
thereby the architecture allows one tenant to adapt its solutions or to
change its business objectives without disrupting other tenants.

Note that although many Sitecore implementations have multiple sites,
most are single tenant, where a single organisational entity can make
decisions on the business direction of the overall implementation.

In any multi-tenancy scenario, it is very important to completely
understand and highlight the restrictions in autonomy, as well as the
benefits of the shared implementation, and subsequently define the
governance model for these overlaps between tenants. Although critical
for the success of the implementation, this is largely an organisational
task that lies outside the realm of the technology.

In a scenario where one implementation hosts two or more tenants with no
common content or desired sharing of features – in other words
completely autonomous tenants – it is highly recommended to split into
multiple implementations, with separate governance models.

Defining a tenant in Helix
^^^^^^^^^^^^^^^^^^^^^^^^^^

Although Sitecore offers a great platform to support multi-tenancy in
the software, there is no predefined tenant context in Sitecore. This
means that the borders between what is shared between tenants and what
can be defined autonomously is largely for you and the business to
define. This includes content hierarchies, content repositories, media,
workflows and more.

It is recommended that each tenant in a Helix compliant implementation
has its own project layer module, i.e. that each tenant has the freedom
to define its own set of datasource and page type templates (see 2.5.3)
as well as its own overall page layouts and sub layouts. If multiple
tenants share templates or layouts, it is recommended to have a shared
project layer module to host these entities. This gives the flexibility
for a tenant to use shared as well as specific page types and layouts in
their site or sites.

.. admonition:: Habitat Example

    In Habitat the Project/Common module contains primarily Datasource
    templates and placeholder settings that can be used across multiple
    tenants, i.e. project layer modules.

Content sharing or isolation between tenants comes largely down to
content hierarchy and security. By defining organisational roles, users
can belong to different tenants and content can be shared or separated.
Because of the powerful, feature-rich and fine grained security model in
Sitecore, pretty much any business requirements can be met. See more on
security in Helix in 2.10.

It is often not relevant for business logic to understand the tenant
context under which the business logic is running. Tenant related
locations such as datasource locations, datasource templates etc. can be
configured in Sitecore and there is often no use for an actual tenant
context API. If this is needed, it is recommended to create it.

.. admonition:: Habitat Example

    The Habitat example site defines one project layer module – effectively
    one tenant. Although the current implementation only defines a single
    site under the tenant - which lives under /sitecore/content/Habitat -
    all features support a multi-site scenario. In Habitat, the tenant or
    site is defined to have its own shared content repositories for features
    such as teasers, dictionary, FAQ’s etc. – which means this content could
    be shared across sites but not necessarily across to other tenants.

    The Habitat tenant defines isolated tenant specific data for the
    following areas:

    -  Page Type and Datasource Templates
    -  Page Layouts and Sub-layouts
    -  Personas and profiling
    -  Goals and outcomes
    -  Campaigns and engagement plans
    -  Social network accounts
    -  Forms
    -  Security domain

Please note that some 3\ :sup:`rd` party modules and features in
Sitecore do not fully support multi-tenancy or multi-site, and thus are
limited in ways they can be isolated across tenants or sites. An example
is that, by default, the Sitecore Analytics only allows analytics to be
broken down by site and thus not by tenant. Please refer to the product
documentation for the modules you are interested in using in your
implementation.