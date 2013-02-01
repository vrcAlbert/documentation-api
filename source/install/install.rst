Installation sur le serveur
###########################

.. contents::
	:depth: 2

Prérequis généraux
******************

* Disposer d'un serveur **LAMP**
* Avoir le mod_rewrite d’Apache est activé

.. note::

	Théoriquement Novius OS peut fonctionner avec un serveur autre qu'**Apache**.

Installation rapide
*******************

Prérequis
---------

* Avoir un accès ligne de commande sur le serveur
* Avoir **Git** installé.

Installation
------------

Ouvrez un terminal et saisissez :

::

    cd /var/www
    sudo wget https://raw.github.com/novius-os/ci/master/0.2/tools/install.sh && sh install.sh

A la question « *Enter the directory name where you want to install Novius OS (default novius-os)* »,
indiquez le nom du répertoire dans lequel vous voulez installer votre instance de Novius OS.
Laissez vide pour l'installer dans un répertoire novius-os.

Une fois l'installation terminée :,

* Ouvrez votre navigateur à l'URL http://votredomaine/novius-os/ (remplacez ``novius-os`` par le nom du répertoire que vous avez saisi).
* Poursuivez l'installation avec :doc:`l'assistant de paramétrage <setup_wizard>`.

.. note::

	* Pour une installation en local, l'URL sera probablement http://localhost/novius-os/ .
	* Si le ``DOCUMENT_ROOT`` de votre serveur n'est pas ``/var/www/`` modifiez la première ligne en conséquence.

Installation sur hébergement mutualisé
**************************************

* Téléchargez  `novius-os.0.1.4.zip <http://nova.li/nos-014>`_.
* Dézippez le fichier.
* Uploadez le répertoire ``novius-os`` sur votre serveur mutualisé (par exemple via FTP).
* Ouvrez votre navigateur à l'URL http://votredomaine/novius-os/ (remplacez ``novius-os`` par le nom du répertoire où vous avez uploadé Novius OS).
* Poursuivez l'installation avec :doc:`l'assistant de paramétrage <setup_wizard>`.


Installation manuelle
*********************

Cette procédure sera détaillé très rapidement.
