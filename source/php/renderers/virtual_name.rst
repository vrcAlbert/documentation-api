Virtual name
############

.. php:namespace:: Nos

.. php:class:: Renderer_Virtualname

	This renderer is used for modify an item slug.

	.. seealso::

		:php:class:`Nos\Orm_Behaviour_Virtualname`


.. image:: images/virtual_name.png
    :alt: Virtual Name UI



Example
*******

Adding a Virtual name in a CRUD form configuration:

.. code-block:: php

    <?php

    return array(
        'label' => '',
        'renderer' => 'Nos\Renderer_Virtualname',
    );
