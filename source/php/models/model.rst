.. _php/models/model:

Model
#####

.. php:namespace:: Nos\Orm

.. php:class:: Model

	Extend :term:`Model of FuelPHP ORM <\Orm\Model>`.

.. todo::

	Expliquer le système de configuration par fichier de config

Configuration
*************

.. php:attr:: title_property

	| Defined the title property of model. Can be a column name or a closure (which take current item to parameter).
	| If not defined, automatically set to first column which have ``title``, ``label`` or ``name`` in his name, if any first column in ``varchar``.

.. php:attr:: behaviours

	Defined behaviours of model like for :term:`observers <Observers>`.

.. php:attr:: attachment

	Defined attachments of model. Attachment is a Novius OS special type of :term:`relations <Relations>`. See :php:class:`Attachment`.

Examples
========

Example in the class definition:

.. code-block:: php

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

	* Relation type : :term:`has_many`.
	* Model : :php:class:`Model_Wysiwyg`

.. php:attr:: linked_medias

	* Relation type : :term:`has_many`.
	* Model : :php:class:`Model_Link`


Accessors
*********

.. php:attr:: medias

	Accessor for :php:class:`Model_Link` linked to model.

	.. code-block:: php

		$item->medias->avatar // Get a Model_Link with key 'avatar'
		$item->medias->avatar->media // Get Model_Media with key 'avatar'

		$item->medias->cv->media = Model_Media // Set a Model_Media to key 'cv'

.. php:attr:: wysiwygs

	Accessor for :php:class:`Model_Wysiwyg` linked to model.

	.. code-block:: php

		$item->wysiwygs->content // Get a Model_Wysiwyg with key 'content'
		$item->wysiwygs->content->wysiwyg_text // Get content of Model_Wysiwyg with key 'content'

		$item->wysiwygs->summary = 'foo' // Set a Model_Wysiwyg with key 'content', width content 'foo'.

Methods
*******

.. php:staticmethod:: title_property()

	:returns: Title property of model. See :php:attr:`Model::$title_property`.

.. php:staticmethod:: behaviours($specific = null, $default = null)

.. php:method:: get_possible_context()

	:returns: Array of possible contexts ID for current item. See :doc:`/php/configuration/software/multi_context`.

.. php:staticmethod:: add_properties($properties)

	:params array $properties: Properties to merge.

.. php:staticmethod:: prefix()

	:returns: Prefix of column name. Computed form primary key column name, search ``_``.

.. php:method:: title_item()

	:returns: Returns the item title, calculated from :php:attr:`Model::$title_property`.

.. php:method:: pick($column [, $column [, $column [, ... ]]] )

	:params array $column: A column name.
	:returns: Returns the first non empty column. Will add column prefix (see :php:func:`Model::prefix`) when needed.
