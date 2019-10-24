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

.. admonition:: Sitecore Helix Examples

  These are examples of modules in the Helix Basic Company site:

  Feature/Basic Content
    The business domain of this Feature module is simple content
    components that will be used on pages throughout the site. This includes
    accordions, hero banners, and section headers.

  Feature/Navigation
    The business domain of this Feature module is website
    navigation elements. This includes the site header /
    main navigation, and the site footer.

  Feature/Products
    The business domain of this Feature module is product catalog
    functionality. This includes product listings and detail.

  Foundation/Field Rendering
    The domain of this Foundation module is extensions/helpers and
    customizations related to Sitecore field rendering, which are used
    across multiple Feature modules.

  Foundation/Multisite
    The domain of this Foundation module is providing multi-site
    structure and enhancements for multiple Feature modules.
    This includes atemplate for a site root item.
 
.. admonition:: Habitat Home Commerce Example

  The Commerce version of the Habitat Home Demo includes modules such as:

  Feature/Cart
    All of the elements that allow users to add Sellable Items to a cart.
    This includes renderings used on the website, and also the plugin that
    provides the functionality in the Commerce Engine.

  Feature/Orders
    All of the elements that allow users to place orders and review order history.
    This includes renderings used on the website, and also the plugin that
    provides the functionality in the Commerce Engine.

  Feature/Wish Lists
    All of the elements that allow users to create and manage product wish lists.
    This includes renderings used on the website, and also the plugin that
    provides the functionality in the Commerce Engine.

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
