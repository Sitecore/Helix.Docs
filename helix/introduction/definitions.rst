Definitions
-----------

Module
    A Module is a conceptual grouping of assets which relates to a business
    requirement. The conventions, processes and tools described in this
    document relate to managing all these assets in a module-centric – and
    thereby business centric – way. For example, when the company asks that
    their Sitecore solution contains website search, all assets, business
    logic and configuration relating to search belongs to the Search module.

Solution
    Technically often refers to Visual Studio solution, but conceptually, it
    can also refer to an *implementation*. For example, Michael is a
    developer at his company. Most of his time is spent working in the
    Visual Studio solution that contains the code that powers his company’s
    Sitecore solution.

Project
    In technical terms, *project* often refers to Visual Studio project, but
    conceptually can also to the process of implementing the business
    requirements into an *implementation*. For example, Michael is a
    developer at his company. Most of his time is spent working in one of
    the five Visual Studio projects that contain the code that powers his
    company’s Sitecore solution. He is starting on a new implementation,
    which is a project that will result in new features being added to his
    company’s website.

Serialization
    The process of writing data in the Sitecore databases to disk so that it
    can maintained in version control and packaged into deployments across
    environments.

Assets
    Technically an Asset refers to a digital asset such as images, but can
    also mean the actual output from any process or task in your entire
    application lifecycle: code, files, visual design, data, content,
    configuration changes, deployment packages etc.

Dictionary
    A collection of named text snippets which can be translated across
    languages and used in the UX, for example on websites, Sitecore tools,
    e-mails, etc.

Tenant
    A product owner of one or more sites in a Sitecore implementation.
    Sitecore allows multiple tenants to share a single *implementation*,
    which allows certain resources to be shared (such as templates and
    digital assets), while allowing other resources (such as sites and other
    business entities) to be defined and managed independently (see 2.8).

Site
    A collection of content and output with a common overall business
    objective, and sharing a common set of assets. A site can output content
    to any channel, not necessarily as a website to the web channel. In
    Sitecore, technically a site is a context under which content is output,
    i.e. which assets the business logic can access.

Website
    A website is a *site* that can output content to the web channel. See
    Site.

Implementation
    An implementation, or customer implementation, is the total number of
    modules, features and functionalities developed and deployed to solve
    the customer business problem. Also often referred to as the *solution*.
