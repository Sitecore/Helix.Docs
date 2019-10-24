Layers
~~~~~~

The layer concept in Helix supports the architecture by making the
dependency flow completely clear everywhere in the solution, in
Sitecore, in Visual Studio and even in the file system. Furthermore, the
layers provide a structure that is extremely suitable for creating and
maintaining solutions of any size and steers both new and experienced
developers to producing more maintenance-friendly and clean code.

Note that the layers in Modular Architecture are not equivalent to the
layers seen in 3/n-tiers architecture even though they bear resemblance
in terms of dependency direction.

Even though layers are a conceptual construct in the architecture,
layers are physically described in the implementation by folders in the
filesystem, Visual Studio and Sitecore, along with namespaces in code and
layers defines in which direction modules can depend on other modules.

Layers helps control the direction of dependencies – the importance of
which is described by the Stable Dependencies Principle or SDP, which is
one of the cornerstone principles in Modular Architecture:

.. note::

    **Stable Dependency Principle**

    The dependencies between packages should be in the direction of the
    stability of the packages. A package should only depend upon packages
    that are more stable than it is.

    http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod

This principle tells us that a module should only depend on a module
that is more stable than itself. Code stability is a way of expressing
how likely it is that the code in a module and its interfaces will
change. Stability is important since if you depend on a module that
changes, then these changes could affect all the dependent modules as
well.

If dependencies are not controlled, then you can end up in a situation
where a change will unintentionally affect seemingly unrelated parts of
the solution – in effect, an unstable codebase - and an unstable
code-base will make your solution hard or impossible to maintain over
time.

Sitecore Helix defines three layers: Project,
Feature and Foundation. Each layer has a very clearly defined purpose.
In order to structure your Sitecore implementation properly, it is
important to understand the principles behind these layers.

.. figure:: _static/image7.png

    Figure: Layers in Sitecore Helix

Practically speaking, the three layers are typically defined in Visual Studio as
Solution folders, in the file system and directories and in Sitecore as
corresponding content type folders.

These typical Sitecore locations contain layer folders out of the box:

* ``master:/sitecore/templates/[Project|Feature|Foundation]``
* ``master:/sitecore/templates/branches/[Project|Feature|Foundation]``
* ``master:/sitecore/layout/renderings/[Project|Feature|Foundation]``
* ``master:/sitecore/layout/layouts/[Project|Feature|Foundation]``
* ``master:/sitecore/layout/placeholder settings/[Project|Feature|Foundation]``

Depending on your needs, you may want to create folders in other locations
to indicate the layer/source of the items contained there:

* ``master:/sitecore/system/Settings/[Project|Feature|Foundation]``
* ``master:/sitecore/layout/models/[Project|Feature|Foundation]``
* ``core:/sitecore/templates/[Project|Feature|Foundation]``

.. admonition:: Sitecore Helix Examples

    The Helix Examples use the built-in Sitecore layer folders for organizing
    items, and serialize items from them using either Sitecore TDS or Unicorn.
    (See :doc:`/principles/sitecore-items/development`)

    In Visual Studio, the layers are defined as solution folders:

    .. figure:: _static/basic-company-solution-folders.png

        Figure: Layer Solution Folders in Visual Studio

    On disk, in most solutions the layers are defined as folders under /src:

    .. figure:: _static/basic-company-filesystem-folders.png

        Figure: Layer folders under /src on disk

    The builtin Sitecore layer folders under Templates and Layouts:

    .. figure:: _static/builtin-sitecore-template-folders.png

        Figure: Layer folders under /sitecore/templates in Sitecore

    .. figure:: _static/builtin-sitecore-layout-folders.png

        Figure: Layer folders under /sitecore/layout/renderings in
        Sitecore

Project Layer
^^^^^^^^^^^^^

The Project layer provides the context of the solution. This means the
actual cohesive website or channel output from the implementation, such
as the page types, layout and graphical design. It is on this layer that
all the features of the solution are stitched together into a cohesive
solution that fits the requirements. Thus it is often referred to as the
*compositional* layer.

Each time there is a change in a feature, a new one is added or one is
removed, then this layer will typically change. The layer also brings
together the concrete graphical design of the solution, which means that
in terms of the \ *Stable Dependencies Principle*, the modules in this
layer are \ *unstable*. The most unstable modules in your solution and
thus, remembering the Stable Dependency Principle, should have the
fewest dependencies on it.

The Project layer is typically small and contains few modules, often
determined by the number of tenants in the solution and their needs (see
:doc:`/principles/multi-site/index`).

Typically, in a single tenant solution there will only be a single
module, namely the specific website or requirements that fits the needs
of the tenant, and this will contain little or no pre-compiled code but
instead consist of mark-up, styling, layout and templates of
the item types in Sitecore which the editors can create (see :doc:`/principles/templates/template-types`).

If working with Sitecore Experience Commerce, the Project layer is where
you will find the Commerce Engine application project. It will then assemble
all of its required functionality through references to modules in the lower
layers.

Project layer modules can also be used to expose one feature’s
functionality to another (that is, *compose* features together),
without having to directly make one Feature
module dependant on another, for example through the inversion of
control or pipeline patterns. However, be careful not to implement
actual feature-specific business logic in the Project layer in this
process.

Feature Layer
^^^^^^^^^^^^^

The *Feature* layer contains concrete features of the solution as
understood by the business owners and editors of the solution, for
example news, articles, promotions, website search, product listings,
shopping cart functionality, etc.

