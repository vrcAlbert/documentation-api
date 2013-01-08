JavaScript API
==============

.. contents::
	:local:
	:backlinks: top
	:depth: 2


Dans les exemples de cette page, le ``domContext`` est un élément du DOM ou un selecteur jQuery.

.. _javascript_api_notifications:

nosNotify
---------

Méthode pour afficher des notifications à l'utilisateur. Cette méthode est une encapsulation du plugin jQuery `Pines Notify <http://pinesframework.org/pnotify/>`_.

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

nosTabs
-------

Une méthode pour gérer les onglets du back-office. C'est une méthode "à tiroir", le premier paramètre pouvant être assimilé à une sous-méthode.

nosTabs('open')
^^^^^^^^^^^^^^^

| L'action ``open`` ouvre un nouvel onglet ou ré-ouvre un onglet existant s'il a la même URL.
| L'action ``open`` est l'action par défaut de ``nosTabs``, c'est à dire que l'on peut se passer du premier paramètre ``open``.

.. code-block:: js

	$(domContext).nosTabs('open', {
		url: 'une/url', // L'URL de l'onglet. Seul paramètre obligatoire
		iframe: false, // Si true, l'onglet sera une iframe
		label: 'un titre', // Le libellé de l'onglet
		labelDisplay: true, // Si false, l'onglet n'affichera que l'icône
		iconUrl: 'url/de/l/icon.png', // L'URL de l'icône
		iconSize: 16 // Taille en pixel de l'icône (carré)
	});

	// Appel simplifié sans le 1er paramètre 'open'
	$(domContext).nosTabs({
		url: 'une/url',
		iframe: false,
		label: 'un titre',
		labelDisplay: true,
		iconUrl: 'url/de/l/icon.png',
		iconSize: 16
	});

nosTabs('add')
^^^^^^^^^^^^^^

L'action ``add`` ouvre systématiquement un nouvel onglet à la différence d'``open``.

.. code-block:: js

	$(domContext).nosTabs(
		'add',
		{
			url: 'une/url', // L'URL de l'onglet. Seul paramètre obligatoire
			iframe: false, // Si true, l'onglet sera une iframe
			label: 'un titre', // Le libellé de l'onglet
			labelDisplay: true, // Si false, l'onglet n'affichera que l'icône
			iconUrl: 'url/de/l/icon.png', // L'URL de l'icône
			iconSize: 16 // Taille en pixel de l'icône (carré)
		},
		'end' // Paramètre facultatif. Si 'before' ou 'after' ouvre l'onglet avant ou après l'onglet dans lequel se trouve l'élément du DOM domContext.
	);

.. _javascript_api_tabsclose:

nosTabs('close')
^^^^^^^^^^^^^^^^

Ferme l'onglet dans lequel se trouve l'élément du DOM ``domContext``

.. code-block:: js

	$(domContext).nosTabs('close');

.. _javascript_api_tabsupdate:

nosTabs('update')
^^^^^^^^^^^^^^^^^

Mets à jour l'affichage de l'onglet dans lequel se trouve l'élément du DOM ``domContext``, voir charge une nouvelle URL.

.. code-block:: js
   :emphasize-lines: 7

	$(domContext).nosTabs('update', {
		url: 'une/url', // L'URL de l'onglet.
		label: 'un titre', // Le libellé de l'onglet
		labelDisplay: true, // Si false, l'onglet n'affichera que l'icône
		iconUrl: 'url/de/l/icon.png', // L'URL de l'icône
		iconSize: 16, // Taille en pixel de l'icône (carré)
		reload: false // Si true et qu'une URL est fournie, cette URL sera chargée dans l'onglet dans lequel se trouve l'élément du DOM domContext
	});

nosTabs('current')
^^^^^^^^^^^^^^^^^^

Retourne l'index de l'onglet dans lequel se trouve l'élément du DOM ``domContext``.

.. code-block:: js

	var current = $(domContext).nosTabs('current');


.. _javascript_api_ajax:

nosAjax
--------

