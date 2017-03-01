Definition Scope
~~~~~~~~~~~~~~~~

Just like code, templates, views etc., configurations and settings
defined in your implementation relate to a specific module and should
therefore be managed and versioned with that module.

Project layer modules should never define new settings or
configurations, as it indicates business logic in the project layer –
which should always be avoided.

Solution-wide
^^^^^^^^^^^^^

Solution-wide settings and configurations cover the entire
implementation. In other words, they are defined once within the
solution and their values will affect the entire implementation.
Examples of solution-wide configurations are all the <settings> defined
under <sitecore> in the web.config. Examples of solution-wide settings
in Sitecore are the installed languages and aliases, which are defined
under /sitecore/system.

Solution-wide Configurations should be defined in a .config file,
whereas Solution-wide Settings should be defined under
/sitecore/system/settings or similar.

Settings defined for a single Project, Feature or Foundation layer
module should be defined in their corresponding module folder under
/sitecore/system/settings/[layer]/[module].

Be cautious when creating solution-wide configurations in your feature
and foundation modules, as you might be restricting the flexibility of
the implementation. It is generally good practise to make features as
context-aware as possible, for example in terms of support for
multi-site, multi-tenant or multi-language. For example, by moving a
configurable path from a Solution-wide configuration under
<sitecore><settings> in the to the Sitecore <site> node in the
web.config, one can help make a feature site context specific - or by
changing the value of an Unversioned setting field, one can make a 
feature context language specific.

Context-wide
^^^^^^^^^^^^

Context-wide covers, as the name implies, a given context. This means
that a configuration or setting can exist in multiple places, for
example per tenant, per site, per language, per database, content
hierarchical, by taxonomy etc. The context is, in other words, defined
by the business logic in the module that defines the configuration or
setting. Examples of context configurations are domain names on sites,
search indexes, security domains, user profiles etc.

Sitecore defines a number of contexts to which you can associate your
own configuration or settings, for example the site definitions in the
web.config.

.. admonition:: Habitat Example

    The Foundation/Dictionary module in the Habitat example site allows
    dictionary content to be defined on a site context. This is done by
    defining a dictionary path on the ``<site>`` definition in the web.config.

    .. code-block:: csharp

        private Item GetDictionaryRoot(SiteContext site)
        {
            var dictionaryPath = site.Properties["dictionaryPath"];
            if (dictionaryPath == null)
                throw new ConfigurationErrorsException("No dictionaryPath was specified on the <site> definition.");
            var rootItem = site.Database.GetItem(dictionaryPath);
            if (rootItem == null)
                throw new ConfigurationErrorsException("The root item specified in the dictionaryPath on the <site> definition was not found.");
            return rootItem;
        }

Context-wide settings are often created in the content section as part
of a hierarchical content tree, for example site-context settings are
defined on the site root item or on an item under the site root. This
allows easy access to the settings for Sitecore users.
