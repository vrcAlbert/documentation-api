.. _php/behaviours/contextable:

Contextable
###########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Contextable

	Allows a :php:class:`Nos\\Orm\\Model` to be bound to a context.

    .. seealso:: :doc:`/php/configuration/software/multi_context`.

Configuration
*************

.. php:attr:: context_property

	Required.
	Column used to store the item's context. Its data type must be ``varchar(25)``.

.. php:attr:: default_context

	Default context to use if not set when creating an item.

Methods
*******

.. php:method:: get_context()

	:returns: The item's context.

Other
*****

This behaviour extends :term:`Model->find()`.

Add option to ``where`` array passed to method: you can use the ``context`` key as an alias to search in the column
:php:attr:`Orm_Behaviour_Contextable::$context_property`.

Example
*******

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Contextable' => array(
				'events' => array('before_insert'),
				'context_property' => 'form_context',
			),
		);
	}

