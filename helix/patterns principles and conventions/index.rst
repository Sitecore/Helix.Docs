Patterns, Principles and Conventions
====================================

Helix describes the overall architecture of your Sitecore solution and
thus communicates some guidelines and conventions which should be
durable and flexible enough to be applied to any Sitecore project or
business. The architecture pattern described by Helix is often referred
to as `Component-based Architecture`_ or Modular Architecture.

Modular architecture provides you with a framework to optimize and
increase productivity by describing how to isolate domain logic to make
the whole solution or implementation more manageable. Modular
architecture is therefore in its foundation a way of making sure that
the resulting solution is flexible enough for whatever change might be
coming. There are many great benefits to modular architecture such as
reusability and rapid development, but the core motivators behind the
conventions are simplicity, flexibility and extensibility in the
implementation.

Keep in mind though, that the principles behind modular architecture
will not ensure you remain within the conventions or confines of said
principles. This is defined by the methodology on which you apply the
architecture and even the specific tools you use to build the final
solution.

.. admonition:: Habitat Example 

    The Habitat example implementation is not meant to dictate the specific
    methods or tools to use in your Sitecore project but should rather be an
    example of how the architectural design pattern, namely modular
    architecture, can be implemented including a methodology and a set of
    tools to support it.

    You should always consciously select the tools and methods which fit the
    scenario, your development team and your business.

.. toctree::
    :caption: Topics 
    :titlesonly:

    architecture principles/index
    visual studio/index
    file and disk structure/index
    managing sitecore items/index
    templates/index
    page layout/index
    configuration and settings/index
    multi-site and multi-tenant/index
    language and culture support/index
    security and workflows/index
    working with code/index
    visual design and theming/index

.. _Component-based Architecture: https://en.wikipedia.org/wiki/Component-based_software_engineering