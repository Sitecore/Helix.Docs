Datasource settings
~~~~~~~~~~~~~~~~~~~

Renderings are defined in the feature layer, but they reference elements
in the project layer, such as Page Type Templates, Datasource Templates
and locations within the content tree. These references can result in
dependencies that go the wrong way, or dependencies that cross features.

When dealing with datasource locations and datasource templates,
Sitecore offers limited help in overcoming these dependencies – and
therefore, to preserve the stringency of the architecture, you will have
to do introduce custom logic to overcome this limitation, typically by
introducing a Foundation module (See 2.6.3.2).

Datasource Template
^^^^^^^^^^^^^^^^^^^

The Datasource Template field in Editing Options section of the
rendering’s item has two functions: it controls which types of items are
allowed as datasource items for the rendering, and it designates the
template used for new items created through the datasource dialog.

The Datasource Template field supports template inheritance. This means
that you can select an item based on the specified template, or an item
based on a template that derives from the specified template. This is
very useful since a rendering in a Feature layer module most often
relies on an Interface Template – which should be defined in the same
Feature layer module (See 2.5.3.1). The problem is, however, that
Sitecore will use the specified template as the template for new items
created through the Select the Associated Content dialog. This means
that even though Sitecore supports it, you should not specify an
Interface Template in the Datasource Template field, as you will end up
with pages or datasource items based on this template – which ends up
violating the architecture and create dependencies (see 2.5.3).

.. figure:: _static/image32.png

    Figure: Creating new content in the datasource dialog

Unless you plan to disable the opportunity to create new content in the
Associated Content dialog or simply ignore the architectural principles
and specify a Page Type or Datasource Template (see 2.5.3) in the
Datasource Template field, there is no easy solution for this conundrum.
However, Sitecore does allow you to hook in to a pipeline to resolve the
datasource template in context and thus be smarter around this. See the
Habitat Example below.

Datasource Locations
^^^^^^^^^^^^^^^^^^^^

The Datasource Location field in the Editor Options section of the
rendering item allows you to specify one or more content locations from
where the editors can select content for the rendering. More locations
can be specified using a piped *query:* syntax.

The immediate challenge is that locations from which the renderings draw
their content are often defined in the Project layer – by the sites
themselves – and thus specifying the Datasource Location of the
rendering will create a dependency from a feature rendering to a Project
layer module. Furthermore, the challenges with specifying datasource
locations can vary according to the complexity of your content
architecture, for example if you are building a multi-site or even a
multi-tenant solution where a rendering will have different locations
depending of the context in which it is used.

A simple solution to this challenge is for the features themselves to
own the datasource location itself. For example, a feature Teasers
module could point to /sitecore/content/teasers as the datasource
location for all its renderings, thereby forcing all sites to have a
shared teasers repository. This will work perfectly fine for a simple
single site/single tenant solution. But in other scenarios this might be
challenged by the content governance model. Habitat provides an example.

.. admonition:: Habitat Example

    The Habitat example site is a true multi-tenant and multi-site solution.
    The Habitat project layer module, as well as our internally built
    product demonstrations, represent tenants (and sites) that define their
    own page types and datasource locations (see 2.8).

    In order to accommodate this scenario, the datasource location and
    template resolution have been extended in the Habitat project. This
    means that it is also possible to define datasource templates and
    locations for each site, in addition to on the rendering itself. This is
    done through an extension of the getRenderingDatasource pipeline and the
    addition of a site: prefix to the Datasource Location field. In short:
    if the Datasource Location field contains a site: prefix, the pipeline
    extension will attempt to lookup the datasource location and template in
    a site specific list. This functionality is implemented in the
    Foundation.Multisite module.

    .. figure:: _static/image33.png

        Figure: Site specific datasource location for a FAQ rendering

    .. figure:: _static/image34.png

        Figure: The FAQ site specific datasource settings for Habitat