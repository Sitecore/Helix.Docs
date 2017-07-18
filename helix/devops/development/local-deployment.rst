Local deployment
~~~~~~~~~~~~~~~~

One of the most frequently asked questions when working with Sitecore is
whether to develop locally inside the web root or outside. Although the
general recommendation is to work outside the web root, a general
qualification is needed.

There are two major aspects which should lead to choosing one or the
other:

Firstly, it is very important to be able to separate the implementation
specific files and changes from the standard frameworks and files. The
importance of this separation cannot be overstated, as it will help in
many aspects in the long run, such as general development,
troubleshooting, upgrades and more. This separation is easier if the
implementation specific files are physically separated from the files in
the standard frameworks etc. On the other hand, tools and processes
might cater for this separation, even when working inside the web root.

Generally, if tasks that are repeated frequently become taxing, they
will be circumvented – and this will lead to inconsistencies in the
processes and ultimately inconsistencies in quality. Therefore,
secondly, the ease of development is important. Working outside the web
root will lead to an additional step in the development process –
deploying the change to the running environment – and given the
frequency of this task it is imperative that this is easy. Tools and
automated scripts can help this to become almost transparent for the
developer.

.. admonition:: Habitat Example

    The build system in Habitat includes a number of tasks that will watch
    files of a given type and deploy these automatically to the local
    instance. This includes changes to assemblies after a build, changes to
    .cshtml view files and changes to .css files. Habitat also includes
    tasks for deploying all files of a given type.

        .. figure:: _static/image43.png

            Figure: All gulp tasks as available through the Visual Studio
            Task Runner
