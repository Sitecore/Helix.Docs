Modules
~~~~~~~

The concept of modules in Helix is derived from the concept of
components in Component-based Architecture, which is described in the
book `Agile Software Development by Robert C. Martin <http://www.amazon.com/Software-Development-Principles-Patterns-Practices/dp/0135974445>`__. However, in
the Sitecore context the word “component” might be confusing as it often
refers to an element of a page – a rendering – and therefore a more
generally accepted term *module* is used.

Keep in mind that in Helix, modules are business-centric. This means
that they should relate to business objectives and group together
multiple technology entities that refer to this objective. This
principle goes against many traditional software conventions - such as
the ones dictated by MVC (models, controllers and views) or even
Sitecore (templates, layouts, settings) - that define grouping based on
their type, rather than their business objective.

For this reason, the breakdown and naming of modules can be one of the
most challenging parts of adopting Helix. Developers are often caught by
the type-centric nature of many development tools or methodologies and
forget about the business- or feature-centric nature of modular
architecture. Be careful not to fall in this trap and always keep the
Common Closure Principle in mind.

.. note::

    **Common Closure Principle**

    Classes that change together are packaged together.

    http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod

Never be too afraid or cautious of having modules with very little logic
or modules with just a single technology. There might be management
issues with having a large number of modules, but these challenges can
often be overcome by breaking the implementation into multiple Visual
Studio solutions or with DevOps and automation. The *Single
Responsibility Principle* should always have higher priority than any
management or tools related issues – if you deviate from this, it will
start to devalue your clean architecture and potentially lead to the
technical debt you are trying to avoid.

The name of a module should reflect the business requirement or the use
case of the feature – never the technology or implementation – and
should always be in the domain language. (See :doc:`/principles/architecture-principles/domain-language`).

.. admonition:: Habitat Example

  These are examples of modules in the Habitat example site:

  Feature/Accounts
    This feature handles everything involving user accounts: login,
    registration, xDB integration, user profiles, etc.

  Feature/Navigation
    All elements of navigation on the website are handled by this module.
    This includes: primary and secondary menus, breadcrumbs and link
    lists.

  Feature/Social
    The Social feature enables Twitter feeds on the pages as well as
    allows the editor to add Facebook metadata to the website pages.

  Foundation/Indexing
    This Foundation layer module provides an abstraction layer on the
    search functionality of Sitecore and allows features both to search
    within the data they provide and to integrate into the site-wide
    search.
 
Groups
^^^^^^

Modules can be conceptually grouped together for better maintainability,
readability or structure, for example commerce related features and
foundation modules can be grouped together to distinguish them from the
standard website features. However, this kind of grouping does not
override any of the other conventions. Nor does it introduce new
architectural layers to do things such as enable references across
feature modules. This kind of grouping exists solely for readability or
discoverability purposes.

.. figure:: _static/image3.png

    Figure: Modules, Layers and Groups
