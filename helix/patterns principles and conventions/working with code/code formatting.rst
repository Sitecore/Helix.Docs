Code formatting
---------------

Formatting of code is deep in the tools layer, but can often be a great
source of discussion and frustration that can lead to decreased
productivity – and therefore important for establishing actual business
value. Focus on a common team standard, and then look at the tooling
available to make transitions for team members. As with most conventions
and standards consistency is essential. Less friction will ease
adoption.

Habitat Example

Habitat uses two spaces for indentation along with a whole series of
conventions, for example for brackets and syntax. Code indentation is
specified in the .editorconfig file in the solution root. The
editorconfig extension for Visual Studio
(https://visualstudiogallery.msdn.microsoft.com/c8bccfe2-650c-4b42-bc5c-845e21f96328)
will read the file when the solution is loaded and configure the editor
for this formatting.

Habitat also uses ReSharper for easy code formatting and has an
associated .DotSettings file that defines the chosen conventions.