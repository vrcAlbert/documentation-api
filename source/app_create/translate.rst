Traduire l'application
######################


Chaque application possède un répertoire :file:`lang` dans lequel sont placés les fichiers de traductions, qu'on
appellera **dictionnaires**.

Ce répertoire contient autant de sous-répertoires que de langues dans lesquelles on veut traduire notre application, et
qui contiennent eux-même les dictionnaires.

Ces répertoires de langues portent des noms de locales, comme par exemple :file:`fr` (Français), ou :file:`en` (Anglais).

Les dictionnaires sont des fichiers PHP qui retournent un tableau PHP, un peu comme les fichiers de configuration.


Fichier :file:`metadata.config.php`
===================================

Les ``metadata`` étant un peu spéciales, elles nécessitent un fichier de traduction à part. La première étape est
d'indiquer dans quel dictionnaire se trouvent les traductions du fichier :file:`metadata.config.php`.

.. code-block:: php
   :emphasize-lines: 6

    <?php

    return array(
        'name' => 'My app',
        'namespace' => 'My\App',
        'i18n_file' => 'my_app::metadata',
        // ... autres clés
    );

Comme toute modification sur les :file:`metadata`, ne pas oublier d'appliquer les changements dans le gestionnaire
d'applications.

Ensuite, il faut créer le dictionnaire :file:`my_app::lang/fr/metadata.lang.php` :

.. code-block:: php

    <?php

    return array(
        'My app' => 'Mon appli',
    );

Novius OS sait automatiquement quelles clés peuvent / ont besoin d'être traduites dans le fichier :file:`metadata` et
ira chercher les traductions correspondantes.


Autres fichiers
===============


Partout ailleurs, le mécanisme à utiliser pour rendre les fichiers sources traduisibles est le suivant :

1. Utiliser la fonction :func:`__` pour récupérer la traduction ;
2. Pour chaque fichier, configurer dans quel dictionnaire sont situées les traductions.


C'est assez simple pour les vues et la configuration :

.. code-block:: php

    <?php

    // Configure la fonction __() pour le reste du fichier
    Nos\I18n::current_dictionary('my_app::common');

    __('Translate this'); // La traduction sera récupérée depuis my_app::lang/<lang>/common.lang.php


C'est plus pointu pour les contrôleurs, car la langue dépend de l'utilisateur et n'est connue qu'après la phase
d'authentification, qui a lieu dans le ``before()``.

C'est pourquoi un point d'entrée ``prepare_i18n()`` a été créé :


.. code-block:: php
   :emphasize-lines: 9-12

    <?php

    namespace Nos\Form;

    class Controller_Admin_Form extends \Nos\Controller_Admin_Crud
    {
        public function prepare_i18n()
        {
            // Configure la langue des fichiers de traductions en fonction de l'utilisateur connecté
            parent::prepare_i18n();
            // Configure la fonction __() pour le reste du contrôleur
            \Nos\I18n::current_dictionary('noviusos_form::common');
        }

        // Autres méthodes qui font usage de __()
    }


Il est possible de spécifier plusieurs dictionnaires pour un fichier en utilisant un tableau. Les traductions seront
alors récupérés dans le premier fichier qui contient la traduction.


.. code-block:: php
   :emphasize-lines: 3

    <?php

    Nos\I18n::current_dictionary(array('my_app::dictionary', 'my_app::common'));

    // La traduction sera récupérée depuis my_app::lang/<lang>/dictionary.lang.php si elle existe
    // Ou dans my_app::lang/<lang>/common.lang.php sinon
    __('Translate this');