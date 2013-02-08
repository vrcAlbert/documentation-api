Tree
####

.. php:class:: Orm_Behaviour_Tree

	| For Model whose behaviour tree (DB table has a join on itself).
	| We then say that an item has a parent and children.
	| Belongs to the namespace :php:ns:`Nos`

Configuration
*************

.. php:attr:: parent_relation

	Required.
	Name of the parent relation. See `relations in FuelPHP ORM <http://fuelphp.com/docs/packages/orm/relations/intro.html>`_.

.. php:attr:: children_relation

	Required.
	Name of the children relation.

.. php:attr:: level_property

	Column name use for save depth of item in tree. Column must have type ``int``.

Method
******

.. php:method:: get_parent()

	:returns: Return Model parent item if exist, ``null`` otherwise.

.. php:method:: set_parent($new_parent)

	:param Model $new_parent: New parent Model of item.
	:throws: ``Exception`` if item is moved in its own tree or, if item have behaviour :php:class:`Orm_Behaviour_Twinnable`,
	         if the new parent does not exist in one of the contexts of the current item.

	Set a new parent for the item.

	If item have behaviour :php:class:`Orm_Behaviour_Twinnable` and if it exists in several contexts, all contexts will be moved synchronously.

.. php:method:: find_children($where = array(), $order_by = array(), $options = array())

	:returns: All direct children of item.

	Children can be filter and / or sort by parameters.

	| This method use native method `->find() <http://fuelphp.com/docs/packages/orm/crud.html#read>`_ of FuelPHP Model.
	| ``$options`` parameter are passed to ``->find()`` like that:

	.. code-block:: php

		<?php
		$options = \Arr::merge($options, array(
			'where'    => $where,
			'order_by' => $order_by,
		));


.. php:method:: find_children_recursive($include_self = true)

	:param boolean $include_self: If ``true``, include current item in return.
	:returns: All children of item and their descendants.

.. php:method:: find_root()

	:returns: First ascendant of item in tree or ``null`` if item has no parent.

Other
*****

This behaviour extend Model method `->find() <http://fuelphp.com/docs/packages/orm/crud.html#read>`_.

Add option to ``where`` array passed to method : you can use ``parent`` key as alias for search in :php:attr:`Orm_Behaviour_Tree::$parent_relation` relation.

Example
*******

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Tree' => array(
				'events' => array('before_query', 'after_delete'),
				'parent_relation' => 'parent',
				'children_relation' => 'children',
				'level_property' => 'page_level',
			),
		);

		protected static $_has_many = array(
			'children' => array(
				'key_from'       => 'page_id',
				'model_to'       => 'Nos\Model_Page',
				'key_to'         => 'page_parent_id',
				'cascade_save'   => false,
				'cascade_delete' => false,
			),
		);

		protected static $_belongs_to = array(
			'parent' => array(
				'key_from'       => 'page_parent_id',
				'model_to'       => 'Nos\Model_Page',
				'key_to'         => 'page_id',
				'cascade_save'   => false,
				'cascade_delete' => false,
			),
		);

	}
