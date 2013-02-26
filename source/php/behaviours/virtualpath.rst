Virtualpath
###########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Virtualpath

	| Extends :php:class:`Nos\\Orm_Behaviour_Virtualname`.
	| Adds a virtual path to an item.

.. seealso::

	:php:class:`Nos\\Orm_Behaviour_Virtualname` for configuration and methods.

Configuration
*************

.. php:attr:: virtual_path_property

	Required.
	Column name use for save virtual path.

.. php:attr:: extension_property

	Required.
	If it's a ``string``, it will be appended to the virtual path.
	If it's an ``array``:

		:before: String to add to extension start.
		:after: String to add to extension end.
		:property: Column name used to store the extension.

.. php:attr:: extension_property

	Required.
	Name of the parent :term:`relation <Relations>` use to generate the first part of the virtual path.

Methods
*******

.. php:method:: virtual_path($dir = false)

	:param boolean $dir: If ``true``, extension is replaced by a final ``/``.
	:returns: Virtual path of the item.

.. php:method:: extension()

	:returns: Return extension part of the virtual path.

Example
*******

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Virtualpath' => array(
				'events' => array('before_save', 'after_save', 'change_parent'),
				'virtual_name_property' => 'page_virtual_name',
				'virtual_path_property' => 'page_virtual_url',
				'extension_property' => '.html',
				'parent_relation' => 'parent',
			),
		);
	}
