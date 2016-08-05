Deploying items
~~~~~~~~~~~~~~~

Even though the details of integrating and deploying your implementation
can be very specific to the business requirements, there are general
recommendations to integrating and deploying your items through
development to production environments (see 3.4).

Just as it is recommended to version and manage items and business logic
together in your development process, it is also highly recommended to
deploy business logic and items together in your deployment process.

Given the split between Definition and Content Items, the deployment
process can continuously deploy all Definition Items as part of a new
version of your implementation. Having this strict approach will help
assure that the ownership of Definition Items lies in the development
process and that no occasional changes are made in production or test
environments.

Note that the modularity of Helix is in no way meant as a general
modular approach to deploying and running Sitecore in production. Even
if you version and maintain modules separately in the development
process, your entire implementation should be integrated and deployed in
a single versioned process (See 3.2).

.. admonition:: Habitat Example

    Given the nature of the Habitat example site, all Content and Definition
    Items are versioned and managed in the development process and
    integrated and deployed as a single package. This is not possible in a
    real life scenario where content items are managed in production.

    Tools such as `Team Development for Sitecore`_ can help automate and secure
    the deployment of all Sitecore items – even Content items – through the
    environments.

.. _Team Development for Sitecore: http://www.teamdevelopmentforsitecore.com/