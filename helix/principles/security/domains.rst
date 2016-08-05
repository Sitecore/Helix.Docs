Domains
~~~~~~~

Sitecore ships with two standard domains, sitecore and extranet, which
in most cases are sufficient to accommodate the business requirements of
Sitecore implementations.

In advanced multi-tenant solutions, it can be required to create
multiple security domains to set up isolated roles and rights for each
tenant – either for the website or for the editors in Sitecore -
prohibiting access for the users of one tenant to another tenant’s
content – or even providing access across tenants or websites in some
cases.

For example, in a case where two tenants, A & B, have two different
projects with their own page types and content trees. This case could
have two domains *ProjectA* and *ProjectB*:

-  An editor in the *ProjectA* domain, *ProjectA/User*, could be
   granted access to his own organisations content by enrolling him in
   the *ProjectA/Editor* role.

-  Likewise, *ProjectB/User* in the *ProjectB* domain could be
   member of the *ProjectB/Editor*.

-  By enrolling *ProjectA/User* in the *ProjectB/Editor*
   role, the editor – despite belonging to the tenant A domain – would
   gain rights to the *ProjectB* content.

If there is a need for more granular rights on a feature level (as
described in 2.10.1) it could be beneficial to add an additional domain
on which modules across the layers can register feature level roles.
Using the previous example:

The *ProjectA/Editor* role could be a member or *Features/Accounts*
Admin and *Features/News* Admin, not only giving *ProjectA/User* access
to the ProjectA website and content but also to administer the feature
configuration for the *News* and *Accounts* feature.

.. admonition:: Habitat Example

    Because of its multi-tenant and multi-site nature, Habitat defines a
    domain for the Habitat Project layer. To exemplify the configuration of
    rights on a feature level, Habitat also defines a Modules domain where
    Feature layer modules define roles which grants access to the
    functionality.