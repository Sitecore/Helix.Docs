Services
-------------

As Sitecore moves to a services-based architecture, there are
more and more services being introduced that you could have to push
code & configuration to. For example the Sitecore Experience Commerce 
Engine Roles, the Commerce Business Tools, Identity Server and the 
different XConnect instances.

The most important thing to remember with these services is that
you should still abide by the Common Closure Principal - classes 
that change together are packaged together. This means that you 
shouldn't, for example, group all of your Commerce functionality
together as then you're reverting to grouping by Type instead of by
Functionality.

.. toctree::
    :caption: Topics 
    :titlesonly:

    commerce