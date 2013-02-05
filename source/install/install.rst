Installation
############

.. contents::
	:depth: 2
	:backlinks: top
	:local:

Prérequis généraux
******************

* Disposer d'un serveur :program:`LAMP` avec PHP 5.3+.
	.. code-block:: bash

			sudo apt-get install apache2 php5 mysql-server libapache2-mod-php5 php5-mysql

* Avoir le **mod_rewrite** d’:program:`Apache` est activé.
	.. code-block:: bash

			sudo a2enmod rewrite

| Les commandes sont données à titre d'exemple si vous installez Novius OS sur votre machine locale ou un serveur sur lequel vous avez les droits d'administration.
| Elles sont valables pour installation sur Ubuntu, adaptez-les en fonction de votre distribution.


.. note::

	Théoriquement Novius OS peut fonctionner avec un serveur autre qu':program:`Apache`.

Installation rapide
*******************

Prérequis
=========

* Avoir un accès ligne de commande sur le serveur et disposer des droits d'administation :command:`sudo`.
* Avoir :program:`Git` installé.

Installation
============

Ouvrez un terminal et saisissez :

.. code-block:: bash

    cd /var/www
    sudo wget https://raw.github.com/novius-os/ci/master/0.2/tools/install.sh && sh install.sh

À la question :guilabel:`« Enter the directory name where you want to install Novius OS (default novius-os) »`,
indiquez le nom du répertoire dans lequel vous voulez installer votre instance de Novius OS.
Laissez vide pour l'installer dans un répertoire :file:`novius-os`.

Une fois l'installation terminée :

* Ouvrez votre navigateur à l'URL :file:`http://votredomaine/novius-os/` (remplacez :file:`novius-os` par le nom du répertoire que vous avez saisi).
* Poursuivez l'installation avec :doc:`l'assistant de paramétrage <setup_wizard>`.

.. note::

	* Pour une installation en local, l'URL sera probablement :file:`http://localhost/novius-os/`.
	* Si le ``DOCUMENT_ROOT`` de votre serveur n'est pas :file:`/var/www/`, modifiez la première ligne en conséquence.

Installation via Zip
********************

Cette procédure est à privilégier si vous souhaitez installer Novius OS sur un hébergement mutualisé :

* Téléchargez  `novius-os.0.2.zip <http://www.novius-os.org/download-novius-os-zip.html>`_.
* Dézippez le fichier.
* Uploadez (ou déplacer) le répertoire :file:`novius-os` dans le ``DOCUMENT_ROOT`` de votre serveur (par exemple via FTP).
* Ouvrez votre navigateur à l'URL :file:`http://votredomaine/novius-os/` (remplacez :file:`novius-os` par le nom du répertoire où vous avez dézippé Novius OS).
* Poursuivez l'installation avec :doc:`l'assistant de paramétrage <setup_wizard>`.


Installation avancée
********************

Configuration d'un Virtual Host
===============================

Les commandes suivantes sont données à titre d'exemple si vous voulez installer Novius OS sur Ubuntu, adaptez les en fonction de votre distribution.

.. code-block:: bash

	sudo nano /etc/apache2/sites-available/novius-os

| Remplacez :command:`nano` par n'importe quel autre éditeur de texte.
| Remplacez ``novius-os`` par le nom que vous voulez donner à votre ``Virtual Host``

| Copiez la configuration suivant dans le fichier que vous venez d'ouvrir et sauvegardez.
| Adaptez la ligne ``ServerName`` avec votre nom de domaine dans le cas d'une installation en production.
| De même, remplacez :file:`/var/www/novius-os` par le répertoire dans lequel vous avez installé Novius OS.

.. code-block:: apache

	<VirtualHost *:80>
		DocumentRoot /var/www/novius-os/public
		ServerName   novius-os
		<Directory /var/www/novius-os/public>
			AllowOverride All
			Options FollowSymLinks
		</Directory>
	</VirtualHost>

La configuration par défaut contient un répertoire public. La racine web doit pointer vers ce répertoire.

Activez votre nouveau VirtualHost

.. code-block:: bash

	sudo a2ensite novius-os

Relancez ensuite Apache pour prendre en compte la nouvelle configuration.

.. code-block:: bash

	sudo service apache2 reload

Configurer le fichier hosts, dans le cas d'installation sur votre machine
-------------------------------------------------------------------------

Si vous installez Novius OS sur votre machine locale, la valeur du ``ServerName`` (``novius-os`` dans l'exemple ci-desssus) doit être ajoutée dans votre fichiers :file:`/etc/hosts`.

.. code-block:: bash

	sudo nano /etc/hosts

Ajouter la ligne suivante :

.. code-block:: bash

	127.0.0.1   novius-os

Installation avancée avec Git
=============================

Pour cloner Novius OS :

.. code-block:: bash

	git clone --recursive git://github.com/novius-os/novius-os.git

Cette commande télécharge le dépôt principal, avec plusieurs submodules :

* novius-os : le cœur de Novius OS, qui contient lui-même des submodules, comme fuel-core ou fuel-orm.
* Différents submodules dans :file:`local/applications` : les applications blog, news, comments, form, slideshow...

| Le dépôt est configuré pour que lors d'un clone, il pointe vers la dernière version stable.
| Lorsqu'une nouvelle version est disponible, on la créé dans une branche.

| Pour le moment, tous les dépôts dépendants de novius-os/novius-os sont synchronisés au niveau des numéros de version.
  C'est-à-dire qu'une application disponible sur notre compte Github suit les mêmes numéros de version que le cœur de Novius OS.
  Donc si vous utilisez ``novius-os/core`` en version |version|, alors vous devriez aussi utiliser ``novius-os/app`` dans le même numéro de version |version|.

| Pour changer la version que vous voulez utiliser après un clone, n'oubliez pas de mettre à jour les submodules !
| Exemple qui utilise la dernière nightly de la branche ``dev`` :

.. code-block:: bash

	cd /var/www/novius-os/
	git checkout dev
	git submodule update --recursive