Cette méthode est une encapsulation de la méthode `jQuery.ajax() <http://api.jquery.com/jQuery.ajax/>`_. Son API est calquée dessus à l'exception de ces 3 différences :

* Quelques options par défaut sont différentes.
* Les fonctions de ``callbacks`` ``success`` et ``error`` sont `monkey-patched <http://fr.wikipedia.org/wiki/Monkey-Patch>`_ pour exécuter des opérations par défaut (en plus des ``callbacks`` éventuels fournis à la fonction).
	* La méthode :ref:`javascript_api_nosajaxsuccess` est automatiquement exécutée en cas de succès si le type de retour est au format JSON.
	* La méthode :ref:`javascript_api_nosajaxerror` est automatiqment exécutée en cas d'erreur.

.. code-block:: js

	$(domContext).nosAjax({
		dataType : 'json', // Le datatype est 'json' par défaut
		type     : 'POST', // La requête est faite en POST par défaut
		data     : {}
	});

.. _javascript_api_nosajaxsuccess:

nosAjaxSuccess
--------------

Traite un JSON de retour de requête AJAX à la recherche de clés spécifiques.

.. code-block:: js

	$(domContext).nosAjaxSuccess({});


* ``notify`` : ``string`` / ``[string]``. Appel à :ref:`javascript_api_notifications` avec le ou les messages.
* ``error`` : ``string`` / ``[string]``. Appel à :ref:`javascript_api_notifications` avec le ou les messages et un type de notification ``'error'``.
* ``action`` : ``string`` / ``[string]``. Appel à :ref:`javascript_api_nosaction` avec la ou les actions.
* ``closeDialog`` : ``bool``. Ferme la popup, si l'élément du DOM ``domContext`` est dans une popup. Voir :ref:`javascript_api_dialogclose`.
* ``closeTab`` : ``bool``. Ferme l'onglet dans lequel se trouve l'élément du DOM ``domContext``. Voir :ref:`javascript_api_tabsclose`.
* ``replaceTab`` : ``{}``. Met à jour l'onglet dans lequel se trouve l'élément du DOM ``domContext``. Voir :ref:`javascript_api_tabsupdate`.
* ``redirect`` : ``string``. Redirige la fenêtre du navigateur vers une nouvelle URL.
* ``dispatchEvent`` : ``string`` / ``{}`` / ``[]``. Dispatche un événement à tous les onglets du back-office. Voir :ref:`javascript_api_dispatchevent`.
* ``internal_server_error`` : ``{}``, // Affichage de l'erreur et du backtrace dans la console web


.. _javascript_api_nosajaxerror:

nosAjaxError
--------------

Traite un retour de requête AJAX en erreur.

| Affiche la popup de reconnection si l'erreur vient d'une fin de la session d'authentification.
| Affiche une notification sinon.

.. code-block:: js

	$(domContext).nosAjaxError(jqXHR, textStatus);

.. _javascript_api_dialog:

nosDialog
---------

Une méthode pour gérer les popups du back-office. C'est une méthode "à tiroir", le premier paramètre pouvant être assimilé à une sous-méthode.

nosDialog('open')
^^^^^^^^^^^^^^^^^

| L'action ``open`` ouvre un popup.
| L'action ``open`` est l'action par défaut de ``nosDialog``, c'est à dire que l'on peut se passer du premier paramètre ``open``.


Cette méthode est une encapsulation du plugin Wijmo `Dialog <http://wijmo.com/wiki/index.php/Dialog>`_. Son API est calquée dessus à quelques différences près :

* Quelques options par défaut sont différentes :
	* ``width`` : Largeur du container moins 200 pixels
	* ``height`` : Hauteur du container moins 100 pixels
	* ``modal`` : Par défaut la popup est modal
	* ``captionButtons`` : Les boutons ``pin``, ``refresh``, ``toggle``, ``minimize`` et ``maximize`` sont invisibles
