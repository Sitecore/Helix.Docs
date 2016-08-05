Managing .config files
~~~~~~~~~~~~~~~~~~~~~~

Managing .config files for even a simple Sitecore project can, over
time, become a very complex and time consuming task, and if done wrongly
it can be a source of many problems such as performance, consistent
testing, instability and waste of resources.

The key to long-lasting good configuration management is isolating not
only the implementation specific changes and additions from the standard
Sitecore and .NET configuration, but also keeping any changes and
additions to configuration together with the business logic which needs
it. The first makes it possible to easily identify changes – making
upgrades much easier – and the latter makes it easy to identify the
reason for changes – making issue resolution and implementation changes
stress-free.

Changes or additions to configuration files are most often associated
with specific features, and in Helix, this means that these
configuration changes belong in the modules that need them.

Sitecore include files
^^^^^^^^^^^^^^^^^^^^^^

Changes to any configuration under the <sitecore> root in the web.config
should always be done through app\_config/include files.

.. admonition:: Habitat Example

    .. figure:: _static/image36.png

        Figure: Foundation/Multisite specific configuration changes

Place the configuration changes for a given module in the modules layer
subfolder under /include and name the configuration file with
[Layer].[Module].config.

Sitecore merges include files alphabetically, and if a certain
configuration file needs to be included last in the web.config merge
with in a layer, prefix the file with z., for example
z.Foundation.Indexing.config. If the file needs to be run last of all
include files, place the file in a subfolder under /include called zzz.
Refer to the Sitecore documentation for more information on config
patching.

Other .config files
^^^^^^^^^^^^^^^^^^^

Changes to .config files outside the <sitecore> element in the
web.config, such as the .NET or IIS parts of the web.config or other
.config files such as domains.config, will require another strategy.
Keep in mind the Helix convention: keeping the configuration change
together with the business logic which requires it.

Sitecore does not provide an out-of-the-box approach for this challenge,
and other tools such as the Visual Studio web.config transformations or
`SlowCheetah <https://visualstudiogallery.msdn.microsoft.com/69023d00-a4f9-4a34-a6cd-7e854ba318b5>`__
works in a file-based approach – which is not directly compliant with
Helix, as all changes to a single file are not necessarily associated
with a single module.

The MS Build xml transforms can be used to apply feature centric
configuration changes to files, but it will require custom integration
into the MS Build system. Please refer to the MS Build documentation on
the TransformXml task.

.. admonition:: Habitat Example

    Habitat does use the MS Build XmlTransform task to make multiple file
    transformation across features. This is done as part of the gulp build
    system supplied with the Habitat example site.

    The functionality allows each module to have one or more .transform
    files placed in the same sub folder as the target .config file and with
    the same name. For example, the
    /App\_Config/Security/domains.config.transform will apply a
    transformation to the domains.config file as part of the build. The
    syntax of the .transform file follows the MS Build web.config
    transformation syntax (See
    https://msdn.microsoft.com/en-us/library/dd465326(v=vs.110).aspx).

    All .transform files are picked up in the 04-Apply-Xml-Transform gulp
    task in the /gulpfile.js and applied one by one in a separate MS Build
    command defined in the /applytransform.targets file.

    At the time of writing, Habitat has four config transformations across
    the web.config and domains.config files.

        .. figure:: _static/image37.png

            Figure: Output from the Habitat xml transform task