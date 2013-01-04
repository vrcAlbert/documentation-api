API de définition des actions
=============================

La configuration d'un back-office d'application se fait en PHP, mais une fois dans le navigateur le code est propulsé par du Javascript.
Les principales actions Javascript sont donc définissables par des tableaux de configuration en PHP.

Cette synthaxe est notamment utilisée pour définir les actions :

* des launchers dans le :doc:`metadata </technical/applications/metadata>`
* des :doc:`data catchers </technical/sharing>`
* des boutons et menus des :doc:`appdesk` et des :doc:`onglets d'édition <crud>`

.. contents::
	:local:
	:backlinks: top

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

:ref:`Documentation de nosTabs() <javascript_api_tabs>`

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


nosDialog
^^^^^^^^^

:ref:`Documentation de nosDialog() <javascript_api_dialog>`

.. code-block:: php

	'action' => array(
		'action' => 'nosDialog',
		'dialog' => array(
			'ajax' => true,
			'contentUrl' => 'une/url/,
			'title' => 'un titre',
			'width' => 500, // Largeur de la popup
			'height' => 200, // Hauteur de la popup
		),
	),

confirmationDialog
^^^^^^^^^^^^^^^^^^

Une forme particulière de ``nosDialog`` pour les popups de confirmation.

.. code-block:: php

	'action' => array(
		'action' => 'confirmationDialog',
		'dialog' => array(
			'contentUrl' => 'une/url',
			'title' => 'un titre',
		),
	),


nosAjax
^^^^^^^

:ref:`Documentation de nosAjax() <javascript_api_ajax>`

.. code-block:: php

	'action' => array(
		'action' => 'nosAjax',
		'params' => array(
			'url' => 'une/url',
			'method' => 'POST',
			'data' => array(
				'id' => '{{_id}}',
			),
		),
	),

window.open
^^^^^^^^^^^

Ouvre une nouvelle fenêtre du navigateur.

.. code-block:: php

	'action' => array(
		'action' => 'window.open',
		'url' => 'une/url/,
	),

document.location
^^^^^^^^^^^^^^^^^

Change l'URL de la fenêtre du navigateur.

.. code-block:: php

	'action' => array(
		'action' => 'document.location',
		'url' => 'une/url/,
	),


nosMediaVisualise
^^^^^^^^^^^^^^^^^

L'action ``nosMediaVisualise`` dépend entièrement des données contextuelles passées à l'action.

.. code-block:: php

	'action' => array(
		'action' => 'nosMediaVisualise',
	),

dialogPick
^^^^^^^^^^

.. code-block:: php

	'action' => array(
		'action' => 'dialogPick',
		'event' => 'nom_de_l_evenement',
	),

