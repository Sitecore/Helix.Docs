Implementation structure
~~~~~~~~~~~~~~~~~~~~~~~~

A Visual Studio (VS) solution is the manifested grouping of one or more
architectural *modules*, and can represent many different types of
groupings. One VS solution could represent an entire Sitecore 
implementation, with all Project, Foundation and Feature layer modules
managed together, while another Sitecore implementation could span
multiple VS solutions, with one VS solution grouping together all the 
modules which target the Commerce Engine and another VS solution housing the 
modules that purely target the website. You could also have additional VS
solutions per tenant. 

It is important to remember that when adding modules
to split solutions like this you must include all elements of the module 
(for example the website code assembly, Commerce Engine code assembly, unit tests, 
item serialization projects etc.) to still conform with the Common Closure Principle. 

How a customer implementation is structured between Visual Studio
solutions is entirely up the requirements, complexity and logical
architecture of the specific customer implementation. Be aware that a
Visual Studio Solution should logically group together conceptual
modules – not VS projects – and therefore all Visual Studio projects
belonging to a logical module should be managed together in one VS
solution, regardless of how many subsystems it targets.

.. admonition:: Habitat Example

    Internally in Sitecore Habitat is used as the foundation for many
    Sitecore demos, each focused on demoing specific business scenarios,
    such lead nurturing, campaign management and portals, and how these are
    handled by the Sitecore products range, such as the Sitecore Experience
    Platform, Sitecore Print Experience Manager or Sitecore Commerce. The
    Habitat demo framework is therefore maintained within its own Visual
    Studio solution (and version control repository) and each demo scenario
    – with any specific scenario features - is maintained in its own
    solution.

    .. figure:: _static/image12.png
        :scale: 75%

        Figure: Habitat Visual Studio Solution