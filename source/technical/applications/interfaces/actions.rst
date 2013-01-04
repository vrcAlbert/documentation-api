API de définition des actions
=============================

La configuration d'un back-office d'application se fait en PHP, mais une fois dans le navigateur le code est propulsé par du Javascript.
Les principales actions Javascript sont donc définissables par des tableaux de configuration en PHP.

Cette synthaxe est notamment utilisée pour définir les actions :

* des launchers dans le :doc:`metadata </technical/applications/metadata>`
* des :doc:`data catchers </technical/sharing>`
* des boutons et menus des :doc:`appdesk` et des :doc:`onglets d'édition <crud>`

Synthaxe générique
------------------

.. code-block:: php

	'action' => array(
		'action' => 'actionName',
		// les autres clés dépendent de l'action
	),

Paramètres à remplacer
----------------------

Certaines valeurs de clé peuvent dépendre du contexte dans lequel l'action va être exécutée.
Par exemple, les actions définies pour chaque ligne d'un tableau d':doc:`AppDesk <appdesk>` : les données de l'item sur lequel porte l'action sont passées à l'action qui s'exécute et servent pour remplacer les paramètres.

Les paramètres à remplacer ont la forme : ``{{nom_du_paramètre}}``.

.. code-block:: php

	'action' => array(
		'action' => 'nosTabs',
		'tab' => array(
			'url' => 'admin/nos/page/page/insert_update/{{id}}',
			'label' => '{{title}}',
		),
	),

Listes des actions
------------------

nosTabs
^^^^^^^

.. code-block:: php

    // Paramétrage complet
	'action' => array(
		'action' => 'nosTabs',
		'method' => 'add',
		'tab' => array(
			'url' => 'une/url',
			'label' => 'un titre',
			'iconUrl' => 'url/de/icon.png',
		),
		'dialog' => array(
			'width' => 800, // Largeur de la popup modal si l'action déjà est exécuté depuis une popup modal.
			'height' => 400 // Hauteur
		),
	),

    // Paramétrage minimal
	'action' => array(
		'action' => 'nosTabs',
		'tab' => array(
			'url' => 'une/url',
		),
	),


:ref:`Documentation for nosTabs() <javascript_api_tabs>`


nosAjax (wrapper)
-----------------

:ref:`Documentation for nosAjax() <javascript_api_ajax>`

Example
^^^^^^^

.. code-block:: js

	// 1. Define a JSON action
	var myAction = {
		action: 'nosAjax',
		params: {} // Params, as defined in the nosAjax() API
	};

	// 2. Called it using the nosAction() wrapper
	$(context).nosAction(myAction);

	// The above is equivalent to
	$(context).nosAjax(myAction.params);



.. _javascript_actions_window-open:

window.open
-----------

Example
^^^^^^^

.. code-block:: js

	// 1. Define a JSON action
	var myAction = {
		action: 'window.open',
		url: 'http://...'
	};

	// 2. Called it using the nosAction() wrapper
	$(context).nosAction(myAction);

	// The above is equivalent to
	window.open(myAction.url);





