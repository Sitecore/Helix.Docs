Value Scope
~~~~~~~~~~~

Environment scoped values
^^^^^^^^^^^^^^^^^^^^^^^^^

Environment scoped values are configurations or settings whose values
change depending on the environment on which the implementation is
running. Environment scoped values are typically associated with
solution-wide configurations, such as connection strings, but can also
be context-wide – for example by allowing sites to specify the
connection string to use.

Environment-scoped values should be managed in .config files as they are
directly affected by the application lifecycle and deployments – which
is typically managed by IT.

In cases where environment scoped values are defined as Settings that
Sitecore users can manage, for example in cases where different sites or
content trees have different connection strings, let these settings
point to values defined in a .config file. This will make it possible to
change the values in Sitecore, while allowing deployments and the IT
application lifecycle to manage the environment’s specific values.

Do not manage environment scoped values as part of the development
process, but rather as part of your deployment procedure (see :doc:`/devops/deployment/index`).

Role scoped values
^^^^^^^^^^^^^^^^^^

Sitecore implementations can extend over multiple servers in a single
environment. This includes content management, content delivery, email
delivery, processing and more. Some configurations have different
values, for example disabling features or functionalities, on specific
server roles. An example of role scoped values is the configuration in
the
App\_Config/Include/Sitecore.Publishing.DedicatedInstance.config.example
file, which configures a server as a dedicated publishing server.

Role scoped values can be managed in the development process, for
example by managing role specific Sitecore .config include files or role
specific web.config files as part of the build process. Alternately the
specific values can be managed as part of the deployment process.

Role scoped values are typically restricted to IT/developer managed
configurations, as Settings are typically managed in Sitecore items –
whose values are shared across server roles.

Implementation scoped values
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This is by far the most typical value scope, as it is a value which,
when set, affects the entire implementation. Most configurations in the
Sitecore .config include files that are implementation scoped and user
managed Settings.

Implementation scoped values for Settings are typically initially
defined in the development process, but are managed as part of the
content management process in the production environment. As
implementation scoped settings values are therefore “owned” by the
Sitecore users in the production environment – and it should be able to
bring these back through the environments as part of the content - for
testing purposes, it is good practice to manage these as part of the
Sitecore content.

Always manage implementation scoped values in configurations in the
development environment and deploy them through the usual deployment
procedure. Avoid at all cost making implementation scoped changes in
specific environments as this will differentiate environments and can
severely cripple a consistent testing effort.

In Helix, implementation scoped values should always be associated with
the module which requires them. For example, if a Foundation module
requires the standard Sitecore configuration setting to change, the
module itself should manage this change – by including an
App\_Config/Include file in the module.