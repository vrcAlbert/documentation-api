Virtualname
###########

.. php:class:: Orm_Behaviour_Virtualname

	| Add a slug property to item.
	| Belongs to the namespace :php:ns:`Nos`

| ``Nos\Orm_Behaviour_Virtualname`` génère un nom virtuel (``slug``) pour chaque item.
| Ce nom virtuel est généré automatiquement à partir de la propriété ``title_property`` du ``Model`` s'il n'est pas renseigné.

	Slug is automatically generated from ``title_property`` of Model if it is not specified.

	If :php:attr:`Orm_Behaviour_Virtualname::$unique` is set, ``->save()`` method can throw an ``Exception`` if slug already in use.

Configuration
*************

.. php:attr:: virtual_name_property

	Required.
	Column name use for save slug.

.. php:attr:: unique

	``true``, ``false`` or ``'context'`` if uniqueness must be done by context.

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

