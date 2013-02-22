Virtualname
###########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Virtualname

	| Add a slug property to item.
    | The slug is automatically generated based on the ``title_property`` of the model if it is not specified.

	If :php:attr:`Orm_Behaviour_Virtualname::$unique` is set, ``->save()`` method can throw an ``Exception`` if slug already in use.

Configuration
*************

.. php:attr:: virtual_name_property

	Required.
	Column used to store the slug.

.. php:attr:: unique

	``true``, ``false`` or ``'context'`` if uniqueness must be checked by context.

Methods
*******

.. php:method:: virtual_name()

	:returns: Item slug.

.. php:method:: friendly_slug($slug)

	:param string $slug: A slug to clean.
	:returns: A clean slug, lowercase, without forbidden characters.

Example
*******

.. code-block:: php

	<?php
	class Model_Monkey extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Virtualname' => array(
				'events' => array('before_save', 'after_save'),
				'virtual_name_property' => 'monk_virtual_name',
			),
		);
	}

