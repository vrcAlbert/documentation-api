.. _php/behaviours/twinnable:

Twinnable
#########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Twinnable

	| Extends :php:class:`Nos\\Orm_Behaviour_Contextable`.
	| It adds the ability to twin together different items with different contexts.

	.. seealso:: :doc:`/php/configuration/software/multi_context`.

    .. seealso:: :php:class:`Nos\\Orm_Behaviour_Contextable` for configuration and methods.

Configuration
*************

.. php:attr:: common_id_property

	Required.
	Column used to store the common ID between twinned items. Data type must be ``int``.

.. php:attr:: is_main_property

	Required.
	Column used to store if the item is the main item among twin items. Data type must be ``boolean``.

Methods
*******

.. php:method:: delete_all_context()

	Removes all items twinned to the current item, including the current item itself.

.. php:method:: is_main_context()

	:returns: ``True`` if item is the main among twin items.

.. php:method:: find_context($context)

	:param mixed $context: Can be

		* Array of contexts ID.
		* ``all``, to receive all contexts.
		* Context ID.
		* ``main``, to receive main twin item.

	:returns: A twinned item, or an array of twinned items, ``null`` or ``array()`` if none.

.. php:method:: find_main_context()

	:returns: The main item among the twins.

	Alias for ``->find_context('main')``.

.. php:method:: find_other_context($filter = array())

	:param array $filter: Array of contexts ID. If set, return only twin items which the context belongs to array ``$filter``.
	:returns: Array of twin items, current item exclude.

.. php:method:: get_all_context()

	:returns: Array of all twinned contexts, including the one of the current item.

.. php:method:: get_other_context($filter = array())

	:param array $filter: Array of contexts ID. If set, return only twinned contexts which belongs to array ``$filter``.
	:returns: Array of all twinned contexts ID, excluding the one of the current item.

Example
*******

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Twinnable' => array(
				'events' => array('before_insert', 'after_insert', 'before_save', 'after_delete', 'change_parent'),
				'context_property'      => 'page_context',
				'common_id_property' => 'page_context_common_id',
				'is_main_property' => 'page_context_is_main',
				'invariant_fields'   => array(),
			),
		);
	}
