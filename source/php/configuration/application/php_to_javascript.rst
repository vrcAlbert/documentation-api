PHP to Javascript
#################

Application configuration is mostly done in PHP, but a lot of code also runs in the browser, and is powered by JavaScript.

Some PHP configuration patterns have been created to define JavaScript behaviours from a PHP configuration file.

.. _php/configuration/application/nosActions:

PHP nosActions
**************

:js:func:`$container.nosAction` executes an action bound to a DOM element.

To define an action in PHP:

.. code-block:: php

	<?php
	'action' => array(
		'action' => 'actionName', // nosTabs, nosDialog, confirmationDialog, nosAjax, window.open, document.location...
		// Other keys are array and depends on the actionName
	),

	// Example with nostabs
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
* buttons and menus in the :doc:`appdesk`
* :doc:`crud`


.. _php/configuration/application/cellFormatters:

PHP cellFormatters
******************

Used to format the value displayed in a column of a grid in the :doc:`appdesk`.

| A ``cellFormatter`` is an associative array.
| You can have multiple ``cellFormatter``, just use arrays.
| You can assign a key to a ``cellFormatter``. This way, someone else can delete or modify it by overloading configuration.

Common keys
===========

:type: The ``cellFormatter`` type. Can one of ``bold``, ``css``, ``icon``, ``iconClasses`` or ``link``.
:replace: If ``true``, ``cellFormatter`` empties the current content.
:ignore: Column name to check if we should ignore this cellFormatter for the current item.
         If ``'1'`` (the string containing the digit ``1``), the cellFormatter will be ignored for this item.

Types
=====

bold
----

Formats the text in bold. No additional key.

css
----

Apply CSS styles to the content.

:css: An associative array of all CSS styles to apply.

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

Prepends an icon to the text, using an URL.

:column: Use a ``data_mapping`` column to fetch the icon URL.
:src: The icon URL.
:mapping: A mapping array to fetch URL depending on the value of the column.
:size: Force a size in pixels for the icon. Used for both width and height.

.. code-block:: php

	<?php
	array(
		'type' => 'icon',
		'column' => 'column_icon', // URL is retrieved from the 'column_icon' column
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

Prepends an icon to the text, using CSS classes.

:column: Use a ``data_mapping`` column to fetch the icon CSS classes.
:classes: The icon CSS classes.

.. code-block:: php

	<?php
	array(
		'type' => 'iconClasses',
		'column' => 'column_icon_classes', // CSS classes are fetch from the 'column_icon_classes' column
	),

	// Or
	array(
		'type' => 'iconClasses',
		'classes' => 'icon icon-foo',
	),

link
----

Wraps a link to the text (which performs an action upon click).

:action: Action to perform when the link is clicked. Can be ``default`` to use the default action of the item,
		 an :ref:`action name <php/configuration/application/common/actions>` of the item
		 or a :ref:`nosAction <php/configuration/application/nosActions>`.

.. code-block:: php

	<?php
	array(
		'type' => 'link',
		'action' => 'default', // Binds the default action (e.g.: 'edit the item' in the most of the cases)
	),

	// Or
	array(
		'type' => 'link',
		'action' => 'Namespace\Model_Example.result', // Binds the 'result' action of the item, which is a Namespace\Model_Example instance.
	),

	// Or
	array(
		'type' => 'link',
		'action' => array(
			'action' => 'nosTabs', // Open a new tab
			'tab' => array(
				'url' => 'admin/nos/page/page/insert_update/{{_id}}', // {{_id}} will be replaced by the item's ID
				'label' => '{{_title}}', // {{_title}} will be replaced by the item's title
			),
		),
	),


Custom cellFormatters
---------------------

It is possible to create custom `cellFormatters`. You just have to indicate your javascript url in the `type` key.

Here is a `cellFormatter` sample allowing you to change the font size of a column.

.. code-block:: js

	define(function(require, exports) {
		exports.format = function(formatter, args) {
			args.$container.css({
				'font-size': 20
			});
		}
	});

Full example
============

.. code-block:: php

	<?php
	'data_mapping' => array(
		'column_a' => array(
			'title' => 'Column a'
			'cellFormatters' => array(
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
			'cellFormatters' => array(
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
