Examples of Sitecore Helix
==========================

While reading this documentation will help you understand the
practices and conventions recommended by Sitecore Helix, having
real code examples as a reference is very helpful when envisioning
how you would apply them to your own solution.

.. note::

    **These Examples are not "Starter Kits"**
    
    While all of the examples below are intended to demonstrate good
    application of Helix practices, you should not utilize any as a
    starter kit for your implementation. You can follow patterns from
    these examples, and even copy code from them as needed, but they
    should not be copied "wholesale" when starting a new implementation.
    Doing so will add technical debt to your solution since the examples
    are made for an imaginary solution context.

    There's one notable exception to this -- `SXA <#sxa>`__ provides many
    components and platform extensions to help speed your Sitecore implementation
    while following Helix solution architecture.

Helix Examples
^^^^^^^^^^^^^^

The `Sitecore Helix Examples <https://github.com/Sitecore/Helix.Examples>`__
are a new repository of example solutions meant to demonstrate Helix practices
for various types of sites and tooling. You will see these examples referenced
throughout this documentation.

These examples are a work in progress and are intended to replace the original
Sitecore Habitat.

Sitecore Habitat
^^^^^^^^^^^^^^^^

In March 2016, Sitecore released `Habitat <https://github.com/Sitecore/Habitat>`__
and did something it had never done before -- released not just a demo site,
but one that reflected a solution architecture which the community should adopt.
Later that year, the solution architecture of Habitat was codified into the
Sitecore Helix practices. Habitat continued to be used as a demo and training
framework as well.

This "original" Habitat site had dual purposes as a developer example for Helix,
and a marketing demo site. You will still see references to Habitat throughout this
documentation, but the new Helix Examples will eventually replace those references.

Habitat Home has fully replaced Habitat as a demo platform.

Habitat Home
^^^^^^^^^^^^

`Habitat Home <https://github.com/Sitecore/Sitecore.HabitatHome.Platform>`__,
`Habitat Home Corporate <https://github.com/Sitecore/Sitecore.HabitatHome.Corporate>`__,
`Habitat Home Commerce <https://github.com/Sitecore/Sitecore.HabitatHome.Commerce>`__,
and `Habitat Home Omni <https://github.com/Sitecore/Sitecore.HabitatHome.Omni>`__
are all part of the Habitat Home demo framework. While still demonstrating
Sitecore Helix solution architecture, Habitat Home's primary intent is to demonstrate
Sitecore's full product capabilities in a realistic website. These should not be
confused with the "original" Sitecore Habitat.

SXA
^^^

The `Sitecore Experience Accelerator <https://doc.sitecore.com/users/sxa/19/sitecore-experience-accelerator/en/introducing-sitecore-experience-accelerator.html>`__
is a Sitecore solution accelerator which implements Helix practices.
It also contains a number of extensions to the Sitecore platform which
can make it easier to implement a modular architecture.