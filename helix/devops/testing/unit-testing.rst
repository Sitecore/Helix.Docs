Unit tests
~~~~~~~~~~

There is a fair number of unit testing approaches and frameworks for
.NET and Sitecore, but as with other technologies and methodologies,
Helix does not dictate which to choose. We do emphasise the value of
adding unit tests to your business logic, and highly encourage the
general practice.

On disk, unit test projects should be contained in the /tests folder
below the module folder. In Visual Studio the unit test project should
be in the same Visual Studio solution as the corresponding module
projects and contained with the module solution folder.

.. admonition:: Habitat Example

    .. figure:: _static/image46.png
    
        Figure: Unit Test Project in Visual Studio

.. admonition:: Habitat Example

    Unit Tests in Habitat are developed as Arrange-Act-Assert and uses the
    following modules:

    -  xUnit (https://xunit.github.io) framework as the main unit testing framework
    -  NSubstitute (http://nsubstitute.github.io/) for mocking objects
    -  AutoFixture (https://github.com/AutoFixture/AutoFixture) for “Arranging” the unit tests
    -  FluentAssertions (http://www.fluentassertions.com/) for the assertion syntax
    -  FakeDb (https://github.com/sergeyshushlyapin/Sitecore.FakeDb) for faking Sitecore objects and services

    Example of a Habitat unit test for Sitecore.Feature.Language.LanguageRepository:

    .. code-block:: csharp
    
        public class LanguageRepositoryTests
        {
            [Theory]
            [AutoDbData]
            public void GetActive_ShouldReturnLanguageModelForContextLanguage(Db db, [Content] DbItem item)
            {
                var contextItem = db.GetItem(item.ID);
                Context.Item = contextItem;
                var activeLanguage = LanguageRepository.GetActive();
                activeLanguage.TwoLetterCode.Should().BeEquivalentTo(Context.Language.Name);
            }
        }

