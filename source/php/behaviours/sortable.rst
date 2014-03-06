Sortable
########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Sortable

	Makes a :php:class:`Nos\\Orm\\Model` sortable.

Configuration
*************

.. php:attr:: sort_property

	Required.
	Column name use for save sort index. Column must have type ``double``.

.. php:attr:: sort_order

	``ASC`` (default) ou ``DESC``

.. php:attr:: sort_twins

	``True`` by default. If ``false`` and the model is twinnable, the sorting won't be common to all contexts.

Methods
*******

.. php:method:: move_before($item)

	:param Model $item: Moves the current item before this one.

.. php:method:: move_after($item)

	:param Model $item: Moves the current item after this one.

.. php:method:: move_to_last_position()

	Moves the current item to the last position (of its siblings).

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
