Setting up a development environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Optimising the task of setting up a local development environment is
a critical optimization point for on-boarding new developers
or resetting a developer’s local environment. It is also
about being able to consistently and quickly set up a given version
of the complete clean implementation for testing and troubleshooting.
This is especially the case during the support phase of a project,
where there are often fewer resources with less experience, who need to
quickly spin up a specific version of the local development environment.

Typical steps of a development environment setup might include:

Check out
    Get the required branch or version from the version control.
    
    *For example: This is typically a manual clone from git or similar of the version which needs to be running.*

Dependencies
    Import and configure external frameworks and dependencies
    
    *For example: Execute package managers such as NuGet or npm or run custom scripts to restore required dependencies*

Build
    Compile the modules
    
    *For example: Run compilers such as MSBuild and other tools, such as CSS/JavaScript processors.*

Baseline
    Set up a running website/environment based on a clean Sitecore or a defined baseline
    
    *For example: Install a local Sitecore setup, for example through Sitecore Install Framework. This may involve restoring backup databases with production-like test data. This may also involve restoring a virtual machine or containers with the full running environment.*

Publish
    Publish the modules to the baseline website
    
    *For example: Deploy the compiled assets and files to the running website - for example through Microsoft WebDeploy, PowerShell or similar.*

Configure
    Configure the baseline for the modules
    
    *For example: Add implementation specific configuration – to, for example, web.config or other files – using MSBuild, PowerShell or similar.*

Deserialize
    Restore the Sitecore items    
    
    *For example: Deserialize or install implementation or version specific items into the running website.*

It is recommended that you automate these steps as far as possible. This
will increase productivity and quality in both the short and especially
the long run.

A task runner framework of some kind can be very useful in automating this process.

.. admonition:: Sitecore Helix Examples

    The Sitecore Helix Examples take advantage of a PowerShell-based task runner
    which Sitecore developers are going to be using anyway -- the Sitecore Installation Framework (SIF).
    The examples use SIF to manage the Sitecore install and configuration, as well
    as solution builds and item deployment (particularly when using Unicorn). **The
    install and build system is optimized for the deployment of multiple examples and
    thus is likely more complex than needed for most solutions.** However, you may find
    SIF to be a useful task runner for your own solution as well. See there
    `SIF Configuration Guide <https://dev.sitecore.net/Downloads/Sitecore_Installation_Framework/2x/Sitecore_Installation_Framework_210.aspx>`__
    for information on creating custom SIF configurations and tasks.

    .. figure:: _static/basic-company-unicorn-sif-tasks.png
        :scale: 75%

        Figure: Custom SIF configuration for build and item deploy in Helix Basic Company - Unicorn
    
.. admonition:: Habitat Home

    The *Habitat Home* marketing demo sites utilize the popular C#-based task runner,
    `Cake (C# Make) <https://cakebuild.net/>`__. You can see
    `examples in the Habitat Home repository <https://github.com/Sitecore/Sitecore.HabitatHome.Platform/blob/master/build.cake>`__.

.. admonition:: Habitat

    The "original" Sitecore Helix example, Habitat, used `Gulp <http://gulpjs.com/>`__,
    as a task runner to build and deploy, which can be triggered through the `Visual Studio Task
    Runner <https://blogs.msdn.microsoft.com/webdev/2016/01/06/task-runners-in-visual-studio-2015/>`__.

    Though not as familiar to .NET developers due to the use of JavaScript-based
    tasks, Gulp may still be a good tool for teams who also need to automate front-end
    development tasks such as executing webpack configurations.

    .. figure:: _static/habitat-gulp-task-runner.png

        Figure: Running the Publish task through the Visual Studio Task
        Runner
