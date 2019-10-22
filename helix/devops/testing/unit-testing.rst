Unit tests
~~~~~~~~~~

There are a fair number of unit testing approaches and frameworks for
.NET and Sitecore, but as with other technologies and methodologies,
Helix does not dictate which to choose. We do emphasise the value of
adding unit tests to your business logic, and highly encourage the
general practice.

On disk, unit test projects should be contained in the ``/tests`` folder
below the module folder. In Visual Studio the unit test project should
be in the same Visual Studio solution as the corresponding module
projects and contained with the module solution folder.

.. admonition:: Sitecore Helix Examples

    .. figure:: _static/basic-company-navigation-tests-visualstudio.png
    
        Figure: Unit Test Project in Visual Studio

    Unit Tests in Helix Examples are developed as Arrange-Act-Assert and use the
    following modules:

    -  `xUnit <https://xunit.github.io>`__ framework as the main unit testing framework
    -  `Moq <https://github.com/moq/moq4>`__ for mocking objects
    -  `FakeDb <https://github.com/sergeyshushlyapin/Sitecore.FakeDb>`__ for faking Sitecore objects and services

