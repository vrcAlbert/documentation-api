Multi-Contextes
***************

| Novius OS peut nativement gérer plusieurs sites, chacun de ces sites pouvant avoir plusieurs versions linguistiques.
| Un contexte est un binome site / langue.

Exemple
=======

Votre instance de Novius OS peut gérer votre site vitrine qui se décline en 3 langues (français, anglais et espagnol),
votre site pour mobile disponible qu'en français, et un site événementiel en anglais.

============= ======== ======= ========
Site / Langue Français Anglais Espagnol
============= ======== ======= ========
Vitrine       X        X       X
Mobile        X
Événementiel           X
============= ======== ======= ========

Votre instance Novius OS gérera alors **5** contextes :

* Vitrine / Français
* Vitrine / Anglais
* Vitrine / Espagnol
* Mobile / Français
* Événementiel / Anglais

.. _multi-context-configuration:

Configuration
=============

Pour modifier les contextes de votre instance de Novius OS, éditez le fichier ``local/config/contexts.config.php``.

Après l'installation, Novius OS est configuré avec 3 contextes, 1 site + 3 langues :

.. code-block:: php

	return array(
		'sites' => array(
			'main' => array(
				'title' => 'Main site',
				'alias' => 'Main',
			),
		),

		'locales' => array(
			'fr_FR' => array(
				'title' => 'Français',
				'flag' => 'fr',
			),
			'en_GB' => array(
				'title' => 'English',
				'flag' => 'gb',
			),
			'ja_JP' => array(
				'title' => '日本語',
				'flag' => 'jp',
			),
		),

		'contexts' => array(
			'main::en_GB' => array(),
			'main::fr_FR' => array(),
			'main::ja_JP' => array(),
		),
	);

Voici comment modifier le fichier pour appliquer la configuration décrite dans l'exemple d'introduction :

.. code-block:: php

	return array(
		'sites' => array(
			'vitrine' => array(
				'title' => 'Site vitrine',
				'alias' => 'Vitrine',
			),
			'mobile' => array(
				'title' => 'Site mobile',
				'alias' => 'Mobile',
			),
			'event' => array(
				'title' => 'Site événementiel',
				'alias' => 'Event',
			),
		),

		'locales' => array(
			'fr_FR' => array(
				'title' => 'Français',
				'flag' => 'fr',
			),
			'en_GB' => array(
				'title' => 'English',
				'flag' => 'gb',
			),
			'es_ES' => array(
				'title' => 'Español',
				'flag' => 'es',
			),
		),

		'contexts' => array(
			'vitrine::fr_FR' => array(),
			'vitrine::en_GB' => array(),
			'vitrine::es_ES' => array(),
			'mobile::fr_FR' => array(),
			'event::en_GB' => array(),
		),
	);


Nom de domaine
==============

| Dans la configuration ci-dessus, votre instance de Novius OS va gérer 5 contextes mais tous sur le même nom de domaine.
| Si votre nom de domaine est ``www.monsite.fr``, vos contextes s'afficheront sur ces URLs :

* La version française du site vitrine sur ``www.monsite.fr/``. C'est le premier contexte, il répond donc sur la racine de votre nom de domaine.
* La version anglaise du site vitrine sur ``www.monsite.fr/vitrine/en_GB/``.
* La version espagnole du site vitrine sur ``www.monsite.fr/vitrine/es_ES/``.
* La version française du site mobile sur ``www.monsite.fr/mobile/fr_FR/``.
* La version anglaise du site événementiel sur ``www.monsite.fr/event/en_GB/``.

Contexte sur sous-répertoire
----------------------------

Peut-être que se fonctionnement vous conviendra. Mais si ça n'est pas le cas vous pouvez facilement le changer en modifiant ainsi la clé ``contexts`` de votre configuration :

