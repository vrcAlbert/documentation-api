Fondamentaux du logiciel
########################

.. sidebar:: Sommaire

	.. contents::
		:backlinks: top
		:depth: 2
		:local:

Une architecture MVC
********************

Novius OS répond aux standards de découpage `Modèle-Vue-Contrôleur <http://fr.wikipedia.org/wiki/Mod%C3%A8le-Vue-Contr%C3%B4leur>`_, qui définissent des logiques de travail :

- dans la conception des applications
- dans l’organisation d'un projet sous Novius OS

Organisation des fichiers
*************************

Tout Novius OS reprend les principes de segmentation issus de l’architecture MVC. Ils s'appliquent aussi bien au core qu'aux applications.

On distingue 5 dossiers principaux :

:file:`classes`
	Ce dossier regroupe la partie logique, c'est-à-dire les classes PHP qui définissent et manipulent les données.
	Il s'agit a minima des contrôleurs et modèles de l’application. On y retrouve également des outils utilisés par les vues ou directement par les contrôleurs.
	Attention, ces outils ne manipulent jamais directement les données de votre application.

:file:`config`
	| Ce dossier rassemble l’ensemble des informations permettant de représenter vos modèles.
	  Les contrôleurs effectuent les opérations logiques sur vos données, mais auront besoin d’informations complémentaires à transmettre aux vues pour leur représentation.
	  Ces informations sont ainsi séparées des contrôleurs, n’ayant pas de valeur logique, et des vues, car celles-ci reçoivent les données en paramètres et ne les recherchent jamais.
	| Les fichiers de config sont organisés dans le dossier config de manière symétrique à l’organisation des contrôleurs dans le dossier /classes/controller.

:file:`lang`
	Ce dossier contient les fichiers de traduction, organisés en sous-dossiers par langue.

:file:`static`
	Ce dossier contient l’ensemble des scripts (JS et CSS) et ressources publiques (comme les images) chargées en front office.

:file:`views`
	Ce dossier contient les fichiers responsables de l’affichage et de la représentation des données.

Utilisation de frameworks
*************************

L’utilisation de frameworks oriente fortement la conception et l’implémentation des applications.
Il convient donc de connaitre le rôle de chacun.
Pour autant, cette documentation concernant Novius OS avant tout, veuillez vous référer à de la documentation ou tutoriaux externes pour plus de précisions sur ces frameworks.

FuelPHP
=======

`Consulter les tutoriaux FuelPHP par Novius <http://www.novius-labs.com/quel-framework-choisir-nous-votons-fuelphp,29.html>`_

Le framework PHP utilisé pour Novius OS est `FuelPHP <http://fuelphp.com>`_. Il influence évidemment la partie logique de Novius OS.

Les éléments de FuelPHP les plus utilisés sont ceux qui permettent de valider les données, l’ORM et le mapping des différents fichiers.
Au delà de ces éléments, des outils inclus dans le framework simplifient grandement l’implémentation des applications (comme l’objet `Arr <http://docs.fuelphp.com/classes/arr.html>`_ par exemple).

ORM de FuelPHP
==============

ORM pour object-relational mapping. En français `mapping objet-relationnel <http://fr.wikipedia.org/wiki/Mapping_objet-relationnel>`_.

| L'ORM permet une gestion de la base de données par des objets PHP, des classes, et en gérant notamment les relations entre les tables.
| Des exemples parlent plus qu'un long discours :

.. code-block:: php

	$new_monkey = Model_Monkey::forge();
	$new_monkey->monk_name = 'Julian';
	$new_monkey->save();

	$monkeys = Model_Monkey::find('all');
	foreach ($monkeys as $monkey) {
		//...
	}

	$monkey = Model_Monkey::find(4);
	$monkey->delete();

Novius OS est basé sur `l'ORM de FuelPHP <http://www.fuelphp.com/docs/packages/orm/intro.html>`_. Veillez vous référer à sa documentation.

| Néanmoins, Novius OS ajoute une sur-couche notable à l'ORM : les ``Behaviours``.
| En français, ``Behaviours`` veut dire comportements. Les ``Behaviours`` permettent d'étendre des ``Model`` en y ajoutant des comportements standardisés.

Ils sont similaire aux `Observers <http://docs.fuelphp.com/packages/orm/observers/intro.html>`_ de FuelPHP mais plus puissant :

* Comme les ``Observers``, ils sont configurables par des options.
* Comme les ``Observers``, ils peuvent intercepter des événements pour agir sur le ``Model`` (par exemple l'événement ``before_save`` se déclenchant avant la sauvegarde).
* En plus, ils fournissent aussi des méthodes, d'instance ou statiques, sur le ``Model``.
* Ils peuvent également fournir de nouveaux événements.

jQuery UI / Wijmo
=================

Bien que les actions logiques soient effectuées en PHP côté serveur, Novius OS est en majorité écrit en Javascript.
Cela s'explique par la grande importance donnée à l'interface utilisateur et à l'ergonomie (cf. :doc:`ergonomie`).

Pour proproser des interfaces et interactions riches, Novius OS utilise plusieurs librairies JS :

**jQuery**
	| Ce framework facilite l'écriture du code JS pour l'édition du contenu HTML. Il n'est pas directement orienté UI.
	| `Documentation <http://api.jquery.com/>`__

**jQuery UI**
	| Ce complément de jQuery permet d'ajouter des éléments d'interface. Une majorité de l'UI de Novius OS est issue de cette librairie.
	| `Documentation <http://api.jqueryui.com/>`__

**Wijmo**
	| Cette librairie est basée sur jQuery UI et fournit des éléments d'interface complémentaires, appelés widgets.
	| `Documentation <http://wijmo.com/wiki/index.php/Main_Page>`__ et `Exemples <http://wijmo.com/demo/explore/>`__

Il y a une hiérarchie entre ces librairies, Wijmo est la plus impactante sur l'ergonomie de Novius OS.
