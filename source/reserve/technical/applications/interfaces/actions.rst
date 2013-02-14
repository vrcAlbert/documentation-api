API des actions
===============

La configuration d'un back-office d'application se fait en PHP, mais une fois dans le navigateur le code est propulsé par du Javascript.
Les principales actions Javascript sont donc définissables par des tableaux de configuration en PHP.
Une fois dans le navigateur, ces tableaux de configuration deviennent des objets JSON et l'action est exécutée via la méthode ``nosAction``.

.. contents::
	:local:
	:backlinks: top

Structure d'une action
----------------------

En Javascript :

.. code-block:: js

	{
		action: 'actionName',
		// les autres clés dépendent de l'action
	)

En PHP :

.. code-block:: php

	'action' => array(
		'action' => 'actionName',
		// les autres clés dépendent de l'action
	),

Cette synthaxe est notamment utilisée pour définir les actions :

* des launchers dans le :doc:`metadata </technical/applications/metadata>`
* des :doc:`data catchers </technical/sharing>`
* des boutons et menus des :doc:`appdesk` et des :doc:`onglets d'édition <crud>`

.. _javascript_action_nosaction:

nosAction en javascript
-----------------------

.. code-block:: js

	$(domContext).nosAction(action_json, data);

L'élément du DOM ``domContext`` est transmi comme contexte pour les actions en nécessitant un.

* ``action_json`` : ``{}``. L'action au format JSON
* ``data`` : ``{}``. Facultatif. Données contextelles à l'action, utilisées pour le :ref:`remplacement de paramètres <javascript_action_placeholder>`.

.. _javascript_action_placeholder:

Paramètres à remplacer
----------------------

Certaines valeurs de clé peuvent dépendre du contexte dans lequel l'action va être exécutée.
Par exemple, les actions définies pour chaque ligne d'un tableau d':doc:`AppDesk <appdesk>` : les données de l'item sur lequel porte l'action sont passées à l'action qui s'exécute et servent pour remplacer les paramètres.

Les paramètres à remplacer ont la forme : ``{{nom_du_paramètre}}``. Dans ce cas la clé ``nom_du_paramètre`` doit être présente dans le :ref:`JSON data <javascript_action_nosaction>`.

.. code-block:: php

	'action' => array(
		'action' => 'nosTabs',
		'tab' => array(
			'url' => 'admin/nos/page/page/insert_update/{{id}}',
			'label' => '{{title}}',
		),
	),

.. code-block:: js

	data = {
		id: 5,
		title: 'Un titre'
	};

Listes des actions
------------------

nosTabs
^^^^^^^

:ref:`Documentation de nosTabs() <javascript_api_tabs>`

En PHP :

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

En Javascript :

.. code-block:: js

	$(domContext).nosAction({
		action: 'nosTabs',
		method: 'add',
		tab: {
			url: 'une/url',
			label: 'un titre',
			iconUrl: 'url/de/icon.png'
		},
		dialog: {
			width: 800,
			height: 400
		}
	});

nosDialog
^^^^^^^^^

:ref:`Documentation de nosDialog() <javascript_api_dialog>`

En PHP :

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

En Javascript :

.. code-block:: js

	$(domContext).nosAction({
		action: 'nosDialog',
		dialog: {
			ajax: true,
			contentUrl: 'une/url/,
			title: 'un titre',
			width: 500,
			height: 200
		}
	});

confirmationDialog
^^^^^^^^^^^^^^^^^^

Une forme particulière de ``nosDialog`` pour les popups de confirmation.

En PHP :

.. code-block:: php

	'action' => array(
		'action' => 'confirmationDialog',
		'dialog' => array(
			'contentUrl' => 'une/url',
			'title' => 'un titre',
		),
	),

En Javascript :

.. code-block:: js

	$(domContext).nosAction({
		action: 'confirmationDialog',
		dialog: {
			contentUrl: 'une/url/,
			title: 'un titre'
		}
	});


nosAjax
^^^^^^^

:ref:`Documentation de nosAjax() <javascript_api_ajax>`

En PHP :

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

En Javascript :

.. code-block:: js

	$(domContext).nosAction({
		action: 'nosAjax',
		params: {
			url: 'une/url',
			method: 'POST',
			data: {
				id: '{{_id}}'
			)
		}
	}, {
		id: 5
	});

window.open
^^^^^^^^^^^

Ouvre une nouvelle fenêtre du navigateur.

En PHP :

.. code-block:: php

	'action' => array(
		'action' => 'window.open',
		'url' => 'une/url/,
	),

En Javascript :

.. code-block:: js

	$(domContext).nosAction({
		action: 'window.open',
		url: 'une/url'
	});

document.location
^^^^^^^^^^^^^^^^^

Change l'URL de la fenêtre du navigateur.

En PHP :

.. code-block:: php

	'action' => array(
		'action' => 'document.location',
		'url' => 'une/url/,
	),

En Javascript :

.. code-block:: js

	$(domContext).nosAction({
		action: 'document.location',
		url: 'une/url'
	});

nosMediaVisualise
^^^^^^^^^^^^^^^^^

| L'action ``nosMediaVisualise`` dépend entièrement des données contextuelles passées à l'action.
| :ref:`Documentation de nosMediaVisualise() <javascript_api_mediavisualise>`

En PHP :

.. code-block:: php

	'action' => array(
		'action' => 'nosMediaVisualise',
	),

En Javascript :

.. code-block:: js

	$(domContext).nosAction({
		action: 'nosMediaVisualise'
	}, {
		path: 'url/du/media/',
        image: true
	});

dialogPick
^^^^^^^^^^

En PHP :

.. code-block:: php

	'action' => array(
		'action' => 'dialogPick',
		'event' => 'nom_de_l_evenement',
	),

En Javascript :

.. code-block:: js

	$(domContext).nosAction({
		action: 'dialogPick',
		'event' => 'nom_de_l_evenement'
	});
