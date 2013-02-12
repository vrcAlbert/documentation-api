Contextable
###########

.. php:class:: Orm_Behaviour_Contextable

	| For Model bound to a context. See :doc:`/php/configuration/multi_context`.
	| Belongs to the namespace :php:ns:`Nos`

Configuration
*************

.. php:attr:: context_property

	Required.
	Column name use for save context. Column must have type ``varchar(25)``.

.. php:attr:: default_context

	Default context to use if not set when create an item.

Methods
*******

.. php:method:: get_context()

	:returns: Item context.

Other
*****

This behaviour extend :term:`Model->find()`.

Add option to ``where`` array passed to method : you can use ``context`` key as alias for search in column :php:attr:`Orm_Behaviour_Contextable::$context_property`.

Example
*******

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Contextable' => array(
				'events' => array('before_insert'),
				'context_property'      => 'form_context',
			),
		);
	}

