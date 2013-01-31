Installation sur le serveur
###########################

Tout au long de la procédure, nous donnons les commandes dans le cas d'une installation sur Ubuntu. Pensez à les adapter selon votre système d'exploitation.


.. contents::

Télécharger les sources de Novius OS
------------------------------------

Vous avez le choix entre deux méthodes pour récupérer les sources de Novius OS :

* |En utilisant **Git**.
  |Avantage : vous pourrez utiliser Git pour faire les mises à jours du logiciel.
  |A prévilégier si vous installer sur votre machine locale ou un serveur dédié.
* |En téléchargeant le **Zip**.


Via Git et GitHub
^^^^^^^^^^^^^^^^^

Prérequis - Installation de Git
"""""""""""""""""""""""""""""""

Si Git n'est pas installé sur votre machine, voici la commande pour l'installer pour une distribution utilisant ``apt-get`` comme gestionnaire de paquet (ex : Ubuntu)

::

    sudo apt-get install git

Cloner le dépôt
"""""""""""""""

Novius OS utilise les submodules Git, faites attention à bien les récupérer. L'option ``--recursive`` fait le nécessaire.

::

    cd ~
    git clone --recursive git://github.com/novius-os/novius-os.git
    sudo mv novius-os /var/www/

Cette commande télécharge le dépôt d'exemple, avec plusieurs submodules :

* novius-os : le cœur de Novius OS, qui contient lui-même des submodules, comme fuel-core ou fuel-orm ;
* Différents submodules dans local/applications : les applications blog, news et comments



Étape A-3 facultative : Changer la version que vous voulez utiliser (pour les téméraires)
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Le dépôt est configuré pour que lors d'un clone, il pointe vers la dernière version stable (c'est la **master/0.1.4*** au moment de l'écriture de cette page).

| Lorsqu'une nouvelle version est disponible, on la créé dans une branche.
| Pour le moment, tous les dépôts dépendants de novius-os/novius-os sont synchronisés au niveau des numéros de version. C'est-à-dire qu'une application disponible sur notre compte Github suit les mêmes numéros de version que le cœur de Novius OS. Donc si vous utilisez novius-os/core en version 0.3 (qui n'est pas encore sorti !), alors vous devriez aussi utiliser novius-os/app dans le même numéro de version 0.3.

| Pour changer la version que vous voulez utiliser après un clone, *n'oubliez pas de mettre à jour les submodules* !
| Exemple qui utilise la dernière nightly de la branche ``dev`` :

::

    cd /var/www/novius-os/
    git checkout dev
    git submodule update --recursive

.. _install_download-zip:

Méthode B : Depuis un fichier Zip
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    cd ~
    wget http://nova.li/nos-014 -O novius-os.0.1.4.zip
    unzip novius-os.0.1.4.zip
    sudo mv novius-os /var/www/

Ou téléchargez le fichier `nos-014 <http://nova.li/nos-014>`_ et dézippez avec votre logiciel favori.

.. _install_server-configuration:

Étape 2: Configuration du serveur
---------------------------------

Nous allons étudier 2 cas :

* une installation sur un serveur que vous maîtrisé (votre machine locale, une VM ou un serveur externe dédié)
* une installation sur une hébergement mutualisé, donc sans accès à la ligne de commande et au paramétrage Apache


.. _install_server-dedicated:

Méthode A : Vous maîtrisez le serveur
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Nous allons configurer Apache pour accéder au site

Étape A-1 : S'assurer que le `mod_rewrite` d'Apache est activé
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

::

    sudo a2enmod rewrite

Étape A-2: Configurer un `VirtualHost`
""""""""""""""""""""""""""""""""""""""

Créer un ``VirtualHost`` pour Novius OS (remplacer ``nano`` par votre éditeur de texte favori dans les commandes suivantes)

::

    sudo nano /etc/apache2/sites-available/novius-os

Copiez la configuration suivant dans le fichier que vous venez d'ouvrir et sauvegardez. Adaptez la ligne ``ServerName`` avec votre nom de domaine dans le cas d'une installation en production.


::

    <VirtualHost *:80>
        DocumentRoot /var/www/novius-os/public
        ServerName   novius-os
        <Directory /var/www/novius-os/public>
            AllowOverride All
            Options FollowSymLinks
        </Directory>
    </VirtualHost>

La configuration par défaut contient un répertoire ``public``. La racine web doit pointer vers ce répertoire.


Activez votre nouveau ``VirtualHost``

::

    sudo a2ensite novius-os


Relancez ensuite Apache (ou votre autre serveur web) pour prendre en compte la nouvelle configuration.

::

    sudo service apache2 reload


Étape A-3 : Configurer le fichier `hosts`, dans le cas d'installation sur votre machine
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Si le ``ServerName`` est différent de ``localhost`` (``novius-os`` dans l'exemple ci-desssus), vous devez l'ajouter dans votre fichiers ``hosts``.

::

    sudo nano /etc/hosts


Ajouter la ligne suivante :

::

    127.0.0.1   novius-os


.. _install_server-shared:

Méthode B : Hébergement mutualisé
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Étape B-1 : Transférer les sources du logiciel sur le serveur
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Utilisez la méthode de votre choix en fonction des possibilités offertes par votre hébergeur (FTP, SSH, Git...).

Étape B-2 : Fichiers ``.htaccess``
""""""""""""""""""""""""""""""""""

Pour fonctionner Novius OS a besoin d'un fichier ``.htaccess``.

Dans une installation classique, le ``DOCUMENT_ROOT`` doit pointer vers le répertoire ``public`` de Novius OS (voir Étape A-2 au dessus). Dans le cas d'un hébergement mutualisé, vous n'avez pas le choix du ``DOCUMENT_ROOT``. Il faut donc supprimer le fichier ``public/.htaccess`` et renommer le fichier ``.htaccess.shared-hosting`` à la racine de Novius OS en ``.htaccess``.

Éditez ensuite ce fichier ``.htaccess``, modifiez la ligne commençant par ``ErrorDocument`` en adaptant le répertoire d'installation de Novius OS à votre cas :

    ErrorDocument 404 /novius-os-install-dir/public/htdocs/novius-os/404.php

Si Novius OS est installé directement à la racine de votre hébergement :

    ErrorDocument 404 /public/htdocs/novius-os/404.php


Étape B-3 : Fichier ``local/config/config.php``
"""""""""""""""""""""""""""""""""""""""""""""""

Éditez le fichier ``local/config/config.php``, dé-commentez et adaptez la ligne suivante à votre cas

    'base_url' => 'http://www.yourdomain.com/novius-os-install-dir/',


Étape 3 : Terminer l'installation
---------------------------------

Le plus difficile est passé. Il ne reste plus qu'à suivre :doc:`l'assistant de paramétrage <setup-wizard>` pour profiter de votre Novius OS