.. code-block:: php

	'contexts' => array(
		'vitrine::fr_FR' => array(),
		'vitrine::en_GB' => array(
			'http://www.monsite.fr/en/',
		),
		'vitrine::es_ES' => array(
			'http://www.monsite.fr/es/',
		),
		'mobile::fr_FR' => array(
			'http://www.monsite.fr/mobile/',
		),
		'event::en_GB' => array(
			'http://www.monsite.fr/event/',
		),
	),

De cette façon votre site vitrine français répondra toujours sur la racine de votre nom de domaine mais les autres contextes auront une URL plus courte.

.. note::

	Attention ! Si votre contexte principal a une page ``en/exemple.html`` et que votre contexte ``'vitrine::en_GB'`` a une page ``exemple.html``, leur URLs seront identiques
	(``http://www.monsite.fr/en/exemple.html``). Seul la page du contexte principal sera accessible.

Contexte sur domaine
--------------------

Mais vous pouvez aussi avoir un domaine pour chacun de vos contextes (il faut bien entendu configurer les domaines dans Apache) :

.. code-block:: php

	'contexts' => array(
		'vitrine::fr_FR' => array(
			'http://www.monsite.fr/',
		),
		'vitrine::en_GB' => array(
			'http://www.monsite.en/',
		),
		'vitrine::es_ES' => array(
			'http://www.monsite.es/',
		),
		'mobile::fr_FR' => array(
			'http://mobile.monsite.fr/',
		),
		'event::en_GB' => array(
			'http://event.monsite.en/',
		),
	),

Contexte avec plusieurs URLs
----------------------------

Pour finir, vous pouvez avoir plusieurs domaines (ou sous-répertoires de domaine) pour un contexte :

.. code-block:: php

	'contexts' => array(
		'vitrine::fr_FR' => array(
			'http://www.monsite.fr/',
		),
		'vitrine::en_GB' => array(
			'http://www.monsite.en/',
		),
		'vitrine::es_ES' => array(
			'http://www.monsite.es/',
		),
		'mobile::fr_FR' => array(
			'http://mobile.monsite.fr/',
			'http://www.monsite-mobile.fr/',
			'http://www.monsite.fr/mobile/',
		),
		'event::en_GB' => array(
			'http://event.monsite.en/',
		),
	),

Dans ce cas la première entrée du tableau est considérée comme celle par défaut. C'est, par exemple, cette URL qui sera utilisée par le back-office pour visualiser une page.


Gestion de l'environnement
--------------------------

En environnement de développement, la gestion automatique de vos contextes par sous-répertoires vous convient peut-être parfaitement.
Par contre vous voulez définir des domaines en environnement de production.

Pour cela nous allons utiliser le `système d'evironnement de FuelPHP <http://fuelphp.com/docs/general/environments.html>`_.

* Renseignez le fichier ``local/config/contexts.config.php`` comme expliqué dans :ref:`multi-context-configuration`.
* S'il n'existe pas, créez un répertoire ``local/config/production/`` et créez un fichier ``contexts.config.php`` à l'intérieur.
* Saisissez le contenu suivant (à adapter selon vos désirs) :

.. code-block:: php

	return array(
		'contexts' => array(
			'vitrine::fr_FR' => array(
				'http://www.monsite.fr/',
			),
			'vitrine::en_GB' => array(
				'http://www.monsite.en/',
			),
			'vitrine::es_ES' => array(
				'http://www.monsite.es/',
			),
			'mobile::fr_FR' => array(
				'http://mobile.monsite.fr/',
				'http://www.monsite-mobile.fr/',
				'http://www.monsite.fr/mobile/',
			),
			'event::en_GB' => array(
				'http://event.monsite.en/',
			),
		),
	);

De cette façon, en production les deux configurations seront fusionnées alors qu'en développement seul le premier fichier sera utilisé.

Ajouter des contextes
=====================

Vous pouvez ajouter à n'importe quel moment de nouveaux contextes, sites ou langues à votre configuration.
Modifiez simplement votre fichier ``contexts.config.php`` comme expliqué ci-dessus, les nouveaux contextes sont aussitôt pris en compte.