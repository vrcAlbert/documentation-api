.. _php/models/model:

Model
#####

.. php:namespace:: Nos\Orm

.. php:class:: Model

    Extends :term:`Model of FuelPHP ORM <\Orm\Model>`.

    Novius OS Model have some differences compare with FuelPHP Model :

        * Novius OS implements a cache mechanism for properties when they are fetched from the database. By default, cache files are save in :file:`NOSPATH/local/cache/fuelphp/list_columns`.
        * In property definition, put ``convert_empty_to_null`` key to ``true`` if you want that this property stores a null value when it receives empty string.


Configuration
*************

.. php:attr:: title_property

	| Defines the title property of a model. Can be a column name or a closure (which take current ``$iitem`` as parameter).
	| If not defined, automatically set to first column which has ``title``, ``label`` or ``name`` in its name, or (as last resort) the first ``varchar``.

.. php:attr:: behaviours

	Defines the behaviours of model. Same syntax as :term:`observers <Observers>`.

.. php:attr:: attachment

	Defines the attachments of a model. Attachment is a special type of :term:`relations <Relations>` created for Novius OS. See :php:class:`Nos\\Attachment`.

.. php:attr:: shared_wysiwygs_context

	Array of WYSIWYG keys which are shared by context twins. See :ref:`WYSIWYG accessor <php/models/model/accessors>`.

.. php:attr:: shared_medias_context

	Array of media keys which are shared by context twins. See :ref:`Media accessor <php/models/model/accessors>`.

In Novius OS, you can configure model by a file configuration.
For sample: if in your application you define a ``Model_Monkey`` class, you can create a file :file:`config/model/monkey.config.php` to extend configuration.
All this attributes can be defined in configuration file : ``properties``, ``table_name``, ``title_property``, ``observers``,
``behaviours``, ``shared_wysiwygs_context``, ``shared_medias_context`` and all relations types (``has_many``, ``belongs_to``,
``has_one``, ``many_many``, ``twinnable_has_many``, ``twinnable_belongs_to``, ``twinnable_has_one``, ``twinnable_many_many``
and ``attachment``).


Examples
========

Example in the class definition:

.. code-block:: php

	<?php
	class Model_Example extends \Nos\Orm\Model
	{
		// In this example, attachments use defaults properties
		protected static $_attachment = array(
			'avatar' => array(),
			'cv' => array(),
		);

		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Contextable' => array(
				'events' => array('before_insert'),
				'context_property' => 'ex_context',
			),
		);

		// In this example, use a column name for defined title_property
		protected static $_title_property = 'ex_reference';

Example in configuration file:

.. code-block:: php

	<?php
	return array(
		'attachment' => array(
			'avatar' => array(
				'dir' => 'namespace/model_name/avatar/',
				'image' => true,
				'alias' => 'avatar',
			),
			'curriculum_vitae' => array(
				'dir' => 'namespace/model_name/curriculum_vitae/',
				'alias' => 'cv',
				'extensions' => array('doc', 'odt', 'pdf'),
				'check' => array('ClassName', 'methodName'),
			),
		),

		'behaviours' => array(
			'Nos\Orm_Behaviour_Contextable' => array(
				'events' => array('before_insert'),
				'context_property' => 'ex_context',
			),
		),

		// In this example, use a closure for defined title_property
		'title_property' => function($item) {
			return $item->ex_reference;
		},
	);

Relations
*********

.. php:attr:: linked_wysiwygs

	* Relation type: :term:`has_many`.
	* Model: :php:class:`Nos\\Model_Wysiwyg`

.. php:attr:: linked_medias

	* Relation type: :term:`has_many`.
	* Model: :php:class:`Nos\\Media\\Model_Link`


.. warning::

    Don't use these relations directly, we created accessors for them.

.. _php/models/model/accessors:

Accessors
*********

.. php:attr:: medias

	Accessor for :php:class:`Nos\\Media\\Model_Link` linked to model.

	.. code-block:: php

		<?php
		$item->medias->avatar; // Get a Model_Link named 'avatar'
		$item->medias->avatar->media; // Get Model_Media named 'avatar'

		$item->medias->cv = $Model_Media; // Attach a Model_Media named 'cv'

		$item->medias->cv = null; // Detach a media from an item
		// or
		unset($item->medias->cv);

.. php:attr:: wysiwygs

	Accessor for :php:class:`Nos\\Model_Wysiwyg` linked to model.

	.. code-block:: php

		<?php
		$item->wysiwygs->content; // Get a Model_Wysiwyg named 'content'
		$item->wysiwygs->content->wysiwyg_text; // Get content of Model_Wysiwyg named 'content'

		$item->wysiwygs->summary = 'foo'; // Set a Model_Wysiwyg named 'content', with content 'foo'.

		$item->medias->summary = null; // Remove a wysiwyg from an item
		// or
		unset($item->wysiwygs->summary);

Methods
*******

.. php:staticmethod:: title_property()

	:returns: Title property of model. See :php:attr:`Model::$title_property`.

.. php:staticmethod:: table()

	:returns: The DB table name of model.

.. php:staticmethod:: behaviours($specific = null, $default = null)

.. php:staticmethod:: add_properties($properties)

	:param array $properties: Additional properties (merged).

.. php:staticmethod:: addRelation($type, $name, array $options = array())

    Add a relation to model

    :param string $type: A valid relation type.
    :param string $name: The relation name to add.
    :param string $options: The relation options
    :throws: ``\FuelException`` if $type is not a valid one.

.. php:staticmethod:: configModel()

	:returns: Array configurations of the model.

.. php:staticmethod:: getApplication()

	:returns: Application name of the model.

.. php:method:: event($method, $args = array())

    Trigger an event (caught by behaviours) on the item.

    :param string $method: Name of the event, also name of the method Behaviours.
    :param array $args: Arguments of the event.

.. php:staticmethod:: eventStatic($method, $args = array())

    Trigger an event (caught by behaviours) on the model class.

    :param string $method: Name of the event, also name of the method Behaviours.
    :param array $args: Arguments of the event.

.. php:staticmethod:: prefix()

	:returns: Prefix of column name. Computed from the primary key name (everything before the first ``_`` character).

.. php:method:: title_item()

	:returns: Returns the item's title, calculated from :php:attr:`Model::$title_property`.

.. php:method:: pick($column [, $column [, $column [, ... ]]] )

	:param array $column: A column name.
	:returns: Returns the first non empty column. Will add column prefix (see :php:func:`Model::prefix`) when needed.
