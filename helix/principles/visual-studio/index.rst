Visual Studio
-------------

A single Sitecore implementation can end up consisting of a large number
of modules and this can lead to technical management issues.

Good rules of thumb are that your architecture should always have higher
priority than any tools or technology related issues and only with
sincere thought should you deviate from your conventions. Deviations or
exceptions will most often lead to technical debt and instability or
lack of flexibility. Management and development problems, such as slow
development environments or complex deployment procedure etc. –
especially with the pressure and stress of performance and deliveries -
will lead to deviations from architectural principles and therefore to
technical debt.

In large scale implementations, it is therefore often helpful to break
down your implementation into multiple Visual Studio Solutions – each
with a logical grouping, for example independent Foundation modules,
cross-project or reusable modules or feature groupings such as Basic
Website or modules that target a specific subsystem for example the 
Commerce Engine.

In this context, though, it is important to stress that each
architectural module, for example the Navigation Feature module, most
often will consists of a number of different technologies and tools used
for the feature and can therefore be represented by different Visual
Studio projects of different types (for example the website code assembly,
Commerce Engine code assembly, unit tests, item serialization projects etc.)
– but which should always be managed together in one Visual Studio solution.
Avoid grouping Visual Studio projects together by technology, type or subsystem.

.. toctree::
    :caption: Topics 
    :titlesonly:

    structure
    solutions
    projects
