Dictionary
~~~~~~~~~~

When defining the content architecture of your implementation, some
pieces of presented content on the pages will not necessarily be part of
the main or related content, i.e. the context item or datasource items,
this could include labels for business forms, buttons or similar. As it
is recommended that all content on the pages can be edited through
Sitecore – for flexibility as well as language support reasons – there
needs to be a way of managing this content.

There are a few different mechanisms for managing these types of
content, but the most traditional way is through a Dictionary – which is
also supported in the Sitecore platform through the
Sitecore.Globalization namespace. Although the default Sitecore
implementation is somewhat rudimentary and does not for example include
Experience Editor or hierarchical support, it is often enough for many
use cases. The Sitecore Dictionary however does not have immediate
support for multi-site, multi-tenant and the modular architecture out of
the box and for more advanced use cases it is recommended to
re-implement the Dictionary concept within the solution.

Avoid reusing dictionary texts across modules, features or views as it
can limit the flexibility for the editors. Just because two labels have
the same value at the time of implementation does not mean that an
editor does not want to change them independently at some later time.

Dictionary entries are used in the presentation and business logic of
the modules and are therefore owned by the feature modules themselves.
In order to make itself available to all features, any custom Dictionary
API, functionality or principles herein should be a foundation level
module in the Sitecore implementation.

To increase modularity and discoverability in the dictionary, entries
should be referenced in a hierarchical structure. For example, their
structure [*module*]/[*view*]/[*text*] would be represented as
*Accounts/Login/Remember Me*. Furthermore, dictionaries should be
available on a site or tenant level to allow labels to be managed
individually across sites.

.. admonition:: Habitat Example

    The Habitat example site includes a custom Dictionary foundation layer
    module which enables site specific dictionaries, enables Experience
    Editor support and hierarchical support.

        .. figure:: _static/image39.png
            
            Figure: Hierarchical dictionary in Habitat