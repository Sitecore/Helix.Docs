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

Changes to any Sitecore configuration should always be done via ``App_Config\Include`` files,
known as *configuration patches*. Do **not** modify the ``Sitecore.config`` or any configuration
files in the ``App_Config\Sitecore`` folder directly.

.. admonition:: Habitat Example

    .. figure:: _static/image36.png

        Figure: Foundation/Multisite specific configuration changes

.. tip::
    Sitecore configuration patches allow you to dynamically manipulate the Sitecore
    XML configuration without modifying the built-in Sitecore configuration. This makes upgrades easier,
    and makes it much clearer what is built-in configuration, and what is a customization. See
    `Sitecore documentation on configuration patching <https://doc.sitecore.net/sitecore_experience_platform/developing/developing_with_sitecore/customizing_server_configuration/use_a_patch_file_to_customize_the_sitecore_configuration>`_
    for more details.

Configuration patches under ``App_Config\Include`` should be organized by module layer. Because
subfolders and their patches are merged alphabetically by default, you can use
`configuration layers <https://doc.sitecore.net/sitecore_experience_platform/developing/developing_with_sitecore/customizing_server_configuration/configuration_layers>`_
via the ``Layers.config`` to ensure module layers are merged in the appropriate order
(Foundation, Feature, Project).

.. admonition:: Habitat Example

    Habitat uses a
    `configuration transform <https://github.com/Sitecore/Habitat/blob/2d3ee809fa4035a46a410d0438ed41e1c7f8a3b1/src/Foundation/SitecoreExtensions/code/App_Config/layers.config.xdt>`_
    to influence the load order of module subfolders.

Place the configuration changes for a given module in the appropriate modules layer
subfolder under ``App_Config\Include`` and name the configuration file with
``[Layer].[Module].config``.

Again, Sitecore merges include files alphabetically. If a configuration file needs to be
included last in the merge with in a layer, prefix the file with ``z.``, for example
``z.Foundation.Indexing.config``. If the file needs to be run last of all
include files, place the file in a subfolder under ``App_Config\Include`` called ``zzz``, or
utilize the ``Layers.config``.


Role and environment-specific and configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You may need to alter the behavior of your Sitecore implementation based on *server role*,
e.g. Content Management or Content Delivery. You should take advantage of
`rule-based configuration <https://doc.sitecore.net/sitecore_experience_platform/developing/developing_with_sitecore/customizing_server_configuration/rulebased_configuration>`_
for these scenarios in order to simplify deployment. You can also utilize
`custom rules <https://doc.sitecore.net/sitecore_experience_platform/developing/developing_with_sitecore/customizing_server_configuration/add_a_custom_rule_to_your_configuration>`_
to dynamically apply different configuration for different environments, such as Development/QA/Production.

You may also place environment-specific configuration in the ``App_Config\Environment``
`configuration layer <https://doc.sitecore.net/sitecore_experience_platform/developing/developing_with_sitecore/customizing_server_configuration/configuration_layers>`_,
for environment-specific configurations where you need to ensure the configuration is patched last. This also clearly
communicates that the configuration may vary by deployment environment.



Other .config files
^^^^^^^^^^^^^^^^^^^

Changes to ``.config`` files outside the ``<sitecore>`` element,
such as the .NET or IIS parts of the ``Web.config`` or other
``.config`` files such as ``domains.config``, will require another strategy.
Keep in mind the Helix convention: keeping the configuration change
together with the business logic which requires it.

Sitecore does not provide an out-of-the-box approach for this challenge,
and other tools such as the Visual Studio ``web.config`` transformations or
`SlowCheetah <https://visualstudiogallery.msdn.microsoft.com/69023d00-a4f9-4a34-a6cd-7e854ba318b5>`__
work in a file-based approach – which is not directly compliant with
Helix, as all changes to a single file are not necessarily associated
with a single module.

The MS Build XML transforms can be used to apply feature centric
configuration changes to files, but it will require custom integration
into the MS Build system. Please refer to the MS Build documentation on
the ``TransformXml`` task.

.. admonition:: Habitat Example

    Habitat does use the MS Build ``XmlTransform`` task to make multiple file
    transformation across features. This is done as part of the gulp build
    system supplied with the Habitat example site.

    The functionality allows each module to have one or more ``.xdt``
    files placed in the same sub folder as the target ``.config`` file and with
    the same name. For example, the
    ``/App_Config/Security/domains.config.xdt`` will apply a
    transformation to the ``domains.config`` file as part of the build. The
    syntax of the ``.xdt`` file follows the MS Build ``Web.config``
    transformation syntax (See
    https://msdn.microsoft.com/en-us/library/dd465326(v=vs.110).aspx).

    All ``.xdt`` files are picked up in the ``04-Apply-Xml-Transform`` gulp
    task in the ``/gulpfile.js`` and applied one by one in a separate MS Build
    command defined in the ``/applytransform.targets`` file.

        .. figure:: _static/image37.png

            Figure: Output from the Habitat xml transform task