* Ajout des options :
	* ``destroyOnClose`` : ``bool``. Détruit la popup à sa fermeture. ``true`` par défaut.
	* ``ajax`` : ``bool``. La ``contentUrl`` va être chargée en AJAX plutôt que dans une ``iframe``. ``true`` par défaut.
	* ``ajaxData`` : ``{}``. ``data`` passé à la requête AJAX si ``ajax`` est à ``true``.
* Gestion des événements. Les événements dispatchés par :ref:`javascript_api_dispatchevent` sont exécutés dans la popup.

Une popup peut être créée de 3 manières différentes :

* à partir d'un élément du DOM existant
* à partir d'une URL chargée dans une ``iframe``
* à partir d'une URL chargée dans une ``<div>`` en AJAX

.. code-block:: js

	// Popup contenant le contenant le résultat HTML de l'URL contentUrl
	$(domContext).nosDialog('open',	{
		contentUrl: 'une/url',
		ajaxData: {
			foo: 'bar'
		},
		title: 'un titre',
		height: 400,
		width: 700
	});

	// Identique au bloc précédent, sans le 1er paramètre 'open'
	$(domContext).nosDialog({
		contentUrl: 'une/url',
		ajaxData: {
			foo: 'bar'
		},
		title: 'un titre',
		height: 400,
		width: 700
	});

	// Popup contenant une iframe pointant sur contentUrl
	$(domContext).nosDialog({
		iframe: true
		contentUrl: 'une/url',
		title: 'un titre',
		height: 400,
		width: 700
	});

	// Popup contenant la <div> ayant pour id 'id_de_div'
	$('#id_de_div').nosDialog({
		title: 'un titre',
		height: 400,
		width: 700
	});

.. _javascript_api_dialogclose:

nosDialog('close')
^^^^^^^^^^^^^^^^^^

Ferme la popup dans laquelle se trouve l'élément du DOM ``domContext``

.. code-block:: js

	$(domContext).nosDialog('close');



.. _javascript_api_events:

Événements
----------

Le back-office de Novius OS est une seule "grosse" page HTML. Les actions faites dans un onglet peuvent avoir des effets sur ce qu'affiche un autre (pa exemple : ajout, modification ou suppression d'un item).

Un système d'événements à été mis en place pour permettre aux différents éléments d'interface de communiquer entre eux.

| D'un côté les éléments d'interface écoutent des événements (attachent des functions de callbacks) en se raccordant à des éléments spécifiques du DOM, les ``dispatchers``.
| De l'autre, les différentes actions génèrent des événements, le plus souvent renvoyés par les requêtes AJAX (voir :ref:`javascript_api_ajax`), qui sont ensuite dispatchés à tous les éléments d'interface via les ``dispatchers``.
| Chaque onglet et chaque popup a son ``dispatcher``.

Les événements dispatchés sont exécutés immédiatement sur l'onglet ou la popup active (ayant le ``focus``). Sur les autres onglets ou popups, ils ne sont exécutés que quand l'onglet ou la popup deviennent actif.

.. _javascript_api_eventsstructur:

Structure d'un event
^^^^^^^^^^^^^^^^^^^^

* ``name`` : ``string``. Seul élément obligatoire. Le nom de l'événement. Pour les événements pour sur un ``Model``, le nom est le nom du ``Model``, ``namespace`` compris.
* ``id`` : ``int`` / ``[int]``. Identifiant de l'item sur lequel porte l'événement.
* ``action`` : ``string``. Nom de l'action sur l'item ayant déclenché l'événement. Par exemple : ``insert``, ``update`` ou ``delete``.
* ``context`` : ``string`` / ``[string]``. Contexte, au sens du :doc:`/technical/multi-context`, de l'item ayant déclenché l'événement.


.. _javascript_api_eventslisten:

nosListenEvent
^^^^^^^^^^^^^^

| ``nosListenEvent`` permet d'écouter un (ou des) événement, c'est à dire enregistrer une fonction de ``callback`` qui sera appelée quand l'événement survient.
| L'écoute se fera sur le ``dispatcher`` le plus proche de l'élément du DOM ``domContext``.

``nosListenEvent`` accepte 3 paramètres :

