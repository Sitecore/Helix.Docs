Rights management
~~~~~~~~~~~~~~~~~

Most aspects of rights and access are defined in the content area of the
sites and therefore in the Project layer modules or directly in the
production content itself.

These types of rights and roles could be called Organisational Rights or
Organisational Roles, as they typically will define the organisation or
groups to which the users belong, and thus the hierarchical content they
can access – and which rights they have to it.

But there are aspects of security that reach into the feature and
foundation modules – and which therefore needs to be addressed in the
modular context of Helix. This is particularly true for individual
fields, as these are defined in Interface Templates in the feature and
foundation layer modules. It is also true for configuration settings,
and even specific tools and editor extensions within Sitecore that are
contained within the feature modules.

These types of rights and roles are called Functional Rights or Roles,
as they define which types of functional access the user is given inside
for the hierarchy that he or she can access.

For example,: If a user has the functional role of News Editor and he
has the Organisational role to edit Site A, this user will be able to
edit news on Site A. If the same user is given the Organisational role
to read Site B, the user will not necessarily be able to edit news on
Site B, as he – although he has the functional right to edit news - will
not have the organisational right to edit content on Site B.

Functional Rights should be defined on Functional Roles owned by the
Feature or Foundation layer modules which defines them. Certain
Functional Roles and Rights will be managed on the project layer, for
example which Page Types an editor can create, which languages or which
workflow states.

This type of functional and organisational combination makes it possible
to define functional roles and rights on the features which defines
them, while staying independent of how the content is structured.

Habitat Example

The Habitat example site defines functional roles for the Feature and
Foundation modules that define access to fields and configuration on the
module. It also defines organisational Roles for the Habitat project.

    |image37|

    Figure 40: Example of Habitat feature roles

Feature roles are prefixed with the layer and module name followed by a
descriptive name for the role, for example sitecore/Foundation Accounts
Admin or sitecore/Feature Maps Editor.

It is highly discouraged to assign specific rights to individual users
inside Sitecore. Always set rights to domain roles and assign these
roles to the individual users.

The fact that a user in one domain can be a member of roles from another
domain can be very useful to separate rights in multi-tenant solutions
or between modules.