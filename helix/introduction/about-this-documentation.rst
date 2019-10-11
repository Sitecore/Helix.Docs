About this Documentation
--------------------------

Prerequisites
^^^^^^^^^^^^^
Before you start venturing into a complete understanding of Sitecore Helix – and
particularly the reasoning behind it – it is a good idea to have
some experience in developing in ASP.NET and in Sitecore. Although
the example sites work well as end-to-end examples of
Sitecore implementations (and as such are a good supplement to the
Sitecore developer training), the added intricacies of the conventions
can add to an increased learning curve of Sitecore.

The Scope of Sitecore Helix
^^^^^^^^^^^^^^^^^^^^^^^^^^^
Sitecore Helix does not define conventions or best practices for
all aspects of ASP.NET or Sitecore, but rather focuses on the macro
**solution architecture** of Sitecore development. This means that you
find that some of aspects of Sitecore development such
as object-oriented architecture and ASP.NET MVC conventions are not
mentioned in this document. In other words, despite the conventions and
recommended practices in this document, Sitecore Helix still gives you great
freedom in your choice of tools and general development practices.

Focus on Sitecore MVC
^^^^^^^^^^^^^^^^^^^^^
Although the overall Sitecore Helix conventions and principles can be applied to
Sitecore JavaScript Services (JSS), SXA, or even Sitecore with ASP.NET Web Forms (!),
this documentation is focused on the use of ASP.NET MVC with Sitecore. Future
enhancements to this documentation will detail the application of Sitecore
Helix practices to JSS, and how practices might differ slightly when
building with SXA.

Sitecore Helix is not a Rulebook
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Although Sitecore Helix is a set of recommended practices and conventions from
Sitecore itself, it is not a set of rules. Development teams, businesses
and requirements will differ for each Sitecore solution. Although there are great benefits to be
gained from aligning to a defined set of conventions, there is also a
need for pragmatism. The advice is to generally read all development
conventions, patterns and principles – including Sitecore Helix – with a critical
mindset and apply them in the context of your own business, team and
solution. However care must be taken when deviating for the sake of short-term
velocity -- always keep in mind the core design principles upon which Sitecore
Helix is based, with the goals of :doc:`maintainability and long-term value <./why-sitecore-helix>`
for your customer.

The Continuing Evolution of Sitecore Helix
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Sitecore Helix is a set of conventions formed through the collective experiences
of Sitecore developers. The conventions are formed through open discussions,
but are formalized by Sitecore. As the Sitecore development technology stack
will change over time, so will the conventions be adapted and updated to
support these changes. The underlying reasoning for Sitecore Helix (the why)
will remain the same, even though the conventions (the how) will change to
reflect the current world.

Your experience about what works, and what does not, when architecting
Sitecore solutions is invaluable to the continuing refinement of these
practices. We welcome feedback and contributions to Sitecore Helix via the
`Helix Docs GitHub Repository <https://github.com/Sitecore/Helix.Docs>`__.