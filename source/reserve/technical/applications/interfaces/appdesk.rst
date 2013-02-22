App Desk
========

L'*App Desk* est l'interface standard pour la page d'acceuil d'une application. Il inclue une ``grid`` principale, entourée par des inspecteurs.
L'idée est de facilement rendre disponible une liste centrale et un système de filtres pour les développeurs.

* :ref:`appdesk_general-informations`
* :ref:`appdesk_main-configuration`
* :ref:`appdesk_inspectors-configuration`

	* :ref:`appdesk_inspectors-configuration-model`
	* :ref:`appdesk_inspectors-configuration-tree`
	* :ref:`appdesk_inspectors-configuration-date`
	* :ref:`appdesk_inspectors-configuration-data`

.. _appdesk_general-informations:

Informations générales
----------------------

Quand l'utilisateur ouvre l'App Desk, la ``grid`` principale et les inspecteurs sont chargés qu'une seule fois et récupèrent les données via des requêtes ``ajax``.

* La ``grid`` principale appelle un ``controller`` qui étend ``\Nos\Controller_Admin_Appdesk``.
* Les inspecteurs appellent un ``controller`` qui généralement étend un des ``controllers`` d'inspecteur standards :

	* ``\Nos\Controller_Inspector_Model`` : Filtre standard sur un ``model``
	* ``\Nos\Controller_Inspector_Modeltree`` : Filtre sous forme d'arbre sur un ``model``
	* ``\Nos\Controller_Inspector_Date`` : Filtre par date
	* ``\Nos\Controller_Inspector_Data``  : Filtre statique

L'App Desk et les inspecteurs sont codés dans Novius OS avec la philosophie que tout peut être fait via des fichiers de configurations.
Par conséquent, si vous regardez le controller de l'App Desk de ``Monkey``, il étend ``\Nos\Controller_Admin_Appdesk`` :

.. code-block:: php

	namespace Nos\Monkey;

	class Controller_Admin_Appdesk extends \Nos\Controller_Admin_Appdesk
	{
	}

Le ``controller`` n'implémente aucune fonction. Tout est chargé par le fichier de configuration associé au ``controller`` de l'App Desk.

.. _appdesk_main-configuration:

Fichier de configuration de l'App Desk
--------------------------------------

Ci-dessous le fichier de configuration de l'App Desk de l'application ``Monkey`` :

.. code-block:: php

	<?php
	Nos\I18n::current_dictionary(array('noviusos_monkey::common', 'nos::common'));

	return array(
		'model' => 'Nos\Monkey\Model_Monkey',
		'inspectors' => array('species'),
		'search_text' => 'monk_name',
		'i18n' => array(
			'item' => __('monkey'),
			'items' => __('monkeys'),
			'showNbItems' => __('Showing {{x}} monkeys out of {{y}}'),
			'showOneItem' => __('Showing 1 monkey'),
			'showNoItem' => __('No monkey'),
			'showAll' => __('Showing all monkeys'),
		),
	);

.. only:: not_rtd


* ``model`` :
* ``query`` : parameters of the query executed when loading the data. This parameters are the same as the static ``find`` function in the orm.

	.. code-block:: php

		<?php
			'query' => array(
				'model' => 'Nos\Monkey\Model_Monkey',
				'related' => array('species'),
				'order_by' => array('monk_name' => 'ASC'),
				'limit' => 20,
			),

* ``search_text`` : column(s) to search into when the search input is filled in the main grid. It can be an ``array`` if search in multiple columns or a ``string`` if single.

	.. code-block:: php

		<?php
			'search_text' => 'monk_name',

* ``views`` : array key => values. Differents views available

	.. code-block:: php

		<?php
			'views' => array(
				'default' => array(
					'name' => __('Default view'),
					'json' => array(
						'static/novius-os/admin/config/media/common.js',
						'static/novius-os/admin/config/media/media.js'
					),
				),
				// ...
			),

	* ``name`` : name of the view
	* ``json`` : json sources

* ``selectedView`` : view by default

	.. code-block:: php

		<?php
			'selectedView' => 'default'

* ``dataset`` : key => value hash returned via ajax.

	.. code-block:: php

		<?php
			'dataset' => array(
				'id' => 'monk_id',
				'name' => 'monk_name',
				'species' => array(
					'value' => function($item) {
						return $item->species->mksp_title;
					},
				),
				'url' => array(
					'value' => function($item) {
						return $item->url_canonical(array('preview' => true));
					},
				),
				'actions' => array(
					'visualise' => function($item) {
						$url = $item->url_canonical(array('preview' => true));

						return !empty($url);
					}
				),
			),

	* if the value is a string, then its value is the column of the object (for example ``monk_id`` will get ``$monkey->monk_id``)
	* if the value is an array

		* the ``value`` key is a callback function which allows you to customize the value (for example take a look at ``species`` key which return the name of the monkey species)
		* if key is ``actions``, then the keys define whether or not the action are enabled (for example, the callback of ``visualise`` return true if the ``visualise`` action is enabled, false otherwise)

