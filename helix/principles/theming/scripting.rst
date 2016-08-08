Scripting
~~~~~~~~~

Although front-end scripting technologies such as JavaScript are often
associated with visual design and CSS, they are starting to serve more
purposes in website implementations. And even though Sitecore is
predominantly ASP.NET and C# driven, JavaScript and its associated
frameworks are taking an increasingly important role in the actual
business logic of the application.

Scripting technologies are typically related to the different layers,
depending on what purpose they serve:

-  Framework technologies (such as jQuery, Angular.js, Backbone.js,
   Require.js and so on) are typically Foundation layer modules that
   provide a standardized API or framework for feature modules to
   leverage. These should therefore be introduced into the
   implementation in a Foundation layer module.
-  Functionality-specific scripts, i.e. presentation or business logic
   which enables parts of a feature to function belongs in the Feature
   layer. For example, scripts that enable menus to open or close,
   results to lazy-load on scrolling of the page and so on, belong in
   the module that has the related content or views.
-  The last group is presentation-related scripting, which relates to
   the way a page or parts of a page presents itself. This includes
   scripts that relate to the holistic visual design of the page and its
   CSS, and scripts that often require knowledge of the DOM of the page
   in order to function. These types of scripts belong with the page or
   site specific design implementation in the Project layer (see :doc:`/principles/theming/scripting`)

In order to support this type of separation, the implementation will
need a mechanism for features to register scripts to be loaded – either
solution-wide or on the pages where they are used. Since Sitecore does
not natively provide such a mechanism, your will need to choose the
approach and provide this in the foundation layer. This can be
accomplished by using either a standard framework, such as require.js,
or custom logic implemented in a foundation layer module.

.. admonition:: Habitat Example

    The Habitat example site provides an Assets module in the Foundation
    layer that allows modules to register script or styling files through
    .config files, which is subsequently loaded on the website. Files and
    assets can also be bound to specific renderings and dynamically loaded
    on pages which use those renderings.

    Although the Habitat example shows a highly pluggable and
    Sitecore-centric approach to assets, it does not include aspects such as
    minification and other optimization techniques. These can however be
    integrated using standard technologies such as require.js.