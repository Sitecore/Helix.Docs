Integration, Acceptance or other automated testing methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When you are doing automated testing – and especially for automated
browser testing – you are often running the tests on an assembled
solution and therefore the tests might be dependent on the combined
pages of the website. Even though your tests might just focus on the
features or functionality in a single module, they depend on the
functionality of integration mapping in other modules or layers.
Therefore, the tests belong in the Project layer as opposed to together
with the module in the Feature or Foundation layer.

Code and other files related to tests – independent of whether they are
unit tests or other testing methodologies – belong in the /tests folder
under the respective module.

A single implementation can consist of multiple Visual Studio solutions.
It might be beneficial to keep automated testing projects (apart from
the unit tests) in a separate solution than the code.

.. admonition:: Habitat Example

    Habitat has a whole range of acceptance tests built with SpecFlow. These
    are generally structured to test the functionality within a single
    module. But since they rely on the integrated Habitat website to run,
    they are all located in the *Habitat* project layer module.

    .. figure:: _static/image47.png
    
        Figure: SpecFlow Projects under the Habitat Project Module