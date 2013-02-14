.. _php/behaviours/twinnable:

Twinnable
#########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Twinnable

	| Extend :php:class:`Orm_Behaviour_Contextable`.
	| It adds the ability to twin together different items with different contexts. See :doc:`/php/configuration/software/multi_context`.

.. seealso::

	:php:class:`Orm_Behaviour_Contextable` for configuration and methods.

Configuration
*************

.. php:attr:: common_id_property

	Required.
	Column name use for save the common ID between twin items. Column must have type ``int``.

.. php:attr:: is_main_property

	Required.
	Column name use for save if the item is the main item among twin items. Column must have type ``boolean``.

Methods
*******

.. php:method:: delete_all_context()

	Removes all items twinned to the current item, including the current item.

.. php:method:: is_main_context()

	:returns: ``True`` if item is the main among twin items.

.. php:method:: find_context($context)

	:param mixed $context:

		* Array of contexts ID.
		* ``all``, to receive all contexts.
		* Contexte ID.
		* ``main``, to receive main twin item.

	:returns: A twin item, or an array of twin items, ``null`` or ``array()`` if none.

.. php:method:: find_main_context()

	:returns: Return main twin item.

	Alias for ``->find_context('main')``.

.. php:method:: find_other_context($filter = array())

	:param array $filter: Array of contexts ID. If set, return only twin items which the context belongs to array ``$filter``.
	:returns: Array of twin items, current item exclude.

.. php:method:: get_all_context()

	:returns: Array of all twin contexts, current item context include.

.. php:method:: get_other_context($filter = array())

	:param array $filter: Array of contexts ID. If set, return only twin contexts which belongs to array ``$filter``.
	:returns: Array of all twin contexts ID, current item context exclude.

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
