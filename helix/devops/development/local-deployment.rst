Local deployment
~~~~~~~~~~~~~~~~

One of the most frequently asked questions when working with Sitecore is
whether to develop locally inside the web root or outside. Although the
general recommendation is to work outside the web root, you should
consider the implications.

There are two major aspects which should lead to choosing one or the
other:

Firstly, it is very important to be able to separate the implementation
specific files and changes from the standard frameworks and files. The
importance of this separation cannot be overstated, as it will help in
many aspects in the long run, such as general development,
troubleshooting, upgrades and more. This separation is easier if the
implementation specific files are physically separated from the files in
the standard frameworks etc.

Generally, if tasks that are repeated frequently become taxing, they
will be circumvented – and this will lead to inconsistencies in the
processes and ultimately inconsistencies in quality. Therefore,
secondly, the ease of development is important. Working outside the web
root will lead to an additional step in the development process –
deploying the change to the running environment – and given the
frequency of this task it is imperative that this is easy. Tools and
automated scripts can help this to become almost transparent for the
developer.

.. admonition:: Sitecore Helix Examples - TDS

    The TDS version of Helix Basic Company uses the built-in
    `capability of TDS <http://hedgehogdevelopment.github.io/tds/chapter4.html>`__
    to deploy files to the web root on build. To avoid the need for a
    TDS project for modules which do not have associated items, a single
    TDS project is used to build and deploy files for all solution modules.

        .. figure:: _static/basic-company-tds-deployment-sources.png

            Figure: Source web projects for file deployment

        .. figure:: _static/basic-company-tds-deployment-build.png

            Figure: File deployment location, originating in the ``TdsGlobal.config``

    You can also enable the *Content File Sync* feature of TDS to automatically
    deploy changes to any content files, such as Razor views and CSS/JS files.

        .. figure:: _static/tds-content-file-sync.png

            Figure: Configuring *Content File Sync* in *Tools > Options > TDS Options*.

.. admonition:: Sitecore Helix Examples - Unicorn

    The Unicorn version of the Helix Basic Company uses the
    `Helix Publishing Pipeline (HPP) <https://github.com/richardszalay/helix-publishing-pipeline>`__
    open source tooling to enable publishing of the entire Helix solution as a
    single unit, and to enable auto-publish to the web root on build.

        .. figure:: _static/basic-company-unicorn-hpp-reference.png

            Figure: Helix Publishing Pipeline reference in Helix Basic Company - Unicorn

    For information on configuring auto-publishing with HPP, see its
    `documentation <https://github.com/richardszalay/helix-publishing-pipeline>`__.