* ``event`` : ``{}`` / ``[{}]``. L'événement à écouter.
* ``callback`` : ``function``. La fonction de ``callback`` à exécuter quand l'événement survient. La fonction prend en paramètre l'événement l'ayant déclenchée.
* ``caller`` : ``string``. Nom du ``listener``. Facultatif, mais si renseigné permet de stopper l'écoute spécifique au ``listener`` (voir :ref:`javascript_api_eventsunlisten`).

Pour que la fonction de ``callback`` soit déclenchée, il ne faut pas que l'événement écouté corresponde exactement à l'événement survenu. L'événement écouté ne peut porter que sur une parti de l'événement.

.. code-block:: js

	// Écoute tous les événements ayant comme nom 'Nos\Model_Page'
	$(domContext).nosListenEvent({
		name: 'Nos\Model_Page'
	}, function(event) {
		// ...
	}, 'caller');

	// Écoute tous les événements ayant comme nom 'Nos\Model_Page' et dont l'action est 'insert' ou 'delete'
	$(domContext).nosListenEvent({
			name: 'Nos\Model_Page',
			action: ['insert', 'delete']
		},
		function(event) {
			// ...
		});

	// Écoute tous les événements ayant comme nom 'Nos\Model_Page' et dont l'action est 'insert' ou 'delete',
	// ou les événements ayant pour nom 'Nos\Model_Page' et comme contexte 'main::en_GB'
	$(domContext).nosListenEvent([
		{
			name: 'Nos\Model_Page',
			action: ['insert', 'delete']
		},
		{
			name; 'Nos\Model_Page',
			context; 'main::en_GB'
		}
	], function(event) {
		// ...
	});

.. _javascript_api_eventsunlisten:

nosUnlistenEvent
^^^^^^^^^^^^^^^^

``nosUnlistenEvent`` permet de stopper l'écoute des événements pour un caller spécifique. Voir le paramètre :ref:`caller dans nosListenEvent <javascript_api_eventslisten>`.

.. code-block:: js

	$(domContext).nosUnlistenEvent('caller');

.. _javascript_api_dispatchevent:

nosDispatchEvent
^^^^^^^^^^^^^^^^

Permet de dispatcher un événement sur tous les ``dispatchers`` disponibles. Voir :ref:`javascript_api_eventsstructur`.

.. code-block:: js

	// Dispatche un événement comme quoi la page d'ID 4 a été créée dans le contexte 'main::en_GB'
	$.nosDispatchEvent({
		name: 'Nos\Model_Page',
		action: 'insert',
		id: 4,
		context: 'main::en_GB',
	});


.. _javascript_api_forms:

nosFormUI
---------

Met en forme les éléments de graphique, contenus dans l'élément du DOM ``domContext``, grace aux librairies `Wijmo <http://wijmo.com/wiki/index.php/Main_Page>`_ et `jQuery UI <http://http://api.jqueryui.com/>`_.

.. code-block:: js

	$(domContext).nosFormUI();

Les éléments suivant sont mis en forme :

* Les ``<input>`` de type ``text``, ``password``, ``email`` ou les ``<textarea>`` avec le `widget wijtextbox <http://wijmo.com/wiki/index.php/Textbox>`_.
* Les ``<select>`` avec le `widget wijdropdown <http://wijmo.com/wiki/index.php/Dropdown>`_.
* Les ``<input type="checkbox">`` avec le `widget wijcheckbox <http://wijmo.com/wiki/index.php/Checkbox>`_.
* Les ``<input type="radio">`` avec le `widget wijradio <http://wijmo.com/wiki/index.php/Radio>`_.
* | Les éléments ayant la classe CSS ``.expander`` avec le `widget wijexpander <http://wijmo.com/wiki/index.php/Expander>`_.
  | La mise en forme peut-être paramétrée en ajoutant un ``data-wijexpander-options`` (``{}``).
