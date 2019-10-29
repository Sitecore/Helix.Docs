Principles of Package Design
====================================================

Helix is based on Robert Martin's "Principles of Package and Component Design" 
(Chapter 28,  *Agile Principles, Patterns, and Practices in C#*, Prentice Hall, 2006). 
These six principles set forth a conceptual framework for managing package boundaries ("cohesion") and interrelationships ("coupling").
The following discussion presents these principles, provides a brief synopsis of how Martin presents them, and shows how they guide
specific Helix practices.  

A note on terms: Martin has written about these principles in a number of places, and sometimes uses the term "package" and
sometimes "component." For consistency, we will use "package" throughout this appendix when referring to Martin's writing,
and "module" when referring to the Helix unit.

The Principles of Package Cohesion
------------------------------------
Martin's first three principles deal with what goes into a package, and what stays out.

The Reuse/Release Equivalency Principle (REP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    The granule of reuse is the granule of release.
 
In Martin's discussion, this principle states that code that is meant to 
be reused must be released according to a defined, predictable process, 
and that the scope of the released package is governed by how it will 
be put to use. He makes the point that one would not expect classes 
that are not intended to be reused to be packaged with ones that are, and
that the package should be reusable by the same audience: "Many people who would 
like to reuse a container class library would have no interest in a financial
framework."

In Helix, this principle underpins the practice of grouping modules by 
recognizable business needs, such as navigation or promotion display. Even 
if such a module is not intended for reuse, it is intended for a specific
audience, such as developers working on navigation. This principle lets them
treat a module as a well-defined space in which only classes relevant to their
development effort are present, limiting distraction, complexity and the 
potential for unintended side effects. In Helix terms, this principle could
be restated as, "The granule of business purpose is the granule of module size,"
or more simply, "A module should serve a single business audience."

The Common Reuse Principle (CRP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    The classes in a package are reused together. If you reuse one of the
    classes in a package, you reuse them all.

In Martin's writing, this principle establishes that there are close relationships
between the classes in a package: "classes that are not bound to each other with 
class relationships should not be in the same package."  We see this principle at work
in the treatment of items and templates in Helix. By defining items through the
composition of interface templates, Helix hides from the module the fields the 
module does not use. Developers familiar with Martin's SOLID principles will
recognize this as an application of the Interface Segregation Principle: "Clients 
should not be forced to depend on methods they do not use" (Martin, ch. 12).

By using interface templates, and limiting item visibility to these fields, Helix 
keeps out of the view of the module functionality of other modules, as well as all the
fields Sitecore uses to manage items (icon, publishing settings, workflow, 
security). This is why even with Data Source packages, Helix recommends a separation
between the interface template, owned by the module, and the Data Source template, 
owned by the Project layer (see `Template types`_).

.. _Template types: principles/templates/template-types.html
 
The Common Closure Principle (CCP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    The classes in a package should be closed together against the same 
    kinds of changes. A change that affects a package affects all the 
    classes in that package and no other packages.

This principle seeks to limit the impact of changes to one or a small set of 
modules, so that changes do not ripple across all the packages of a system. 
This principle motivates the Helix practice of grouping different types of elements
(templates, renderings, views, controllers) that collaborate to produce a feature.
In this way, a change to that feature will land entirely within the scope of one
module. For example, imagine adding a new behavior to a navigation package, 
with a new field added to an interface template, new code added to a model repository,
and new markup added to CSHTML. Although these are different technologies, they are 
bound in one Helix module, and thus the impact of the modification is limited to 
that module. 

Principles of Package Coupling
--------------------------------
The last three principles define how packages (i.e. modules in Helix) should interact with one another.

The Acyclic Dependencies Principle (ADP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  
  No cycles will be accepted in the dependency graph.

This principle guards against circular references and dependencies, so that the direction of 
dependencies flow in one direction.  The reason for this precaution is that if a circular 
dependency is allowed to stay, then a change to the offending package will mean that every other 
package will need to be validated,  undoing the benefits of modularization.  
It is important to note that these cycles can arise in 
numerous ways: project references, which Visual Studio will guard against, but also through 
more subtle means, such as type references in content or markup. This principle inspires Helix's attention
to managing relationships through layers, and for taking proactive steps to guard against implicit
dependencies between modules. For example, Helix requires that fields always be addressed by Field ID 
rather than field name, as by using field names a module takes on an implicit dependencies on 
every other module in the system not to have overlapping field names. (See `References from code`_)

.. _References from Code: principles/templates/references.html

The Stable Dependencies Principle (SDP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  
  Code should depend in the direction of stability

Packages that change rarely should not depend on modules that change often, as this reduces the benefit of 
modularizing stable code. Martin proposes a numerical formula for assessing module stability in terms of class
dependencies. In Helix, this mechanism is replaced by two guard rails: all features should live in "Feature"-layer 
modules, and no Feature layer module may depend on another. In this way, Helix prevents any business sensitive
and thus highly dynamic module from depending on another highly dynamic module. This prevents any solution built with this 
architecture from falling into the conundrum that a business facing feature cannot be easily changed as it provides 
functionality to another, and apparently unrelated, one.

The Stable Abstractions Principle (SAP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  A package should be as abstract as it is stable

Robert Martin considers a package's abstractness to be measurable by the percentage of abstract classes and interfaces compared to concrete classes. Abstract classes provide the capability of being extended without modification to meet dynamic business needs, (see the "Open/Closed Principle," ch. 9).  
In Helix, this principle is observed by keeping the Foundation layer "conceptually abstract": free of markup, and not directly
servicing business audiences, but rather enabling the Feature modules that do so.  In addition, abstract classes and interfaces 
in the Foundation layer can provide a mechanism for one Feature to provide services to other Features: an interface in 
the Foundation layer provides a stable contract between multiple features (see Adam Coates's article, `Dependencies On Another Feature`_). 
Finally, the Sitecore developer can make use of pipeline definitions to define Foundation-layer abstract contracts, 
allowing Feature modules to subscribe via pipeline processors, as Martin Davies has shown (`Helix Code Smells`_).  

.. _Dependencies On Another Feature: https://blog.coates.dk/2017/04/18/sitecore-helix-modules-that-need-to-reference-another-module-in-the-same-layer-part-1/
.. _Helix Code Smells: http://www.bekagool.com/news-and-insights/code-smells/
