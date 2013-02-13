Sortable
########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Sortable

	For Model can be sort.

Configuration
*************

.. php:attr:: sort_property

	Required.
	Column name use for save sort index. Column must have type ``double``.

.. php:attr:: sort_order

	``ASC`` (défaut) ou ``DESC``

Methods
*******

.. php:method:: move_before($item)

	:param Model $item: Item before which move the current.

.. php:method:: move_after($item)

	:param Model $item: Item after which move the current.

.. php:method:: move_to_last_position()

	Move current item in last position.

Example
*******

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Sortable' => array(
				'events' => array('after_sort', 'before_insert'),
				'sort_property' => 'page_sort',
			),
		);
	}

	$page_1 = Model_Page::find(1);
	$page_2 = Model_Page::find(2);

	$page_2->move_after($page_1);
