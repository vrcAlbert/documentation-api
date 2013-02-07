Principes ergonomiques
======================

L’interface de Novius OS est construite autour de grands principes ergonomiques. Deux d’entre eux sont à connaitre pour
le développement d’applications : la navigation par onglets et l’App Desk.


Navigation par onglets
----------------------

`Voir le screencast consacré à la navigation par onglets <http://youtu.be/l1TKuP3TomA>`_

Les onglets structurent le travail de l’utilisateur du back-office. Le but est de le faire gagner en productivité, en
limitant les tâches répétitives et les chargement de pages.

On distingue deux types d’onglets :

- **Onglet d’application** : Les onglets d’application n’ont pas de titre, ils sont uniquement représentés par l’icône
  de l’application, en grand. Dans cet onglet, on trouve l’App Desk de l’application (voir plus bas).
- **Onglet d’item** : | depuis l’onglet d’application, on accède à l’édition ou la visualisation d’un item, dans un
  nouvel onglet. Les onglets d’item portent le titre de l’item et l’icône de l’application, en petit.

.. image:: images/ergonomie-tabs.png
	:alt: Navigation par onglets
	:align: center

Les avantages de la navigation par onglets sont multiples. On retiendra :

- plusieurs items d’une même application peuvent être modifiés en parallèle ;
- les aller-retours entre items ou applications sont extrêmement rapides ;
- l’utilisateur reprend son travail là où elle / il l’avait laissé, l’ouverture des onglets étant conservée d’une
  session à une autre.

Les **pop-ups** doivent être limitées au cas modal, c’est-à-dire quand une action doit impérativement être accomplie
(ou annulée) avant que le travail ne puisse se poursuivre (ex : confirmation d’une suppression, ajout d’un lien ou
image à un contenu WYSIWYG).

.. _understand/ergnonomie/app_desk:


L’App Desk
----------

`Voir le screencast consacré à l’App Desk <http://youtu.be/opuOAS_XRrA>`_

L’App Desk est l’accueil d’une application, il permet l’accès aux différents items. Il est constitué des éléments
suivants :

- **Tableau principal** : il liste les items d’une application, une ou plusieurs vues sont proposées (vignettes,
  tableau, arborescence, etc.). Son contenu est filtré par les inspecteurs et / ou une recherche full-text. Il ne peut
  y avoir qu’un seul tableau principal par application.
- **Inspecteurs** : les inspecteurs regroupent les éléments meta d’une application (ex : auteurs pour un blog,
  dossiers pour la médiathèque). Les inspecteurs permettent de filtrer le contenu du tableau principal (ex : voir
  uniquement les billets d’un auteur précis). Certains inspecteurs permettent aussi de gérer des données (ex :
  supprimer un dossier).

	* Inspecteur de prévisualisation : l’inspecteur de prévisualisation est un cas particulier. Contrairement aux
	  autres inspecteurs, il n'agit pas sur le tableau principal, c'est le tableau principal qui agit sur lui : quand
	  un item est sélectionné, ses détails sont affichés dans l'inspecteur de prévisualisation (image, propriétés,
	  récapitulatif des actions possibles pour l’item).

- **Actions** : dans la vaste majorité des cas, chaque App Desk doit proposer une et une seule action principale,
  généralement l’ajout d’un nouvel item. Des actions secondaires peuvent aussi être  proposées, sous forme de liens :
  ajout d’un élément meta (ex : un dossier) ou action fréquente (ex : export).

.. image:: images/ergonomie-app-desk.png
	:alt: App Desk
	:align: center

L’App Desk offre de nombreuses possibilités de mise en page aux développeurs, comme à l’utilisateur final. Néanmoins,
nous recommandons de proposer comme mise en page par défaut une
`Three-Pane Interface <http://en.wikipedia.org/wiki/Three-pane_interface>`_ :

.. image:: images/ergonomie-tpi-fr.png
	:alt: Three-Pane Interface
	:align: center

Alternativement, l’inspecteur de prévisualisation peut être placé sous le tableau principal.