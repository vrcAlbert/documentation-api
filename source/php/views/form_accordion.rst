.. _php/views/form_accordion:

Accordion
---------

View path: ``nos::form/accordion``

.. seealso:: `Wijmo Accordion <http://wijmo.com/widgets/wijmo-open/accordion/>`__


For each accordion, you can either set:

- a **view** + **params** pair ;
- or a **fields** list.


**Params**:

:accordions: A list of accordions

    :title:           Optional. Default value is *empty string*.
    :view:            Optional. Path to a view.
    :params:          Optional. Data for the ``view``.
    :fields:          Optional. A list of field names.
    :field_template:  Optional. Template to wrap each field. Default value is ``<p>{field}</p>``
    :header_class:    Optional. CSS classes for the ``<h3>`` tag.
    :content_class:   Optional. CSS classes for the ``<div>`` panel.
