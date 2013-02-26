Tree
####

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Tree

	| Makes a :php:class:`Nos\\Orm\\Model` behaves like a Tree.
	| An item can then have a parent and children (all of the same Model).

Configuration
*************

.. php:attr:: parent_relation

	Required.
	Name of the parent :term:`relation <Relations>`.

.. php:attr:: children_relation

	Required.
	Name of the children :term:`relation <Relations>`.

.. php:attr:: level_property

	Column used to store the item's depth inside the tree. Data type must be ``int``.

Method
******

.. php:method:: get_parent()

	:returns: Model parent item, if it exists, ``null`` otherwise.

.. php:method:: set_parent($new_parent)

	Set a new parent for the item.

	If the item is :php:class:`twinnable <Nos\\Orm_Behaviour_Twinnable>` and if it exists in several contexts, all contexts will be moved synchronously.

	:param Model $new_parent: New parent Model of the item (use ``null`` to remove the parent).
	:throws:

	    ``Exception`` when:

	    - the item is moved in its own tree ;
	    - the item is :php:class:`twinnable <Nos\\Orm_Behaviour_Twinnable>` and its parent does not exist in one of the contexts of the current item.

.. php:method:: find_children($where = array(), $order_by = array(), $options = array())

	:returns: All direct children of item.

	Children can be filter and / or sort by parameters.

	| This method use native method :term:`Model->find()`.
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

This behaviour extends :term:`Model->find()`.

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
