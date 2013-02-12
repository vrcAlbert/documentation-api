Créer un gabarit
################



1. Définition dans le fichier :file:`metadata`
==============================================

Les metadata d'un template sont décrites dans la :ref:`documentation d'API <api:metadata/templates>`.


2. Création du fichier de vue
=============================

L'emplacement du fichier dépend de la clé ``file`` configurée dans le fichier :file:`metadata.config.php`.

À l'intérieur du gabarit, vous avez accès à plusieurs variables intéressantes :

- ``$wysiwyg`` est un tableau contenant en clé le nom du WYSIWYG configuré dans le fichier :file:`metadata.config.php`
  et en valeur le contenu saisi dans le back-office ;
- ``$page`` contient l'instance du ``Nos\model_Page`` courant ;
- ``$main_controller`` contient l'instance du contrôleur s'occupant du front-office ;
  :ref:`voir la documentation associée <api:php/classes/controller_front>`.

.. todo::

    Vérifier le lien vers la documenation d'API (le document n'existe pas encore dedans...)


.. code-block:: html

    <!DOCTYPE html>
    <html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <link rel="shortcut icon" href="static/favicon.ico" />
        <link rel="stylesheet" type="text/css" href="static/apps/noviusos_templates_basic/css/base.css" media="all">
    </head>

    <body>

        <header>Cette zone d'entête sera affichée sur toutes les pages configurées avec ce gabarit.</header>

        <div id="menu">
            Mon joli menu
        </div>

        <div id="content">
            <?= $wysiwyg['content']; ?>
        </div>

    </body>
    </html>
