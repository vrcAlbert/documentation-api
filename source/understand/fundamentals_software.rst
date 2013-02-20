Fondamentaux du logiciel
########################

.. index:: MVC

Une architecture MVC
********************

Novius OS répond aux standards de découpage `Modèle-Vue-Contrôleur <http://fr.wikipedia.org/wiki/Mod%C3%A8le-Vue-Contr%C3%B4leur>`__,
qui définissent des logiques de travail :

- dans la conception des applications ;
- dans l’organisation d'un projet sous Novius OS.

Utilisation de frameworks
*************************

L'utilisation de frameworks oriente fortement la conception et l'implémentation des applications.
Il convient donc de connaitre le rôle de chacun.
Pour autant, cette documentation concernant Novius OS avant tout, veuillez vous référer à de la documentation ou
tutoriaux externes pour plus de précisions sur ces frameworks.

.. index:: FuelPHP

FuelPHP
=======

`Consulter les tutoriaux FuelPHP par Novius <http://www.novius-labs.com/quel-framework-choisir-nous-votons-fuelphp,29.html>`__

Le framework PHP utilisé pour Novius OS est `FuelPHP <http://fuelphp.com>`__.

Les éléments de FuelPHP les plus utilisés sont ceux qui permettent de valider les données, l'ORM et le mapping des différents fichiers.
Au delà de ces éléments, des outils inclus dans le framework simplifient grandement l'implémentation des applications (comme
la classe `Arr <http://docs.fuelphp.com/classes/arr.html>`__ par exemple).

.. index:: ORM

ORM de FuelPHP
==============

ORM pour object-relational mapping. En français `mapping objet-relationnel <http://fr.wikipedia.org/wiki/Mapping_objet-relationnel>`__.

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

Novius OS est basé sur `l'ORM de FuelPHP <http://www.fuelphp.com/docs/packages/orm/intro.html>`__. Veuillez vous référer à sa documentation.

| Néanmoins, Novius OS ajoute une sur-couche notable à l'ORM : les ``Behaviours``.
| En français, ``Behaviour`` veut dire comportement. Les ``Behaviours`` permettent d'étendre des ``Model`` en y ajoutant des comportements standardisés.

Ils sont similaires aux `Observers <http://docs.fuelphp.com/packages/orm/observers/intro.html>`__ de FuelPHP mais plus puissants :

* Comme les ``Observers``, ils sont configurables par des options.
* Comme les ``Observers``, ils peuvent intercepter des événements pour agir sur le ``Model`` (par exemple l'événement ``before_save`` se déclenchant avant la sauvegarde).
* En plus, ils fournissent aussi des méthodes, d'instance ou statiques, sur le ``Model``.
* Ils peuvent également fournir de nouveaux événements.

jQuery UI / Wijmo
=================

Bien que les actions logiques soient effectuées en PHP côté serveur, Novius OS est en majorité écrit en Javascript.
Cela s'explique par la grande importance donnée à l'interface utilisateur et à l'ergonomie (cf. :doc:`ergonomy`).

Pour proposer des interfaces et interactions riches, Novius OS utilise plusieurs librairies JS :

.. glossary::

	jQuery
		| Ce framework facilite l'écriture du code JS pour l'édition du contenu HTML. Il n'est pas directement orienté UI.
		| `Documentation <http://api.jquery.com/>`__

	jQuery UI
		| Ce complément de jQuery permet d'ajouter des éléments d'interface. Une majorité de l'UI de Novius OS est issue de cette librairie.
		| `Documentation <http://api.jqueryui.com/>`__

	Wijmo
		| Cette librairie est basée sur jQuery UI et fournit des éléments d'interface complémentaires, appelés widgets.
		| `Documentation <http://wijmo.com/wiki/index.php/Main_Page>`__ et `Exemples <http://wijmo.com/demo/explore/>`__

Il y a une hiérarchie entre ces librairies, Wijmo est la plus impactante sur l'ergonomie de Novius OS.
