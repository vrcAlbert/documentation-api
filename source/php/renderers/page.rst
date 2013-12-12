Page Selector
##############

.. php:namespace:: Nos\Page

.. php:class:: Renderer_Selector

    | Extends :php:class:`Nos\\Renderer`.
    | This renderer is used to pick a page.
    | It displays a tree of the pages with radio buttons.


.. image:: images/page_selector.png
	:alt: Page selector UI


Configuration
*************

.. php:attr:: input_name

	Name for the radio input.

.. php:attr:: multiple

	Set to ``true`` if you want to select multiple pages. Default ``false``.

.. php:attr:: selected

    .. Strange syntax here, we need a dummy text and double-indentation for :id: or it will write 'Id' (uppercase I)

    An ``array``, or an ``array`` of ``array`` iff ``multiple`` is ``true``, containning:

        :id: Pre-selected page id (value).
        :model: ``Nos\Page\Model_Page``

.. php:attr:: treeOptions

    .. Strange syntax here, we need a dummy text and double-indentation for :context: or it will write 'Context' (uppercase C)

    ``Array``

    :context: Context of the pages displayed in the page selector.

.. php:attr:: height

    Height of the renderer. Default is 150px.

.. php:attr:: width

    Width of the renderer. Default is none.


Methods
*******

.. php:method:: renderer($renderer)

	:param Model $renderer:

	    Array the attributes.

	:return: The <input> tag with JavaScript to initialise it

	Displays a page selector renderer in a standalone manner.


Example
*******

Adding a page in a CRUD form configuration:

.. code-block:: php

    <?php

    return array(
        'label' => __('Location:'),
        'renderer' => 'Nos\Page\Renderer_Selector',
        'renderer_options' => array(
            'height' => '250px',
        ),
    );


Displaying a media selector:

.. code-block:: php

    <?php

    echo Nos\Page\Renderer_Selector::renderer(array(
        'input_name' => 'my_page',
        'selected' => array(
            'id' => 2, // ID of the previously selected page
        ),
        'treeOptions' => array(
            'context' => 'main::en_GB',
        ),
        'height' => '250px',
    ));
