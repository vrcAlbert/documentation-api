Text
#####

.. php:namespace:: Nos

.. php:class:: Renderer_Text

	This renderer will show the value of the field as plain-text.

Examples
********

Adding a text in a CRUD form configuration:

.. code-block:: php

    <?php

    return array(
        'label' => '',
        'renderer' => 'Nos\Renderer_Text',
    );
