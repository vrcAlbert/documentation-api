Form views
##########


Standard layout
---------------

View path: ``nos::form/layout_standard``.


.. image:: images/crud_form.png
	:alt: Standard layout of a form
	:align: center

**Params**:

:title:    Main fields at the top of the form.
:medias:   Medias are shown at the left of the title.
:large:    Default layout has spaces on the sides. If true, the form will use 100% of the width.
:save:     Which field is the save button.
:subtitle: Fields under title.
:content:  It has the same syntax as the **full** version of the ``layout`` (see above).
:menu:     Shown on the right. Data for the **accordion** view (see below). Optionally comes with an **simplified syntax**.


**Standard syntax** for the accordion:

.. code-block:: php

    array(
        'first_accordion' => array(
            'title' => __('My first accordion'),
            'fields' => array('field_1', 'field_2'),
        ),
        'second_accordion' => array(
            'title' => __('My second accordion'),
            'fields' => array('field_3', 'field_4'),
        ),
    ),

- if ``title`` is omitted, it will use the key as default value ;
- if ``fields`` is omitted, it will use the whole array as the list of fields.

(so you can't omit the ``fields`` if you set a ``title``).

**Simplified syntax** for the accordion:

.. code-block:: php

    array(
        __('My first accordion') => array(
            'field_1',
            'field_2',
        ),
        __('My second accordion') => array(
            'field_3',
            'field_4',
        ),
    ),

    // OR


    array(
        __('My first accordion') => array(
            'fields' => array('field_1', 'field_2'),
        ),
        __('My second accordion') => array(
            'fields' => array('field_4', 'field_4'),
        ),
    ),


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


Expander
--------

View path: ``nos::form/expander``

.. seealso:: `Wijmo Expander <http://wijmo.com/widgets/wijmo-open/expander/>`__


**Params**:

:title:   Expander's title.
:options: Options for the wijexpander.
:content: Either a plain *string*, a *callable*, or a *view* + *params* pair (array).


Fields
------

View path: ``nos::form/fields``


**Params**:

:begin:    String to display at the beginning.
:end:      String to display at the end.
:fields:   A list of field names.
:callback: Optional. Callback function used to render the field. By default, a field will be rendered by calling it's ``build()`` method.
