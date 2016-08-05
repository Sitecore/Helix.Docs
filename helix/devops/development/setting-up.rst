Setting up a development environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Optimising the task of setting up a local development environment is not
just about on-boarding new developers or resetting a developer’s local
environment – although these tasks can be important to optimise. It is
also – and sometimes more importantly – about being able to consistently
and quickly set up a given version of the complete clean implementation
for testing and troubleshooting.

Typically, after the initial build phase – where there often is an
abundance of resources – comes the support or extension phase. In this
phase, where there are often fewer resources and maybe even less
experience with the implementation and processes, there is often a need
for working on multiple branches at the same time, testing on
production-like environments, the need to establish troubleshooting
environments, etc. and so the need to quickly spin up a specific version
of the local development environment increases.

Setting up a local developer machine with a running environment can be
more or less complex given business requirements and dependencies, but
the following is an example of the tasks that could be involved and
example of what each might contain:

Check out
    Get the required branch or version from the version control.
    
    *For example: This is typically a manual clone from git or similar of the version which needs to be running.*

Dependencies
    Import and configure external frameworks and dependencies
    
    *For example: Execute package managers such as NuGet or npm or runs custom scripts to restore required dependencies*

Build
    Compile the modules
    
    *For example: Run compilers such as MSBuild and other tools, such as CSS/JavaScript processors.*

Baseline
    Set up a running website/environment based on a clean Sitecore or a defined baseline
    
    *For example: Install a local Sitecore setup, for example through SIM, PowerShell or similar. This may involve restoring backup databases with production-like test data. This may also involve restoring a virtual machine with the full running environment.*

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

.. admonition:: Habitat Example

    Habitat includes an example of an almost fully automated local
    environment configuration using a combination of various tools. The
    overall build system uses `Gulp <http://gulpjs.com/>`__, which can be
    triggered through the `Visual Studio Task
    Runner <https://blogs.msdn.microsoft.com/webdev/2016/01/06/task-runners-in-visual-studio-2015/>`__.

    Please note that the Habitat example site has all content versioned
    through the version control system – unlike a production environment in
    which content is managed in production – and can therefore use a clean
    Sitecore installation as the baseline.

        .. figure:: _static/image42.png

            Figure: Running the Publish task through the Visual Studio Task
            Runner