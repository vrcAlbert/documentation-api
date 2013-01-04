JavaScript API
==============

.. contents::
	:local:
	:backlinks: top
	:depth: 2


Dans les exemples de cette page, le ``context`` est un élément du DOM ou un selecteur jQuery.

.. _javascript_api_notifications:

Notifications
-------------

Un simple wrapper du plugin jQuery `Pines Notify <http://pinesframework.org/pnotify/>`_.

.. code-block:: js

	$.nosNotify('message');
	// L'exemple suivant est identique à la ligne précédente
	$.nosNotify('message', 'notice');

	$.nosNotify('message', 'error');

	$.nosNotify('message', 'success');

	$.nosNotify('message', 'info');
	// L'exemple suivant est identique à la ligne précédente
	$.nosNotify({
		title : 'message',
		type : 'info'
	});


.. _javascript_api_tabs:

Onglets
-------

Gestion des onglets du back-office.

Open
^^^^

L'action ``open`` ouvre un nouvel onglet ou ré-ouvre un onglet existant s'il a la même URL.

.. code-block:: js

	$(context).nosTabs('open', {
		url: 'une/url', // L'URL de l'onglet. Seul paramètre obligatoire
		iframe: false, // Si true, l'onglet sera une iframe
		label: 'un titre', // Le libellé de l'onglet
		labelDisplay: true, // Si false, l'onglet n'affichera que l'icône
		iconUrl: 'url/de/l/icon.png', // L'URL de l'icône
		iconSize: 16 // Taille en pixel de l'icône (carré)
	});


Add
^^^^

L'action ``add`` ouvre systématiquement un nouvel onglet à la différence d'``open``.

.. code-block:: js

	$(context).nosTabs(
		'add',
		{
			url: 'une/url', // L'URL de l'onglet. Seul paramètre obligatoire
			iframe: false, // Si true, l'onglet sera une iframe
			label: 'un titre', // Le libellé de l'onglet
			labelDisplay: true, // Si false, l'onglet n'affichera que l'icône
			iconUrl: 'url/de/l/icon.png', // L'URL de l'icône
			iconSize: 16 // Taille en pixel de l'icône (carré)
		},
		'end' // Paramètre facultatif. Si 'before' ou 'after' ouvre l'onglet avant ou après l'onglet courant.
	);

Close
^^^^^

Ferme l'onglet courant.

.. code-block:: js

	$(context).nosTabs('close');

Update
^^^^^^

Mets à jour l'affichage de l'onglet courant, voir charge une nouvelle URL.

.. code-block:: js
   :emphasize-lines: 9

	$(context).nosTabs('update', {
		url: 'une/url', // L'URL de l'onglet.
		label: 'un titre', // Le libellé de l'onglet
		labelDisplay: true, // Si false, l'onglet n'affichera que l'icône
		iconUrl: 'url/de/l/icon.png', // L'URL de l'icône
		iconSize: 16, // Taille en pixel de l'icône (carré)
		reload: false // Si true et qu'une URL est fournie, cette URL sera chargée dans l'onglet courant
	});

Current
^^^^^^^^

Retourne l'index de l'onglet courant.

.. code-block:: js

	var current = $(context).nosTabs('current');


.. _javascript_api_ajax:

Ajax
----

Usage
^^^^^

``$(context).nosAjax(params);``

The back-office is a big HTML page. Most requests are made using Ajax. Hence Novius OS has is wrapper around jQuery.

The ``nosAjax`` function has the same API as ``$.ajax``. There are two main differences:

* Default options
* Native operations performed on returned JSON

Default options
^^^^^^^^^^^^^^^

.. code-block:: js

	{
		dataType: 'json',
		type: 'POST'
	}


Callbacks & return value (JSON)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The ``success`` and ``error`` callbacks are `monkey-patched <http://en.wikipedia.org/wiki/Monkey_patch>`_ to perform default native operations (in addition to the callback provided by the user).

The returned JSON support the following actions:

* ``notify [string or array]`` : displays one or several notification(s).
* ``error`` [string or array]: displays one or several error notification(s).
* ``closeDialog [bool]``: used for ajax requests performed from a dialog.
* ``closeTab [bool]``: closes the current tab.
* ``replaceTab [string]``: URL of the new tab.
* ``dispatchEvent [object or array]``: see ``listenEvent()`` / ``dispatchEvent()``

Example of request
^^^^^^^^^^^^^^^^^^

.. code-block:: js

	// Performs a POST request, expecting JSON response
	$.nosAjax({
		'url': 'admin/nos/page/appdesk/clear_cache'
	});


Example of returned JSON
""""""""""""""""""""""""

.. code-block:: js

	{
		// This will trigger a notification
		'notify': 'Cache has been renewed.'
	}



.. _javascript_api_dialog:

Dialog
------

This API can be used to create a dialog:

* From an exising ``<div>``
* From an URL (``<iframe>``)
* From Ajax-fetched content

Default options
^^^^^^^^^^^^^^^

