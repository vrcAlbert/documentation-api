Fondamentaux de l'OS
====================

Une architecture MVC
--------------------

Novius OS répond aux standards de découpage Modèle Vue Contrôleur, qui définissent des logiques de travail :

- dans la conception des applications
- dans l’organisation d'un projet sous Novius OS

MVC et conception
^^^^^^^^^^^^^^^^^

L’architecture MVC organise toute la conception autour des données. Chaque modèle a des représentations concrètes, les vues (ex : le formulaire d’ajout / édition, la représentation arborescente ou sous forme de liste) ainsi qu'un contrôleur unique. Le contrôleur fournit des méthodes permettant de manipuler les données du modèle associé (ajouter, éditer, supprimer, associer, etc.).

Grâce au MVC, l’utilisateur sait précisément quelles données il traite. Cette architecture permet de mieux les segmenter et donc de rendre l’utilisation du système plus compréhensible, plus facile à appréhender et à maîtriser.

Organisation des fichiers
^^^^^^^^^^^^^^^^^^^^^^^^^

Tout Novius OS reprend les principes de segmentation issus de l’architecture MVC. Ils s'appliquent aussi bien au core qu'aux applications.

On distingue 5 dossiers principaux :

* **classes** : ce dossier regroupe la partie logique, c'est-à-dire les classes PHP qui définissent et manipulent les données. Il s'agit a minima des contrôleurs et modèles de l’application. On y retrouve également des outils utilisés par les vues ou directement par les contrôleurs. Attention, ces outils ne manipulent jamais directement les données de votre application.
* **config** : ce dossier rassemble l’ensemble des informations permettant de représenter vos modèles. Les contrôleurs effectuent les opérations logiques sur vos données, mais auront besoin d’informations complémentaires à transmettre aux vues pour leur représentation. Ces informations sont ainsi séparées des contrôleurs, n’ayant pas de valeur logique, et des vues, car celles-ci reçoivent les données en paramètres et ne les recherchent jamais.
	Les fichiers de config sont organisés dans le dossier config de manière symétrique à l’organisation des contrôleurs dans le dossier /classes/controller.
* **lang** : ce dossier contient les fichiers de traduction, organisés en sous-dossiers par langue.
* **static** : ce dossier contient l’ensemble des scripts (JS et CSS) et ressources publiques (comme les images) chargées en front office.
* **views** : ce dossier contient les fichiers responsables de l’affichage et de la représentation des données.

Utilisation de frameworks
-------------------------

L’utilisation de frameworks oriente fortement la conception et l’implémentation des applications. Il convient donc de connaitre le rôle de chacun. Pour autant, cette documentation concernant Novius OS avant tout, veuillez vous référer à de la documentation ou tutoriaux externes pour plus de précisions sur ces frameworks.

Framework back-end (PHP)
^^^^^^^^^^^^^^^^^^^^^^^^

`Consulter les tutoriaux FuelPHP par Novius <http://www.novius-labs.com/quel-framework-choisir-nous-votons-fuelphp,29.html>`_

Le framework PHP utilisé pour Novius OS est `FuelPHP <http://fuelphp.com>`_. Il influence évidemment la partie logique de Novius OS.

Les éléments de FuelPHP les plus utilisés sont ceux qui permettent de valider les données, l’ORM et le mapping des différents fichiers.
Au delà de ces éléments, des outils inclus dans le framework simplifient grandement l’implémentation des applications (comme l’objet `Arr <http://docs.fuelphp.com/classes/arr.html>`_ par exemple).

Framework front-end (Javascript)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Bien que les actions logiques soient effectuées en PHP côté serveur, Novius OS est en majorité écrit en Javascript. Cela s'explique par la grande importance donnée à l'interface utilisateur et à l'ergonomie (cf. :doc:`ergonomie`).

Pour proproser des interfaces et interactions riches, Novius OS utilise plusieurs librairies JS :

* **jQuery** : ce framework facilite l'écriture du code JS pour l'édition du contenu HTML. Il n'est pas directement orienté UI.
* **jQuery UI** : ce complément de jQuery permet d'ajouter des éléments d'interface. Une majorité de l'UI de Novius OS est issue de cette librairie.
* **Wijmo** : cette librairie est basée sur jQuery UI et fournit des éléments d'interface complémentaires, appelés widgets.

Il y a une hiérarchie entre ces librairies, Wijmo est la plus impactante sur l'ergonomie de Novius OS.
