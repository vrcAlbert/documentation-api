Model
#####

.. php:class:: Model

	| Extend Model of FuelPHP ORM.
	| Belongs to the namespace :php:ns:`Nos/Orm`

.. seealso::

	See `Model of FuelPHP ORM <http://fuelphp.com/docs/packages/orm/creating_models.html>`_ for natives properties and methods.

.. todo::

	Revoir l'ensemble
	Expliquer le système de configuration par fichier de config
	Lien vers Media et Wysiwyg

Configuration
*************

.. php:attr:: title_property

	| Defined the title property of model. Can be a column name or a closure (which take current item to parameter).
	| If not defined, automatically set to first column which have ``title``, ``label`` or ``name`` in his name, if any first column in ``varchar``.

.. php:attr:: behaviours

	Defined behaviours of model like for `observers <http://fuelphp.com/docs/packages/orm/observers/intro.html>`_.

.. php:attr:: attachment

	Defined attachments of model. Attachment is a Novius OS special type of `relations <http://fuelphp.com/docs/packages/orm/relations/intro.html>`_. See :php:class:`Attachment`.

Examples
========

Example in the class definition:

.. code-block:: php

	class Model_Example extends \Nos\Orm\Model
	{
		// In this example, attachments use defaults properties
		protected static $_attachment = array(
			'avatar' => array(
			),
			'cv' => array(
			),
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
				'url_path' => 'avatar',
			),
			'curriculum_vitae' => array(
				'dir' => 'namespace/model_name/curriculum_vitae/',
				'alias' => 'cv',
				'extensions' => array('doc', 'odt', 'pdf'),
				'check' => function($attached, $file_name) {
					// ...
					// return true or false, depend if current user have right to get file.
				},
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

Properties
**********

.. php:attr:: medias

	:php:class:`Model_Media` link to model.

.. php:attr:: wysiwyg

	:php:class:`Model_Wysiwyg` link to model.


Methods
*******

.. php:staticmethod:: title_property()

	:returns: Title property of model. See :php:attr:`Model::$title_property`.

.. php:staticmethod:: behaviours($specific = null, $default = null)

.. php:method:: get_possible_context()

	:returns: Array of possible contexts ID for current item. See :doc:`/configuration/common/multi_context`.

.. php:staticmethod:: add_properties($properties)

	:params array $properties: Properties to merge.

.. php:staticmethod:: prefix()

	:returns: Prefix of column name. Computed form primary key column name, search ``_``.

.. php:method:: title_item()

.. php:method:: pick()
