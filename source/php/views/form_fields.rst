
.. _php/views/form_fields:

Fields
------

View path: ``nos::form/fields``


**Params**:

:begin:    String to display at the beginning.
:end:      String to display at the end.
:fields:   A list of field names.
:callback: Optional. Callback function used to render the field. By default, a field will be rendered by calling it's ``build()`` method.
:show_when_empty: Optional. Default false. Should the ``begin`` and ``end`` variables be displayed if there is no content inside of it?