* ``inputs`` : is a key => value array allowing to apply filtering on the list (requested by the inspectors)

	.. code-block:: php

		<?php
			'inputs' => array(
				'monk_species_id' => function($value, $query) {
					if ( is_array($value) && count($value) && $value[0]) {
									$query->where(array('monk_species_id', 'in', $value));
					}

					return $query;
				},
			),

	* the key is the input name
	* the value is a callback function with two parameters

		* the first parameter is the value of the input
		* the second parameter is the query : the callback function have to modify the query object in order to apply the filtering requested

All keys we have enumerated since now have an effect on the json result returned by the controller. We will now get into the ``appdesk`` key, which determine the display of grid : columns title, actions display, inspector display and positions...

The ``appdesk`` key defines a key => value array :

* ``tab`` : how the tab is represented (same parameter of the tabs in the [[JavaScript API | (EN) JavaScript API]])

	.. code-block:: php

		<?php
			'tab' => array(
				'label' => __('Monkey'),
				'iconUrl' => 'static/apps/noviusos_monkey/img/32/monkey.png'
			),

* ``actions`` : predefined actions used by the appdesk, key => value array :

	.. code-block:: php

		<?php
			'actions' => array(
				'update' => array(
					'action' => array(
						'action' => 'nosTabs',
						'tab' => array(
							'url' => "admin/noviusos_monkey/monkey/insert_update/{{id}}",
							'label' => __('Edit'),
						),
					),
					'label' => __('Edit'),
					'primary' => true,
					'icon' => 'pencil'
				),
				//...
			),

	* the key is the action name
	* value, key => value array :

		* ``action`` : define the action executed when the action button is clicked. The parameters inside are the same as in [[JavaScript actions | (EN) JavaScript actions]]
		* ``label``
		* ``primary`` :

			* if set to true, the button will always be shown as standalone
			* if set to false, if there is more than two secondary button, the action will appear inside the drop down button ; otherwise it will also appear as a standalone button

		* ``iconClasses`` : set the css classes of the button's icon
		* ``icon`` : shorcut for iconClasses. Will set the css class of the button's icon to the jquery ui css class (for example, if the value is ``pencil``, then the css classes will be ``ui-icon ui-icon-pencil``)

* ``reloadEvent`` : the appdesk listens to the associated event (events if the value is an array). Take a look at events in the :doc:`javascript_api`

	.. code-block:: php

		<?php
			'reloadEvent' => 'Nos\Monkey\Model_Monkey',

* ``appdesk`` : display of the appdesk, key => value array :

	* ``buttons`` : upper buttons that are generally intended to add objects. It is a key => value array

		.. code-block:: php

			<?php
				'buttons' => array(
					'monkey' => array(
						'label' => __('Add a monkey'),
						'action' => array(
							'action' => 'nosTabs',
							'method' => 'add',
							'tab' => array(
								'url' => 'admin/noviusos_monkey/monkey/insert_update?lang={{lang}}',
								'label' => __('Add a new monkey'),
							),
						),
					),
					//...
				),

		* the key is the name of the action
		* the value is a key => value array :

			* ``label``
			* ``action`` : define the action executed when the button is clicked. The parameters inside are the same as in [[JavaScript actions | (EN) JavaScript actions]]

	* ``splittersVertical`` : position of the vertical splitter (distance from the left border in pixel)

		.. code-block:: php

			<?php
				'splittersVertical' => 250,

	* ``grid`` : display of the main grid

		.. code-block:: php

			<?php
				'grid' => array(
					'urlJson' => 'admin/noviusos_monkey/appdesk/json',
					'columns' => array(
						'name' => array(
							'headerText' => __('Name'),
							'dataKey' => 'name'
						),
						'lang' => array(
							'lang' => true
						),
						// ...
						'actions' => array(
							'actions' => array('update', 'delete', 'visualise'),
						),
					),
				),

	* ``urlJson`` : url called to load via ajax the json data
	* ``columns`` : key => value array which defines how the columns are displayed

		* ``headerText`` : head title of the column
		* ``dataKey`` : key of an item of the data received
		* ``lang`` : languages of the item if it has the translatable behaviour
		* ``actions`` : actions buttons, for each element of the array :

			* if it is a string, then it comes from the key related predefined action
			* it it is an array, it is a custom action which is defined the same way as the predefined actions

	* ``inspectors`` : key => value array which define the inspectors

		.. code-block:: php

			<?php
				'inspectors' => array(
					 'speciess' => array(
						'reloadEvent' => 'Nos\Monkey\Model_Species',
						'label' => __('Speciess'),
						'url' => 'admin/noviusos_monkey/inspector/species/list',
						'inputName' => 'monk_species_id[]',
						'vertical' => true,
						'grid' => array(
							'columns' => array(
								'title' => array(
									'headerText' => __('Species'),
									'dataKey' => 'title'
								),
								'actions' => array(/* ... */),
							),
							'urlJson' => 'admin/noviusos_monkey/inspector/species/json'
						),
					),
				),

		* the key is equivalent to the inspector name
		* ``reloadEvent`` : the event name that will trigger the inspector reload
		* ``label`` : title label of the inspector
		* ``url`` : url of the html structure of the inspector (loaded at the begining)
		* ``inputName`` : filter name affected by the inspector
		* ``vertical`` : if true, the inspector will be on the left, otherwise if will be on the top
		* ``grid`` : same as the main grid except it is for the inspectors

