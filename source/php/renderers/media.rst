Media Selector
##############

.. php:namespace:: Nos

.. php:class:: Renderer_Media

	| This renderer is used to pick a file from the media centre.
	| The UI part uses the jQuery UI widget called ``input-file-thumb``.


:Default UI:

    .. image:: images/media_selector_default.png
        :alt: Default UI

:Hover state UI:

    .. image:: images/media_selector_hover.png
        :alt: Hover state UI

:Hover state with a selected media UI:

    .. image:: images/media_selector_selection.png
	    :alt: Hover state with a selected media UI


Configuration
*************

.. php:attr:: mode

	Possible values are ``image`` (default) or ``all``.

.. php:attr:: inputFileThumb

	Options for the inputFileThumb widget used to render the UI. See the
	`inputFileThumb documentation <http://www.novius-labs.com/contributions/jquery-plugin-inputfile/documentation.html>`_
	for all available options.


.. note::

    The ``inputFileThumb.file`` key will automatically be populated with the URL of the media if a ``value`` is
    provided in the renderer.


Methods
*******

.. php:method:: renderer($renderer)

	:param Model $renderer:

	    HTML attributes (``name``, ``class``, ``id``, ``value``, etc.), with a special key ``renderer_options``

	:return: The <input> tag with JavaScript to initialise it

	Displays a media selector in a standalone manner.


Examples
********

Adding a media in a CRUD form configuration:

.. code-block:: php

    <?php

    return array(
        'label' => '',
        'renderer' => 'Nos\Renderer_Media',
        'renderer_options' => array(
            'mode' => 'image',
                'inputFileThumb' => array(
                'title' => 'Title of the image',
            ),
        ),
    );


Displaying a media selector:

.. code-block:: php

    <?php

    echo Nos\Renderer_Media::renderer(array(
        'name' => 'my_image',
        'class' => 'some_class',
        'value' => 2, // ID of the previously selected media
        'renderer_options' => array(
            'mode' => 'image',
                'inputFileThumb' => array(
                'title' => 'Title of the image',
            ),
        ),
    ));