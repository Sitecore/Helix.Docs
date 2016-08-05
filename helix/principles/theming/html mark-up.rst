HTML mark-up
~~~~~~~~~~~~

In a web solution, the relationship between mark-up and theming is one
of the biggest sources of dependencies. If there is no strategy for
managing HTML mark-up in a decoupled manner, the whole implementation
can easily become very monolithic, and flexibility and productivity
become stifled.

Most renderings, and therefore the HTML mark-up, in a Helix
implementation will reside in the feature layer. On the other side, the
business requirements are fulfilled in the project layer, by combining
the features into the user experience. Therefore, in a multi-tenant or
multi-site scenario, the challenge is that features need to address
multiple business requirements – or simply different visual designs.

In other words, in a multi-tenant scenario some assets will always be
shared between tenants (see 2.8) and when following the Helix
conventions, the mark-up is very often one of these assets.

In a single tenant scenario, this is not such a big issue, as features
can be built with a single business in mind. Features can be changed and
adapted as the requirements changes.

A recommended approach to the shared mark-up challenge is to align your
front-end technologies with the Helix principles and split the
implementation of the Visual Design across the layers. In your
foundation layer, you place the principal front-end framework or
frameworks on which you are basing the implementation. These are the
frameworks that define how to structure the HTML mark-up in the
features. This includes technologies like Bootstrap, Foundation, 960
Grid System, and jQuery. In reality, the foundation layer module will
likely contain a multitude of frameworks and utilities – perhaps
extended with custom mark-up - which together form the conceptual base
that feature developers need to follow. It can even be a custom defined
mark-up strategy that is clearly known to feature developer.

The point is that by defining a mark-up strategy in the foundation
layer, the feature modules can follow this strategy and know that they
are adhering to the implementation conventions.

.. admonition:: Habitat Example

    The module Foundation/Theming establishes the mark-up framework for the
    Habitat example site. The module uses bower to bring in a number of
    external frameworks based on Bootstrap and jQuery.

    .. code-block:: json
    
        {
            "name": "sitecorehabitattheme",
            "private": true,
            "dependencies": {
                "bootstrap-sass": "~3.3.5",
                "bootstrap-block-grid": "~1.1.2",
                "modernizr": "~2.8.3",
                "hover": "Hover#~2.0.2",
                "animate.css": "~3.5.0",
                "wow": "wowjs#~1.1.2",
                "shufflejs": "~3.1.1",
                "responsive-bootstrap-toolkit": "responsive-toolkit#~2.5.1",
                "OwlCarousel": "~1.3.2",
                "jquery": "~2.2.0",
                "font-awesome": "4.4.0",
                "ekko-lightbox": "~4.0.1",
                "ace-builds": "~1.2.2",
                "imagesloaded": "~4.1.0"
            },
            "overrides": {
                "bootstrap-sass": {
                "main": [
                    "assets/stylesheets/_bootstrap.scss",
                    "assets/fonts/bootstrap/*",
                    "assets/javascripts/bootstrap.js"
                ]
                },
                "font-awesome": {
                "main": [
                    "fonts/*"
                ]
                },
                "OwlCarousel": {
                "main": [
                    "owl-carousel/owl.carousel.min.js",
                    "owl-carousel/owl.carousel.css"
                ]
                }
            },
            "devDependencies": {},
            "resolutions": {
                "jquery": "~2"
            }
        }