.. _appdesk_inspectors-configuration:

Inspectors configuration
------------------------

.. _appdesk_inspectors-configuration-model:

Model inspector
^^^^^^^^^^^^^^^

Example of configuration :

.. code-block:: php

	<?php
	return array(
		'query' => array(
			'model' => 'Nos\Monkey\Model_Species',
			'order_by' => array('mksp_title' => 'ASC'),
		),
		'dataset' => array(
			'id' => 'mksp_id',
			'title' => 'mksp_title',
		),
	);

The configuration has two keys :

* ``query`` : which defines the query executed for retrieving the data :

	* ``model`` is the model's class
	* all other columns are used for the query

* ``dataset`` : key => value hash returned via ajax, same as in the appdesk configuration

.. _appdesk_inspectors-configuration-tree:

Tree model inspector
^^^^^^^^^^^^^^^^^^^^

Example of configuration :

.. code-block:: php

	<?php
	return array(
		'models' => array(
			array(
				'model' => 'Nos\BlogNews\Blog\Model_Category',
				'order_by' => 'cat_sort',
				'childs' => array('Nos\BlogNews\Blog\Model_Category'),
				'dataset' => array(
					'id' => 'cat_id',
					'title' => 'cat_title',

				),
			),
		),
		'roots' => array(
			array(
				'model' => 'Nos\BlogNews\Blog\Model_Category',
				'where' => array(array('cat_parent_id', 'IS', \DB::expr('NULL'))),
				'order_by' => 'cat_sort',
			),
		),
	);

* ``models`` :

	* ``model`` : model's class
	* ``childs`` : children's classes
	* ``dataset`` : same as in the appdesk configuration
	* other columns can be applied to the query object

* ``roots`` : how to load the root nodes of the tree

	* ``model`` : model's class
	* other columns can be applied to the query object

.. _appdesk_inspectors-configuration-date:

Date inspector
^^^^^^^^^^^^^^

.. code-block:: php

	<?php
	return array(

		'input_begin'           => 'date_begin',
		'input_end'             => 'date_end',
		'label_custom'          => 'Custom dates',
		'label_custom_inputs'   => 'from xxxbeginxxx to xxxendxxx',
		'options'               => array('custom', 'since', 'month', 'year'),
		'since'                 => array(
			'optgroup'  => 'Since',
			'options'   => array(
				'-3 day'            => '3 last days',
				'previous monday'   => 'Week beginning',
				'-1 week'           => 'Less than a week',
				'current month'     => 'Month beginning',
				'-1 month'          => 'Less than one month',
				'-2 month'          => 'Less than two months',
				'-3 month'          => 'Less than three months',
				'-6 month'          => 'Less than six months',
				'-1 year'           => 'Less than one year',
			),
		),
		'month'                 => array(
			'optgroup'      => 'Previous months',
			'first_month'   => 'now',
			'limit_type'    => 'year',
			'limit_value'   => 1,
		),
		'year'                  => array(
			'optgroup'      => 'Years',
			'first_year'    => 'now',
			'limit'         => 4,
		),
	);


.. _appdesk_inspectors-configuration-data:

Data inspector
^^^^^^^^^^^^^^

Example of configuration :

.. code-block:: php

	<?php
	return array(
		'data' => array(
			array(
				'id' => 'image',
				'title' => 'Images',
				'icon' => 'image.png',
			),
			array(
				'id' => 'document',
				'title' => 'Documents',
				'icon' => 'document-office.png',
			),
	/* ... */


The ``data`` is simply sent via json. Each element in data has :

* ``id``
* ``title``
* ``icon`` : which is displayed at the left of the title (optionnal)
