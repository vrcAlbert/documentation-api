PHP to Javascript
#################

Configuring an application is in PHP, but once in the browser, code is powered by Javascript.

Some PHP configuration patterns are made for define Javascript behaviours.

.. _php/configuration/application/nosActions:

PHP nosActions
**************

:js:func:`$container.nosAction` execute an action bind to a DOM element.

To define an action in PHP:

.. code-block:: php

	<?php
	'action' => array(
		'action' => 'actionName', // nosTabs, nosDialog, confirmationDialog, nosAjax, window.open, document.location...
		// Other array keys depending the actionName
	),

	//Example for nostabs
	'action' => array(
		'action' => 'nosTabs',
		'tab' => array(
			'url' => 'admin/nos/page/page/insert_update/{{id}}',
			'label' => '{{title}}',
		),
	),

This syntax is used to define actions for:

* :ref:`php/configuration/metadata/launchers`
* :ref:`php/configuration/metadata/data_catchers`
* buttons and menus in :doc:`appdesk`
* :doc:`crud`


.. _php/configuration/application/cellFormatters:

PHP cellFormatters
******************

Use for formatting column display in grids of :doc:`appdesk`.

| A ``cellFormatter`` is an associative array.
| You can have multiple ``cellFormatter``, set an array of arrays.
| You can assign a key to a ``cellFormatter``. This way, someone else can delete or modify it by overloading configuration.

Common keys
===========

:type: The ``cellFormatter`` type. Can one of ``bold``, ``css``, ``icon``, ``iconClasses`` or ``link``.
:replace: If ``true``, ``cellFormatter`` empties the current content.

Types
=====

bold
----

Formatting content in bold. No additional key.

css
----

Apply CSS to content

:css: An associative array of styles CSS to apply.

.. code-block:: php

	<?php
	array(
		'type' => 'css',
		'css' => array(
			'text-align' => 'center',
		),
	),

icon
----

Add an icon, by its URL, before the actual content.

:column: The column key of item data which contains icon URL.
:src: The icon URL.
:mapping: An associative array, column value in keys, corresponding URLs in values.
:size: Size in pixel, use for width and height.

.. code-block:: php

	<?php
	array(
		'type' => 'icon',
		'column' => 'column_icon', //URL is in the 'column_icon' column
		'size' => 16
	),

	// Or
	array(
		'type' => 'icon',
		'src' => 'static/path/icon.png',
	),

	// Or
	array(
		'type' => 'icon',
		'mapping' => array(
			'1' => 'static/path/icon-1.png', // If column value is '1', use this URL
			'2' => 'static/path/icon-2.png',
		),
	),

iconClasses
-----------

Add an icon, by CSS classes, before the actual content.

:column: The column key of item data which contains icon CSS classes.
:classes: The icon CSS classes.

.. code-block:: php

	<?php
	array(
		'type' => 'iconClasses',
		'column' => 'column_icon_classes', //CSS classes is in the 'column_icon_classes' column
	),

	// Or
	array(
		'type' => 'iconClasses',
		'classes' => 'icon icon-foo',
	),

link
----

Add a link on actual content.

:action: Action when link clicked. Can be ``default`` for the default action of the item,
		 an :ref:`action name <php/configuration/application/common/actions>` of the item
		 or an :ref:`nosAction <php/configuration/application/nosActions>`.

.. code-block:: php

	<?php
	array(
		'type' => 'link',
		'action' => 'default', // Click bind the default action (ex: editing in the majority of cases)
	),

	// Or
	array(
		'type' => 'link',
		'action' => 'Namespace\Model_Example.result', // Click bind de 'result' action of the item, which is a Namespace\Model_Example instance.
	),

	// Or
	array(
		'type' => 'link',
		'action' => array(
			'action' => 'nosTabs', // Open a new tab
			'tab' => array(
				'url' => 'admin/nos/page/page/insert_update/{{_id}}', // {{_id}} will be replace by the current item ID
				'label' => '{{_title}}', // {{_title}} will be replace by the current item title
			),
		),
	),


Full example
============

.. code-block:: php

	<?php
	'data_mapping' => array(
		'column_a' => array(
			'title' => 'Column a'
			'cellFormaters' => array(
				'bold' => array(
					'type' => 'bold',
				),
				'center' => array(
					'type' => 'css',
					'css' => array(
						'text-align' => 'center',
					),
				),
			),
		),
		'column_b' => array(
			'title' => 'Column b'
			'cellFormaters' => array(
				'icon' => array(
					'type' => 'icon',
					'column' => 'column_icon',
					'size' => 16
				),
			),
		),
		'column_icon' => array(
			value => function($item) {
				return $item->icon();
			},
		),
	),