* Les éléments ayant la classe CSS ``.accordion`` avec le `widget wijaccordion <http://wijmo.com/wiki/index.php/Accordion>`_.
* | Les ``<input type="submit">`` et les ``<button>`` avec le `widget button <http://api.jqueryui.com/button/>`_.
  | La mise en forme peut être paramétrée en ajoutant des ``data-`` à l'élément :

	* ``red`` : pour que le bouton soit de couleur rouge.
	* ``icons`` : ``{}`` pour définir les icônes du bouton.
	* ``icon`` : pour définir le nom (voir le `nom des icônes jQuery UI <http://jqueryui.com/themeroller/>`_) de l'icône de gauche.
	* ``iconClasses`` : pour définir les classes CSS de l'icône de gauche.
	* ``iconUrl`` : pour définir l'URL de l'icône de gauche.

Pour ne pas qu'un élément soit mis en forme, il suffit de lui donner la classe CSS ``.notransform``.

nosFormAjax
^^^^^^^^^^^

La soumission des formulaires, contenus dans l'élément du DOM ``domContext``, se fera en AJAX grace au plugin `jquery-form <http://malsup.com/jquery/form/>`_.

Le type de données en retour est par défaut ``json``, et les ``callbacks`` ``success`` et ``error`` font automatiquement appel à :ref:`javascript_api_nosajaxsuccess` et :ref:`javascript_api_nosajaxerror`.

.. code-block:: js

	$(domContext).nosFormAjax();


nosFormValidate
^^^^^^^^^^^^^^^

Les formulaires contenus dans l'élément du DOM ``domContext``, seront validés côté client (dans le navigateur) avant soumission.

La validation utilise le plugin `jquery-validation <http://docs.jquery.com/Plugins/Validation>`_.
Les messages d'erreurs sont affichés à côté des éléments de formulaire incriminés et le cas des éléments imbriqués dans des ``accordions`` est pris en compte.

.. code-block:: js

	$(domContext).nosFormValidate({});


.. _javascript_api_onshow:

nosOnShow
---------

| ``nosOnShow`` permet l'exécution de fonctions au moment où l'élément devient visible.
| Dans la plupart des cas, elle est utilisé pour retarder la mise en forme d'élement lorsque cette mise en forme nécessite que l'élément est des dimensions et une position.

C'est une méthode "à tiroir", le premier paramètre pouvant être assimilé à une sous-méthode.

nosOnShow('one')
^^^^^^^^^^^^^^^^^

Exécute une méthode de ``callback`` au premier affichage de l'élément.

.. code-block:: js

	$(element).nosOnShow('one', function() {
		$(this).widget();
	});


nosOnShow('bind')
^^^^^^^^^^^^^^^^^

Exécute une méthode de ``callback`` à chaque affichage de l'élément.

.. code-block:: js

	$(element).nosOnShow('bind', function() {
		$(this).widgetRefresh();
	});

nosOnShow('show')
^^^^^^^^^^^^^^^^^

| Affiche tous les éléments ayant une fonction ``binder`` par ``nosOnShow`` et se trouvant dans l'élément du DOM ``domContext``, déclenchant ainsi la ou les fonctions.
| L'action ``show`` est l'action par défaut de ``nosOnShow``, c'est à dire que l'on peut se passer du premier paramètre ``show``.

.. code-block:: js

	$(domContext).nosOnShow();

	// Ou
	$(domContext).nosOnShow('show');

nosMedia
--------

Génère un élement graphique de sélection d'un média dans le Média Center, basé sur un ``<input type="hidden">``.

Utilise le plugin `inputFileThumb <http://www.novius-labs.com/contributions/jquery-plugin-inputfile/documentation.html>`_.

.. code-block:: js

	$(:input).nosMedia();

	$(:input).nosMedia({
		mode: 'image', // Peut aussi être 'all'
		inputFileThumb: {
			title: 'un titre'
		}
	});

.. _javascript_api_mediavisualise:

nosMediaVisualise
-----------------

Affiche un média, dans un popup pour les images, dans une nouvelle fenêtre de navigateur pour les autres.

.. code-block:: js

	$.nosMediaVisualise({
		path: 'url/du/media/'
		image: true
	});

