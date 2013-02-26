Sharable
########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Sharable

	Adds the sharable behaviour on a :php:class:`Nos\\Orm\\Model`.

.. todo::

	* Lien vers comprendre le sharing dans un see also de la classe
	* Multiples liens vers reference glossaire de content nugget
	* Multiples liens vers reference glossaire de data catchers
	* Lien vers classe Model_Content_Nuggets
	* Lien vers classe Model_Media
	* Lien vers Monkey

Configuration
*************

.. php:attr:: data

Associative array of different types of data forming a ``content nuggets``.

* Keys can be one of :php:class:`DataCatcher` constants.
* Values are associative array.

	:value: A column name or a closure. See :ref:`php/behaviours/sharable_examples`.
	:useTitle: Help label indicate which property of item is use as default value.
	:options: Associative array of different options. Only for :php:const:`DataCatcher::TYPE_URL`.
	:possibles: Associative array of possibles values. Only for :php:const:`DataCatcher::TYPE_IMAGE`.

Methods
*******

.. php:method:: get_default_nuggets()

	:returns: Array containing the default ``content nuggets`` of an item.

.. php:method:: get_catcher_nuggets($catcher = Model_Content_Nuggets::DEFAULT_CATCHER)

	:param string $catcher: ``Data catchers`` ID.
	:returns: The ``Model_Content_Nuggets`` of this item for the specified ``data catcher``.

.. php:method:: get_sharable_property($property = null, $default = null)

	:param string $property: A property name.
	:param string $default: A default value if data property is null.
	:returns: :php:attr:`Orm_Behaviour_Sharable::$data` if ``$property`` is null. Otherwise, property value with default fallback.

.. php:method:: data_catchers()

    Retrieves all the data catchers that can use the ``content nugget`` of this item (checks the ``required_data`` of a
    data catcher and ).

	:returns: All the valid ``data catchers`` for this item (keys are the ``data catcher`` names).

.. php:method:: possible_medias()

    Retrieves all possible medias that can be associated with the item. Search for linked medias and images inserted in
    the WYSIWYGs.

	:returns: Associative array of all ``Model_Media``, ``Model_Media`` ID in keys, of item.

.. php:method:: get_nugget_content($catcher)

    Retrieves the personalised ``content nugget`` of a ``data catcher``, merged with the default ``content nugget`` of
    the item.

	:param string $catcher: ``Data catchers`` ID.
	:returns: ``Array`` A ``content nugget``.

.. _php/behaviours/sharable_examples:

Examples
********

A column for the default value
==============================

.. code-block:: php

	<?php
	array(
		\Nos\DataCatcher::TYPE_TITLE => array(
			'value' => 'monk_name',
		),
	);

A closure which returns a default value
=======================================

.. code-block:: php

	<?php
	array(
		\Nos\DataCatcher::TYPE_TITLE => array(
			'value' => function($monkey) {
				return $monkey->monk_name;
			},
		),
	);


Real example
============

Find in ``Monkey`` example application.

.. code-block:: php

	<?php

	class Model_Monkey extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Sharable' => array(
				'data' => array(
					\Nos\DataCatcher::TYPE_TITLE => array(
						'value' => 'monk_name',
						'useTitle' => __('Use monkey name'),
					),
					\Nos\DataCatcher::TYPE_URL => array(
						'value' => function($monkey) {
							$urls = $monkey->urls();
							if (empty($urls)) {
								return null;
							}
							reset($urls);

							return key($urls);
						},
						'options' => function($monkey) {
							return $monkey->urls();
						},
					),
					\Nos\DataCatcher::TYPE_TEXT => array(
						'value' => function($monkey) {
							return $monkey->monk_summary;
						},
						'useTitle' => __('Use monkey summary'),
					),
					\Nos\DataCatcher::TYPE_IMAGE => array(
						'value' => function($monkey) {
							$possible = $monkey->possible_medias();

							return Arr::get(array_keys($possible), 0, null);
						},
						'possibles' => function($monkey) {
							return $monkey->possible_medias();
						},
					),
				),
			),
		);
	}