The features are expressed as seen in the business domain of the
solution and not by technology, which means that the responsibility of a
Feature layer module is defined by the intent of the module as seen by a
business user and not by the underlying technology. Therefore the
module’s responsibility and naming should never be decided by
specific technologies but rather by the module’s business value or
business responsibility.

Each Feature layer module has to strictly conform to the Common Closure
Principle.

.. note::

    **Common Closure Principle**

    Classes that change together are packaged together.

    http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod

This principle ensures that changes in one feature do not cause changes
anywhere else, and that features can be added, modified and removed
without impacting other features. For example, in a Sitecore context, it
is important that all Sitecore items – such as the interface templates
and rendering items – are managed, versioned and packaged with the views
and code files of the feature. This can be done by serialization (see
:doc:`/principles/sitecore-items/development`). Likewise, changes to configuration files (web.config or Sitecore
.config include files) must be managed as part of the feature module
(see :doc:`/principles/configuration/index`). The same applies when working
with Sitecore Experience Commerce, if you have a module whose functionality 
spans both the website and the Commerce Engine, then all of it must also
be managed together as part of a single feature module.

A strict awareness of dependencies within the Feature layer is very
important. One Feature module must \ *never* depend on another Feature
module as this certainly makes you lose many of the benefits that that
Modular Architecture provides, such as the overall flexibility and
reliability of the solution. This principle can sometimes be challenging
as functionality in some features often rely on data from other features
and you will have to rely on architectural patterns to get around this.
For example, website search will rely on data from other modules as part
of the indexing and search results rendering. To get around this a
typical approach would be to add the concept of indexing and rendering
search results to a foundation level module (see :doc:`/principles/architecture-principles/layers`) which the
Search feature module then utilises. Other modules can then offer their
content to search by plug into the indexing and rendering functionality
in the Foundation module – through for example an inversion of control
pattern.

Note that although several modules in the Feature layer can be grouped
together semantically (see :doc:`/principles/architecture-principles/modules`) 
this only suggests a conceptual coherence between modules – not in any 
way a technical dependency.

Foundation Layer
^^^^^^^^^^^^^^^^

The lowest level layer in Helix is the Foundation layer, which as the
name suggests forms the foundation of your solution. When a change
occurs in one of these modules it can impact many other modules in the
solution. This mean that these modules should be the **most stable** in your
solution in terms of the \ *Stable Dependencies Principle*.

Conceptually, it is helpful to think of all the frameworks and software
you rely on in your solution as foundation modules. This includes the
Sitecore platform, .NET and other technology frameworks such as
Bootstrap, Foundation, jQuery etc. In the context of your
implementation, these are typically very stable modules but when they do
change, it often requires a more rigorous testing process and
potentially a lot of changes to your Feature and Project layer modules.
By controlling dependencies even to these frameworks, you can greatly
decrease the time needed on technology upgrades and increase the
stability of the solution.

.. admonition:: Habitat Example

    In the Habitat example, the Sitecore.Foundation.Theming module
    implements most of the CSS stylesheets for the Habitat website. This
    might be seen as a very Project layer specific functionality but on
    close inspection, you will notice that the CSS of the module merely
    pulls in, wraps and extends the standard Bootstrap framework, and thus
    exposes an implementation specific design framework for all Feature
    modules to use. Any website or page specific CSS additions can be added
    in the Project layer modules – just as you would if you are styling on
    top of standard Bootstrap, Foundation or other frontend frameworks.

    CSS is the single most common cause for implicit dependencies between
    modules, so be sure to have a strategy for how to deal with the
    graphical design implementation in your Helix compliant solution (see
    :doc:`/principles/theming/index`).

Typically, modules in the Foundation layer are either business-logic
specific extensions on the technology frameworks used in the
implementation, or shared functionality between feature modules that is
abstracted out into separate frameworks.

Typically, modules in the Foundation layer are conceptually abstract and
do not contain presentation in the form of renderings or views - as
these are to be considered concrete. Some framework modules might still
contain mark-up in code though, examples being precompiled web-controls
and html helper functions, but in order to control dependencies, any
Feature or Project specific knowledge should be passed as parameters
from the depending module.

.. admonition:: Habitat Example

    The Sitecore.Foundation.Indexing module in Habitat allows all Feature
    modules, and their content types, to participate in the search
    functionality of the solution. This means that a new Feature layer
    module can be exposed through the search pages of the websites by simply
    implementing the interface or configuration defined in the Foundation
    layer module – and without the Sitecore.Feature.Search module knowing
    anything about the new module or its content.

Unlike the Feature layer, there is no strict convention on dependencies
between modules in the Foundation layer. This means that one Foundation
layer module can depend on another Foundation layer module in the
solution – as long as they rely on the basic principles on component
architecture such as the Acyclic Dependencies Principle and the Stable
Abstractions Principle:

.. note::

    **Acyclic Dependencies Principle**

    The dependency graph of packages must have no cycles.

    http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod

.. note::

    **Stable Abstractions Principle**

    Abstractness increases with stability.

    http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod


Other Layers
^^^^^^^^^^^^

Increasingly it's common to include a Helix layer which defines infrastructure
(e.g. Azure Resource Manager templates) or that handle consolidating deployments
to a particular service in your Sitecore environment. Names for this layer in the
community include *Infrastructure*, *Environment*, and *Deployment*. At this time
there is no recommended standard for naming this layer.

.. admonition:: Sitecore Helix Examples

    Some of the Sitecore Helix Examples use a small *Environment* layer for projects
    which handle deployment to the main Sitecore Website/Platform service, either
    using Sitecore TDS or Helix Publishing Pipeline.