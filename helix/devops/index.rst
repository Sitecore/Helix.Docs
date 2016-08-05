DevOps and development lifecycle management
===========================================

The development lifecycle consists of a number of different phases. The
length of each phase depends on the development methodology you use
(Waterfall, Agile, etc.). These phases can include Analysis, Design,
Specification, Planning, Development, Testing, Deployment and more.

Depending on the complexity of your specific Sitecore implementation –
or general Sitecore governance model – the need for automation of all or
some of processes in the Application Lifecycle phases can vary greatly.
Take, for example, the differences between a small in-house development
team independently working solely and consistently on a single Sitecore
implementation, a Sitecore implementation partner trying to consistently
develop and maintain numerous Sitecore implementations and an enterprise
product owner trying to govern a Sitecore implementation with multiple
implementation partners and design agencies working together. In other
words, in some governance models, it would be acceptable to have
documented and manually executed processes, where as in others it could
be catastrophic to be unable to repeat processes consistently.

Therefore, DevOps can be as much a challenge of identifying and
prioritizing the important processes to automate as it is the task of
actually implementing the automation.

In the scope of this document we will only look into DevOps processes in
specific phases of the application lifecycle:

Development
    in which the features or modules are being built
Build
    or *Integration* in which the implementation is put together as a single testable package
Testing
    in which the features or integrated package are tested against the specifications
Deployment
    in which the package is ultimately deployed onto the production environment

Please note that this is in no way an in-depth look at the DevOps or a
governance model for these phases, but rather is an inspection of some
of the Sitecore related processes and activities in these phases.

.. toctree::
    :caption: Topics 
    :titlesonly:

    development/index
    integration/index
    testing/index
    deployment/index