.. code-block:: js

	{
		destroyOnClose : true,
		width: window.innerWidth - 200,
		height: window.innerHeight - 100,
		modal: true,
		title: ''
	}

Usage
^^^^^

.. code-block:: js

	// Transform an existing div
	$(div).nosDialog();

	// Open an iframe
	$(context).nosDialog({
		contentUrl: 'http://...'
	});

	// Load Ajax HTML into the DOM and transform it into a dialog
	$(context).nosDialog({
		contentUrl: 'http://...',
		ajax: true,
		// optional data
		ajaxData: {}
	});


If the Ajax URL returns a valid JSON value, it will be parsed by our native Ajax response handler rather than opening a new tab.


The dialog knows the tab context it's opened from. If you close a tab, any dialog contained within it will appropriately be destoyed.



.. _javascript_api_events:

Events
------

Some UI widgets are listening to particular events. For example, the appdesk's grid and inspectors are listening to events related to Model they display.

Events are bound to the tab they're being registered from. Events can be dispatched (created) anytime from any tab. Callbacks registered in the active (visible) tab will be triggered instantaneously. Callback registered in non-active tabs will be trigger when it become visible.


Standard event structure used in Novius OS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: js

	{
		name: '', // model class related to the event. Example: ``Nos\Model_Page``
		id: 1, // primary key (or array) of the model
		action: '', // action performed. Examples: ``insert``, ``update``, ``delete``
		lang: '' // lang (or array) of the model
	}


Dispatched (created) events usually have a lot of informations than callback listen to. Listeners don't need the whole information to be useful, they can listen to a subset of the full event.


Listening
^^^^^^^^^

.. code-block:: js

	// Page grid listens the following events (if the selected lang is en_GB):
	$(context).nosListenEvent([
		{
			name: 'Nos\Model_Page',
			action: ['insert', 'delete']
		},
		{
			name; 'Nos\Model_Page',
			lang; 'en_GB'
		}
	], function() {
		// Reload the grid data
	});


The context will be listening to:

* all page's creation (from any language) or deletion (any page ID) ;
* any action performed on a page in en_GB (creation, deletion, update).

Both objects will match for the event ``{name:'Nos\Model_Page', action:'delete', lang: 'en_GB'}``.


Dispatching
^^^^^^^^^^^

This function does not require a context.

.. code-block:: js

	// This is triggered when a page is inserted
	$.nosDispatchEvent({
		name: 'Nos\Model_Page',
		action: 'insert',
		id: 4,
		lang: 'en_GB',
	});

	// This is triggered when a sub-tree is deleted
	$.nosDispatchEvent({
		name: 'Nos\Model_Page',
		action: 'delete',
		id: [4, 5, 9, 8],
		lang: ['en_GB', 'fr_FR'],
	});


.. _javascript_api_forms:

Forms
-----

UI enhancements
^^^^^^^^^^^^^^^

``$(context).nosFormUI();`` will perform UI enhancements on the form inputs. We rely mainly on `Wijmo <http://wijmo.com/wiki/index.php/Main_Page>`_, which use `jQuery UI <http://jqueryui.com/themeroller/>`_ for the theming:

* ``wijtextbox()``
* ``wijdropdown()``
* ``wijcheckbox()``
* ``wijradio()``
* ``wijexpander()`` for ``.expander`` elements
* ``wijaccordion()`` for ``.accordion`` elements

``<input type="submit">`` and ``<button>`` can have a ``data-icon="{icon-name}"`` or ``data-iconUrl="http://..."`` property. ``{icon-name}"`` is a standard icon name from jQuery UI.


Ajax
^^^^

``$(context).nosFormAjax();`` will use the `jquery-form <http://malsup.com/jquery/form/>`_ plugin to submit the form using Ajax rather than the native browser action. If there's validation too, it will run before submitting.

Most forms are using it, since it's part of the standard form layout.

Validation
^^^^^^^^^^

``$(context).nosFormValidate(params);`` will use the `jquery-validation <http://docs.jquery.com/Plugins/Validation>`_ plugin to perform inline validation on the elements. It's already configured to display error messages nicely, and take into account some specificity from the UI enhancements (like the accordion).

Most forms are using it, since it's part of the standard form layout.

.. _javascript_api_onshow:

On Show
-------

``nosOnShow()`` is a special API which delays the rendering of UI elements when they are visible.

A lot of UI elements don't initialise correctly when they are hidden (they can't calculate sizes properly).

.. code-block:: js

	// Instead of this:
	$(element).widget();

	// Do this:
	$(element).nosOnShow('one', function() {
		$(this).widget();
	});

	// You can also use 'bind' instead of 'one': the callback will be executed each time the element is shown, instead of just the first time.


This way, the element won't be initialised until it becomes visible. If you're responsible for the code displaying an element, then you just need to call ``.nosOnShow()`` to trigger the delayed actions on the children.

.. code-block:: js

	// Instead of this:
	$(element).show();

	// Do this:
	$(element).show().nosOnShow();


