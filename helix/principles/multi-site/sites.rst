Sites
~~~~~

The connotation of *a Site* varies, but in Sitecore a Site is a concrete
context to which different properties can be attributed. Hence a
multi-site implementation is an implementation where content can exist
in multiple different contexts (for example different channel types,
domains, websites etc.). Despite the association with a website, a site
can output content and define contexts for a range of channels, web,
mail, print etc. and different features and modules (such as for example
EXM – Email Experience Manager – and FXM - Federated Experience Manager)
can attribute different properties to the site context.

In this perspective, Feature or Foundation layer modules should always
be implemented in a multi-site setting, i.e. the business logic in
modules has to be context aware. Furthermore, this means that not only
can the Feature layer or Foundation layer modules in Sitecore utilise
the site definitions in Sitecore to determine context, they can also
extend the Sitecore site context with their own properties.

.. admonition:: Habitat Example

    The Foundation/Dictionary module extends the site context in Sitecore
    with the ability to configure a site specific dictionary location. This
    is done by adding an attribute to the Site definition and reading this
    through the Site context API.

    Note also how the Sitecore WFFM module uses the same technique to set
    the root folder for forms for the site.

    .. code-block:: xml

        <sites>
            <site name="habitat" patch:before="site[@name='demo']" 
                database="web" 
                virtualFolder="/" 
                physicalFolder="/" 
                rootPath="/sitecore/content/habitat" 
                startItem="/Home" 
                dictionaryPath="/sitecore/content/habitat/global/dictionary" 
                dictionaryAutoCreate="false" 
                domain="extranet" 
                allowDebug="true" 
                cacheHtml="true" 
                htmlCacheSize="50MB" 
                registryCacheSize="0" 
                viewStateCacheSize="0" 
                xslCacheSize="25MB" 
                filteredItemsCacheSize="10MB" 
                enablePreview="true" 
                enableWebEdit="true" 
                enableDebugger="true" 
                disableClientData="false" 
                cacheRenderingParameters="true" 
                renderingParametersCacheSize="10MB" 
                formsRoot="{4BC8A78C-44A7-46EB-8126-040D3F12CAA0}" 
                enableItemLanguageFallback="true" />
        </sites>

Most standard modules and functionality rely on the Site definition in
Sitecore for context, and it is therefore recommended to use the
standard Sitecore API to determine site context in business logic – as
opposed to implementing new logic to define the site context. If any
additional properties or extended logic are needed on the site context,
it is recommended to provide these to the feature modules through a
foundation layer module.

.. admonition:: Habitat Example

    The Habitat example site implements the Foundation/Multisite module that
    defines multi-site and multi-tenancy specific functionality for the
    feature modules. The most important feature in the Foundation/Multisite
    module is the ability for renderings to define site specific
    datasources. This means that each site can maintain a list of datasource
    locations for different renderings – which means that for example
    teasers does not have to be shared between all tenants in a solution,
    but only between sites within a tenant.

By default, sites are defined in the configuration files, in the
<sitecore><sites> section of the web.config, and the site context is
resolved as part of the request for each page or context. It is however
possible to add site definitions configured by other means, for example
the FXM (Federated Experience Manager) feature adds site definitions for
each domain matcher defined under /sitecore/system/Marketing Control
Panel/FXM, to allow requests from 3\ :sup:`rd` party sites to be
isolated by domain. There are also 3\ :sup:`rd` party modules which
allow you to define new site definitions using Sitecore items (see for
example the Multiple Sites Manager in Sitecore Marketplace
https://marketplace.sitecore.net/Modules/M/Multiple_Sites_Manager.aspx).

When adding properties to the site definitions and context, consider the
separation between configuration and settings (see :doc:`/principles/configuration/index`). In a standard
configuration scenario, site definition additions should be added to the
<site> definition in the configuration file. To add editor managed
settings to the site, modules should define templates which can be added
as base templates to the site root item for the project layer module, or
add settings items inside the site hierarchy. Regardless of which of the
two approaches you choose in your implementation, be consistent in how
you define context specific settings. Also, be conscious that advanced
settings might be confusing for the average editor, so consider limiting
visibility of and access to these settings to administrative users.

.. admonition:: Habitat Example

    The Habitat example site generally uses the base templates approach, for
    example, the Feature/Accounts module defines an AccountsSettings
    template which is assigned to the Site Root template in the
    Project/Habitat module.

    The module uses the site hierarchy to find the settings items for the
    module.

    .. code-block:: c#

        public virtual Item GetAccountsSettingsItem(Item contextItem)
        {
            Item item = null;

            if (contextItem != null)
            {
                item = contextItem.GetAncestorOrSelfOfTemplate(Templates.AccountsSettings.ID);
            }
            item = item ?? Context.Site.GetContextItem(Templates.AccountsSettings.ID);

            return item;
        }

Keep in mind that parts of the site definition configuration or settings
can be environment specific, and should the managed with an environments
specific perspective (see :doc:`/principles/configuration/index`).