nosUIElement
------------

Renvoi un élément graphique, non rattaché au DOM.

.. code-block:: js

	$.nosUIElement(element, data);

* ``element`` : ``{}``. L'élément à générer sous forme JSON.

 	* ``type`` : ``string``. ``button`` (par défaut) ou ``link``. Voir :ref:`javascript_api_forms` pour les ``data`` des ``buttons``, ceux des ``link`` sont quasiment les mêmes.
 	* ``label`` : ``string``. Libellé de l'élément.
 	* ``action`` : ``{}``. L'action a attaché à l'événement click. Voir :ref:`javascript_api_nosaction`.
 	* ``bind`` : ``{}``. Le ou les événements à attacher à l'élément. Voir `$().bind() <http://api.jquery.com/bind/>`_.
 	* ``disabled`` : ``bool``. Si ``true``, l'élément est désactivé.
 	* ``menu`` : ``{}``. Si présent, attache un menu contextuel à l'élément.

 		* ``menus`` : ``[{}]``. Tableau contenant chaque ligne du menu

 			* ``action`` : ``{}``. L'action a attaché à la ligne du menu. Voir :ref:`javascript_api_nosaction`.
 			* ``content`` : ``string``. Contenu HTML de la ligne du menu.
 			* ``label`` : ``string``. Libellé de la ligne du menu.
			* ``icon`` : `Nom de l'icône jQuery UI <http://jqueryui.com/themeroller/>`_ (sans ``ui-icon-``).
			* ``iconClasses`` : Les classes CSS de l'icône.
			* ``iconUrl`` : L'URL de l'icône.

		* ``options`` : ``{}``. Paramétrage du `widget wijmenu de Wijmo <http://wijmo.com/wiki/index.php/Menu>`_.

* ``data`` : ``{}``. Données rattachés à l'élément et passées en paramètre de l'action. Voir :ref:`javascript_api_nosaction`.


nosDataReplace
--------------

Remplace des caractères dans une chaîne ou un JSON (de façon récursive).

.. code-block:: js

	$.nosDataReplace(obj, data);

	$.nosDataReplace('exemple {{foo}}', {foo : 'bar'});
	// retourne 'exemple bar'

	$.nosDataReplace({
		chaine: 'exemple {{foo}}',
		json: {
			string: 'sample {{bar}}',
		}
	},
	{
		foo : 'bar',
		bar : 'foo'
	});
	// retourne {
	//	chaine: 'exemple bar',
	//	json: {
	//		string: 'sample foo',
	//}


nosToolbar
----------

Une méthode pour gérer les barres d'outils du back-office. C'est une méthode "à tiroir", le premier paramètre pouvant être assimilé à une sous-méthode.

nosToolbar('create')
^^^^^^^^^^^^^^^^^^^^

Crée une barre d'outils juste avant l'élément ``domContext``.

.. code-block:: js

	$(domContext).nosToolbar('create');

nosToolbar('add')
^^^^^^^^^^^^^^^^^

| L'action ``add`` ajoute un élément à une toolbar.
| L'action ``add`` est l'action par défaut de ``nosToolbar``, c'est à dire que l'on peut se passer du premier paramètre ``add``.

L'élément est ajouté à la barre d'outils dont dépend l'élément du DOM ``domContext``. Si aucune barre d'outils n'existe, elle est créée à la volée.

* ``element`` : Peut être du code HTML, un objet DOM ou un container jQuery.
* ``right_side`` : ``bool``. ``False`` par défaut, si ``true`` ajoute l'élément à la partie droite de la barre d'outils.

.. code-block:: js

	$(domContext).nosToolbar('add', element, right_side);

	\\ ou
	$(domContext).nosToolbar(element, right_side);

	\\ Ajoute un bouton à droite de la barre d'outils
	$(domContext).nosToolbar('<button>Exemple</button>', true);

	\\ Ajoute un lien à gauche de la barre d'outils
	var $a = $('<a href="#">Exemple</a>');
	$(domContext).nosToolbar($a);


nosAction
---------
