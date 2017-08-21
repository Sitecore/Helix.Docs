What to deploy and to where
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Some data and configuration will sit outside the development and build
phases of the application lifecycle. Therefore, your process should
cater for this environment specific data or configuration (see :doc:`/principles/configuration/value-scope`).

Some data and configuration is owned by the development process (such as
C# code, views and the template structure) while others are owned by the
production environment (such as the content items). It is important that
your deployment process takes this into consideration and maps this
carefully. This is especially important for items in Sitecore and
configuration in .config changes –both of which can be managed in
multiple places. Also, this is important in an automation process, as
you do not want to overwrite production content or configuration by
accident or be unable to test on a representative production-like
dataset.

The detailed ownership and direction of flow depends on the business
logic and requirements of the solution. For example, although templates
are most often managed in development and should at all times be
deployed from development to production, in some rare cases Project
layer templates, such as Page Type templates and Datasource templates,
can be managed partly in production to allow for dynamic fields and
content.

.. figure:: _static/image48.png
    
    Figure: Parts of a deployed Sitecore instance

The diagram above breaks down the overall parts of a typical deployed
Sitecore instances, and highlights some of the data types and
configurations to consider. The following describes the diagram in more
details. Ownership in the table means that a change in the given
environment always takes precedence – and therefore will overwrite
changes in other environments.

Items
    :What is it: Items in the Sitecore databases (core and master)

    Content Items
        :What is it: The content that is displayed on a website or other digital channel, and settings that affect the behaviour of a website or another digital channel. This content can be edited by content authors.   
        :Owned by: Production
        :Direction: Typically moved from production to other environments for testing. Some items might initially be created in development and deployed to production in an install-once process.

    Definition Items 
        :What is it: Sitecore data items that configure the implementation and that have a direct relationship with the presentation and business logic in the code, for example templates, fields, layouts, placeholders etc.   
        :Owned by: Development   
        :Direction: Installed as part of application deployments from development to QA and ultimately production. 

Files    
    :What is it: Files on disk on the servers  
  
    Implementation Files   
        :What is it: The implementation specific files, for example assemblies, views, CSS and JavaScript files.     
        :Owned by: Development   
        :Direction: Installed as part of application deployments from development to QA and ultimately production. 

    Platform Files   
        :What is it: Vendor specific files, i.e. files that are installed as part of a standard module   
        :Owned by: Development   
        :Direction: Installed as part of application deployments from development to QA and ultimately production or as part of the initial configuration of the environment.  

    Configuration files  
        :What is it: .config or other files that configure the system.     

        Implementation   
            :What is it: Configuration that sets up the functionality, but that is application wide    
            :Owned by: Development   
            :Direction: Installed as part of application deployments from development to QA and ultimately production. 

        Role 
            :What is it: Configuration that sets up the instance as a particular Sitecore instance role, for example a delivery, management or xDB processing server.    
            :Owned by: Deployment    
            :Direction: Set up by the deployment process as part of the configuration of the installation. Any individual role configuration files can be managed in Development as part of the implementation.  

        Environment
            :What is it: Configuration file changes relating to the specific running server or specific environment, for example connection strings, server names, domains etc.
            :Owned by: Deployment    
            :Direction: Set up by the deployment and managed in the specific environments.

Environment    
    :What is it: The infrastructure needed for running the Sitecore and the application. 
    
    Configuration    
        :What is it: Server or environment specific configurations such as network, DNS, hosts file changes, machine.config etc. 
        :Owned by: Deployment    
        :Direction: Set up as part of the initial deployment process. Can be automated but often is not.

    Services   
        :What is it: Related services running in the environment or on the instance server, for example operating systems, IIS, SQL servers, Windows Services etc.   
        :Owned by: Deployment    
        :Direction: Set up as part of the initial deployment process. Can be automated but often is not.

    Infrastructure   
        :What is it: The underlying server, virtual or physical,     
        :Owned by: Deployment    
        :Direction: Set up as part of the initial deployment process. Can be automated but often is not.

Once you have mapped the ownership and direction of data in your
implementation, avoid making changes that violate this, for example by
submitting code or configuration changes directly to test or product
environments and circumventing the QA and development procedures.
Violating this mapping is highly discouraged and should be avoided at
all cost.

Consider every type of deployment onto the environments, including
initial deployment, vendor upgrades and minor or major application
updates, when designing your deployment process. Remember to take into
account the availability of the running solution.
