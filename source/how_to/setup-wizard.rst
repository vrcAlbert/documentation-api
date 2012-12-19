Assistant de paramétrage
========================

Les :doc:`fichiers de Novius OS sont installés, le serveur paramétré <install>`, le plus dur est passé, on commence la partie simple :-)

Dans votre navigateur préféré, appelez la page install.php de votre Novius OS et laissez vous guider par l'assistant :

* http://novius-os/install.php si vous avez suivi la procédure d'installation locale
* http://www.votredomaine.com/install.php pour une installation classique sur un serveur externe
* http://www.votrehébergement.com/rep-novius-os/install.php pour une installation dans un sous-répertoire d'un hébergement mutualisé


Étape 1 : vérification des pré-requis
-------------------------------------

Cette étape peut-être une simple formalité si vous avez installé Novius OS sur un hébergement mutualisé. Dans les autres cas, si vous voyez beaucoup de rouge, ne vous inquiétez pas ! Le site a juste besoin de droits en écriture dans certains répertoires. Cette étape vous donne des explications et les commandes à exécuter pour corriger tous les points.

.. image:: /how_to/step-1a.png
	:alt: Étape 1a

Si vous ne voulez pas vous embêter, copiez / collez le résumé des commandes disponibles en bas de la page dans un terminal : c'est fini !

.. image:: /how_to/step-1b.png
	:alt: Étape 1b

Étape 2 : configurer la base de données MySQL
---------------------------------------------

Prérequis à cette étape, avoir crée une base dans MySQL avec un utilisateur associé ayant les droits dessus. Dans le cas d'un hébergement mutualisé, ces paramètres ont dû vous être fournis par votre hébergeur. Dans les autres cas, voici un exemple pour une base en ``localhost``.

.. code-block:: sql

    CREATE DATABASE `nom_de_votre_base` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
    GRANT ALL PRIVILEGES ON `nom_de_votre_base`.* TO 'nom_de_votre_utilisateur'@localhost IDENTIFIED BY 'mot_de_passe';
    FLUSH PRIVILEGES;

Remplissez simplement les 4 champs en fonction de votre configuration. Prenez note que la base de données doit exister, et que vous aurez peut-être besoin de la créer avant de continuer.

.. image:: /how_to/step-2.png
	:alt: Étape 2

Ceci va créer les 2 fichiers *local/config/db.php* et *local/config/crypt.php* et surtout créer les tables nécessaires dans votre base de données.

Étape 3 : créer le premier compte administrateur
------------------------------------------------

.. image:: /how_to/step-3.png
	:alt: Étape 3


Étape 4: terminer l'installation
--------------------------------

.. image:: /how_to/step-4.png
	:alt: Étape 4



Se connecter à Novius OS
------------------------

.. image:: /how_to/step-login.png
	:alt: Écran de connexion

Vous devriez arriver sur le gestionnaire d'applications après votre première connexion (parce que vous êtes administrateur). C'est ici que vous pouvez installer les applications que vous souhaitez utiliser.

.. image:: /how_to/step-appmanager.png
	:alt: Applications manager

* *Blog / News* est une application "librairie" indispensable pour faire fonctionner les applications Blog et Actualités ( *News stories* )
* *Comments* est une application "librairie" fournissant la couche commentaires en front pour faire fonctionner les applications Blog et Actualités
* *Simple Facebook share* et *Simple Twitter share* sont des `Data catchers <http://novius-os.github.com/docs/applications.html#sharing>`_ permettant de partager simplement vos :ref:`Content nuggets <en:sharing_content-nuggets>` sur Facebook et Twitter

Vous voilà dans votre Novius OS. Amusez-vous bien !

