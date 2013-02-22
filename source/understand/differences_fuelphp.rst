Différences avec FuelPHP
########################

Chemin des constantes
**********************

Consultez la :ref:`documentation d'API des constantes <api:php/constants>`.

Autoloader
**********

Deux ``namespaces`` sont ajoutés par Novius OS :

:novius-os: pointant vers :ref:`NOSPATH <api:php/constants/NOSPATH>`.
:local: pointant vers :ref:`APPPATH <api:php/constants/APPPATH>`.

Bootstrap et points d'entrées
*****************************

Dans Novius OS, le front-office et le back-office sont deux espaces bien séparés.

Au lieu d'un seul point d'entrée :file:`index.php` de FuelPHP, Novius OS a deux points d'entrée :

* :file:`~/novius-os/htdocs/admin.php` : Point d'entrée du back-office. Traite toutes les URL commençant par :file:`/admin/`.
* :file:`~/novius-os/htdocs/front.php` : Point d'entrée du front-office. Traite toutes les URL finissant par ``.html`` ou la racine de votre site.

Point d'entrée du back-office
=============================

Novius OS a une ``route`` configurée pour son back-office, dont la règle est la suivante :

.. code-block:: php

	<?php
	'routes' => array(
		'^admin/(:segment)/(:any)' => '$1/admin/$2',
	),

Concrètement une URL :file:`admin/noviusos_page/page/insert_update/113` va être transformée en :file:`noviusos_page/admin/page/insert_update/113`.
Ce qui correspond à exécuter la méthode ``action_insert_update`` du ``controller`` ``Controller_Admin_Page`` de l'application ``noviusos_page``.

.. seealso::

	`Documentation de FuelPHP sur le routing <http://fuelphp.com/docs/general/routing.html>`__.
