Front-end technologies
~~~~~~~~~~~~~~~~~~~~~~

Avoid looking at front-end technologies, such as JavaScript, CSS, Sass,
Less etc., as a monolithic technology maintained in a single module, but
rather as another technical part of the business domain modules in
Helix. In other words, front-end technologies and assets such as
JavaScript and CSS are technologies and are related to features and
modules as other technologies.

Technologies with specific purposes, such as, bootstrap, jQuery, sass,
bower, grunt, gulp etc. can be introduced and managed in separate
modules. However, if a technology is used across multiple modules – for
example in a multi-tenant or multi-site implementation – it can be
useful to introduce it in a foundation layer module to make it available
to all modules.

Habitat Example

The front-end technologies used in the Habitat example site are
introduced in the Foundation/Theming module and can therefore be shared
across to all foundation, feature and project layer modules.

The main front-end technologies introduced in Habitat are Bootstrap,
jQuery, Bower and Sass. Furthermore, it uses the Visual Studio Web
Compiler to bundle and minify JavaScript and CSS.

