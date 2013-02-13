PHP to Javascript
#################

Configuring an application is in PHP, but once in the browser, code is powered by Javascript.

Some PHP configuration patterns are made for define Javascript behaviours.

PHP nosActions
**************

:js:func:`$container.nosAction` execute an action bind to a DOM element.

To define an action in PHP:

.. code-block:: php

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


PHP cellFormatter
*****************

