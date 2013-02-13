Publishable
###########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Publishable

	For Model whose behavior publishable.

.. note::

	For now, only one state yes / no is supported. Publications with dates of start and end will be possible later.

Configuration
*************

.. php:attr:: publication_bool_property

	Required.
	Column name use for save publish state. Column must have type ``boolean``.

Methods
*******

.. php:method:: published()

	:returns: ``true`` or ``false`` depending on whether the item is published or not.

Example
*******

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Publishable' => array(
				'publication_bool_property' => 'page_published',
			),
		);
	}

	$page = Model_Page::find(1);

	if ($page->published()) {
		// Do something
	}
