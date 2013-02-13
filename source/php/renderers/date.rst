Date Picker
###########

.. php:namespace:: Nos

.. php:class:: Renderer_Date_Picker

	| This renderer is used to pick a date.
	| It's based on `jQuery UI Date Picker <http://jqueryui.com/datepicker/>`__.


.. image:: images/date_picker.png
    :alt: Date Picker UI


Configuration
*************

.. php:attr:: wrapper

	HTML string to wrap the ``<input>`` + the generated image to open the datepicker

.. php:attr:: datepicker

	Options for the datepicker widget used to render the UI. See the
	`jQuery UI documentation <http://api.jqueryui.com/datepicker/>`__ for all available options.

        .. Strange syntax here, we need a dummy text and double-indentation for :labels: to keep the case

        Default values below:

            :showOn: both
            :buttonImage: static/novius-os/admin/novius-os/img/icons/date-picker.png
            :buttonImageOnly: true
            :autoSize: true
            :dateFormat: yy-mm-dd
            :showButtonPanel: true
            :changeMonth: true
            :changeYear: true
            :showOtherMonths: true
            :selectOtherMonths: true
            :gotoCurrent: true
            :firstDay: 1
            :showAnim: slideDown


Methods
*******

.. php:method:: renderer($renderer)

	:param Model $renderer:

	    HTML attributes (``name``, ``class``, ``id``, ``value``, etc.), with a special key ``renderer_options``

	:return: The <input> tag with JavaScript to initialise it

	Displays a date picker in a standalone manner.


Example
*******

Adding a date picker in a CRUD form configuration:

.. code-block:: php

    <?php

    return array(
        'label' => '',
        'renderer' => 'Nos\Renderer_Date_Picker',
        'renderer_options' => array(
            'datepicker' => array(),
            'wrapper' => '<div class="datepicker-wrapper"></div>',
        ),
    );


Displaying a date picker:

.. code-block:: php

    <?php

    echo Nos\Renderer_Date_Picker::renderer(array(
        'name' => 'my_date',
        'class' => 'some_class',
        'value' => '2013-02-13',
        'renderer_options' => array(
            'datepicker' => array(),
            'wrapper' => '<div class="datepicker-wrapper"></div>',
        ),
    ));