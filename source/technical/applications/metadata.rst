Fichier de configuration ``metadata``
=====================================

Le fichier de configuration ``metadata`` est obligatoire. Il indique au moteur les informations clés dont il a besoin pour utiliser l'application.
Ci-dessous, le fichier ``metadata`` de l'application ``Monkey`` :

.. todo::

	Mettre à jour le metadata en exemple avec la dernière version de Monkey

.. code-block:: php

	<?php
	return array(
		'name'    => 'Monkey : Novius OS Application Bootstrap',
		'version' => '0.2',
		'provider' => array(
			'name' => 'Provider',
		),
		'namespace' => 'Nos\Monkey',
		'permission' => array(),
		'icons' => array(
			16  => 'static/apps/noviusos_monkey/img/16/monkey.png',
			32 => 'static/apps/noviusos_monkey/img/32/monkey.png',
			64    => 'static/apps/noviusos_monkey/img/64/monkey.png',
		),
		'launchers' => array(
			'noviusos_monkey' => array(
				'name'    => 'Monkey',
				'action' => array(
					'action' => 'nosTabs',
					'tab' => array(
						'url' => 'admin/noviusos_monkey/appdesk',
						'iconUrl' => 'static/apps/noviusos_monkey/img/32/monkey.png',
					),
				),
			),
		),
		'enhancers' => array(
			'noviusos_monkey' => array(
				'title' => 'Monkey',
				'desc'  => '',
				//'enhancer' => 'noviusos_monkey/front',
				'urlEnhancer' => 'noviusos_monkey/front/main',
				'iconUrl' => 'static/apps/noviusos_monkey/img/16/monkey.png',
				'dialog' => array(
					'contentUrl' => 'admin/noviusos_monkey/application/popup',
					'width' => 450,
					'height' => 200,
					'ajax' => true,
				),
			),
		),
	);

Le fichier de configuration ``metadata`` retourne un tableau clé => valeur :

* ``name`` : Nom de l'application
* ``version``
* ``provider`` : Tableau clé => valeur donnant des informations sur le fournisseur de l'application
* ``namespace`` : Le ``namespace`` de toutes les classes de l'application
* ``permission`` : Tableau vide. Ajoute une permission globale pour l'application
* ``icons`` : Tableau clé => valeur des icônes de l'application dans différents formats (16 pour 16x16 pixels, 32, 64)
* | ``launchers`` : Tableau clé => valeur de définition des ``launchers`` de l'application (icônes sur le bureau qui ouvrent l'application dans un onglet)
  | La clé est l'identifiant du ``launcher``.
  | La valeur est un tableau clé => valeur de définition du ``launcher``

	* ``name``
	* ``action`` : Tableau clé => valeur de définition de l'action. Voir :doc:`interfaces/actions`.

* ``enhancers`` : Voir :doc:`enhancers`
* ``data-catchers`` : Voir :doc:`/technical/sharing`
* ``template`` : Tableau clé => valeur de définition des gabarits

	.. code-block:: php

		<?php
			'templates' => array(
				'top_menu' => array(
					'file' => 'noviusos_templates_basic::top_menu',
					'title' => 'Default template with a top menu',
					'cols' => 1,
					'rows' => 1,
					'layout' => array(
						'content' => '0,0,1,1',
					),
				),
				// ...
			),

Chaque gabarit peut être séparé en différentes parties. Vous pouvez avoir un gabarit standard où tout est affiché à un seul endroit,
mais vous pouvez aussi avoir des gabarits plus complexes avec un côté droit et un côté gauche par exemple.
L'idée est de fournir ces informations à novius OS pour permettre au moteur de gérer plusieurs WYSIWYGs.
Les WYSIWYGs sont affichés dans une grille : vous pouvez choisir la position et l'echelle de ces WYSIWYGs.

	* ``file`` : Localisation de la vue.
	* ``title`` : Titre du gabarit. Il est utilisé quand vous créez / éditez une page pour choisir son gabarit.
	* ``cols`` : Nombre de colonnes dans la grille.
	* ``rows`` : Nombre de lignes dans la grille.
	* ``layout`` : Disposition des WYSIWYGs dans la grille. Tableau clé => valeur :

		* La clé est l'identifiant du WYSIWYG.
		* La valeur est une chaine, représentant la position gauche, sommet, largeur, hauteur séparés par des virgules (``left``, ``top``, ``width``, ``height``).

