Inheritance
~~~~~~~~~~~

In Helix, think of template inheritance as interfaces on an item which
exposes a certain set of data to the business logic. This makes it
possible for a multiple modules and business logic to share items and
content, but simple look at the interface of the item which they
understand.

The architecture does not have the concept of a single common base
template across all templates – which is a practice that is commonly
discouraged as it will often lead to bloated items with unnecessary
fields.

Any business logic or views which uses content on an item should
therefore only reference the base template of the item – by using a *is*
operator approach (for example by using the Item.Template.InheritsFrom)
– which allows for much less coupled feature modules and a freer content
architecture.

.. figure:: _static/image23.png

    Figure: Template inheritance

This figure shows how the architecture allows business and presentation
logic, i.e. renderings, and other logic to recognize the templates and
fields they require while at the same time allowing pages and page types
to be designed with the specific presentation and organisational
governance model in mind. In other words, renderings and business logic
can be written with sole focus on the domain of the specific feature and
oblivious to the other features or logic in the implementation.

