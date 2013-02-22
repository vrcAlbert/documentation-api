Publishable
###########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Publishable

	Adds a publication status on a :php:class:`Nos\\Orm\\Model`.

.. note::

	For now, only one state yes / no is supported. Publication with dates of start and end will be possible later.

Configuration
*************

.. php:attr:: publication_bool_property

	Required.
	Column used to store the publication state. Its data type must be ``boolean``.

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
