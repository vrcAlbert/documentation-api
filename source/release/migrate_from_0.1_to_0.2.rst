Guide de migration de la version 0.1 à la version 0.2
#####################################################

Changements non rétro-compatibles obligatoires
**********************************************

Conséquences du passage de multi-languages à multi-contextes
============================================================

	* La configuration se fait dans un fichier dédié (plus dans ``config.php``). Deux nouvelles clé ``contexts`` et ``sites`` en plus de ``locales``
	* Toutes les colonnes ``lang``, ``lang_common_id``, ``lang_is_main`` de la base de données ont été renommées avec ``context``
	* Les nouvelles colonnes ``context`` ont été agrandies, de 5 à 25 caractères
	* Le ``behaviour`` ``Translatable`` a été renommé en ``Twinnable``
	* Dans le ``CRUD``, la notion de ``context`` est remplacée celle d'``environment`` pour éviter les confusions (``context_relation`` -> ``environment_relation``, ``item_context`` -> ``item_environment``)
	* Toutes les variables liées ont, elles aussi, été renommées

Modification de l'API des pages
===============================

	* ``Model_Page->get_link()`` -> ``Model_Page->link()``
	* ``Model_Page->get_href()`` -> ``Model_Page->url()``
	* ``Model_Page::get_url()`` -> ``Tools_Url::page()``
	* Suppression de ``Model_Page::get_url_absolute()``
	* Toutes les méthodes retournent des URLs absolues

Procédure à suivre
==================

* Créer le fichier ``contexts.config.php`` (se baser sur le sample).
* Modifier ``config.php`` pour rajouter la clé ``novius-os`` (se baser sur le sample).

* Rechercher ``_lang`` et remplacer par ``_context`` (c-à-d ``page_lang => page_context``)
* Rechercher ``Nos\Model_`` et remplacer par ``Nos\{{app}}\Model_`` (c-à-d ``Nos\Model_Page => Nos\Page\Model_Page``, ``Nos\Model_Media => Nos\Media\Model_Media``)
* Rechercher ``Translatable`` et remplacer par ``Contextable``
* Rechercher  ``Model_Page->get_link()`` et remplacer par ``Model_Page->link()``
* Rechercher ``Model_Page->get_href()`` et remplacer par ``Model_Page->url()``
* Rechercher ``Model_Page::get_url()`` et remplacer par ``Tools_Url::page()``


Changement dans les applications
********************************

Metadata
========


* Launchers : la clé ``url`` a été remplacée par ``action`` (syntaxe standard nosAction)
* Launchers : la clé ``icon64`` a été remplacée par ``icon``

.. code-block:: php

	<?php

	return array(
	    'launcher_name' => array(
	        'url' => '{{your_url_here}}',
	    ),
	);

	// Replace with

	return array(
	    'launcher_name' => array(
	        'action' => array(
	            'action' => 'nosTabs',
	            'tab' => array(
	                'url' => '{{your_url_here}}',
	            ),
	        ),
	    ),
	);


* L'application fournit désormais une liste d'icônes :

.. code-block:: php

    <?php

    return array(
        'icons' => array(
            64 => 'static/apps/noviusos_page/img/64/page.png',
            32 => 'static/apps/noviusos_page/img/32/page.png',
            16 => 'static/apps/noviusos_page/img/16/page.png',
        ),
    );

* Un launcher sans ``icon`` utilisera l'icône 64 de son applicaton
* Un onglet (``tab``) sans ``iconUrl`` utilisera l'icône 32 de son applicaton
* Un enhancer sans ``iconUrl`` utilisera l'icône 16 de son applicaton


Configuration des CRUD
======================

* ``widget`` a été renommé en ``renderer``


.. code-block:: php

    <?php

    return array(
        'field_name' => array(
            'widget' => 'Nos\Widget_Media',
            'widget_options' => array(),
        ),
    );

    // À remplacer par :
    return array(
        'field_name' => array(
            'renderer' => 'Nos\Renderer_Media',
            'renderer_options' => array(),
        ),
    );


Migration "complète" 0.2
************************


Cette partie se base sur l'existence d'une hypothétique application ``lib_agenda``.


Appdesk
=======

Les modèles possèdent un nouveau fichier de configuration ``common`` qui contient :
* un ``data_mapping``
* une liste d'``actions``

Dans ``appdesk.config.php`` :

* Supprimer les clés ``selectedView`` et ``views`` (si vous n'avez qu'une seule vue sans fichier de conf JS).
* Repérez le modèle principale de votre appdesk (clé ``query.model``).
* Créez le ficher common associé ``config/common/{{model_name}}.config.php``
    * ``{{model_name}}`` correspond au nom du model en minuscule, sans le préfixe ``Model_``, par exemple ``Model_Page`` devient ``page``
    * ``Model_Page`` correspond donc au fichier ``config/common/page.config.php``


Note :

* Attention à bien avoir ``'hideContexts' => true,`` dans la configuration de votre appdesk si vos élements ne sont pas ``Contextable``.


Data mapping
------------

Le ``data_mapping`` correspond à la fusion du ``dataset`` et de ``appdesk.grid.columns``


.. code-block:: php
   :emphasize-lines: 6,11-21,29-49

    <?php

    // Ancien code de appdesk.config.php
    return array(
        'query' => array(
            'model' => 'Lib\Agenda\Model_Event',
            'order_by' => array('evt_date_begin' => 'DESC'),
            'limit' => 20,
        ),
        // ...
        'dataset' => array(
            'id'            => 'evt_id',
            'title'         => 'evt_title',
            'periode'       => array(
                'search_column' => 'evt_date_begin',
                'dataType'      => 'datetime',
                'value'         => function ($object) {
                    // ...
                },
            },
        ),
        // ...
        'appdesk' => array(
            // ...
            'grid' => array(
                'urlJson' => 'admin/lib_agenda/appdesk/json',
                'columns' => array(
                    'id' => array(
                        'headerText' => __('Id'),
                        'dataKey' => 'id'
                    ),
                    'title' => array(
                        'headerText' => __('Nom'),
                        'dataKey' => 'title'
                    ),
                    'periode' => array(
                        'headerText' => __('Dates'),
                        'dataKey' => 'periode'
                    ),
                    'published' => array(
                        'headerText' => __('Status'),
                        'dataKey' => 'publication_status'
                    ),
                    'actions' => array(
                        'actions' => array('update', 'delete'),
                    ),
                ),
            ),
            // ...
        ),
    );


.. code-block:: php
   :emphasize-lines: 12,16

    <?php

    // Nouveau code de appdesk.config.php
    return array(
        'query' => array(
            'order_by' => array('evt_date_begin' => 'DESC'),
            'limit' => 20,
        ),
        // Indique quel est le model, et donc quel fichier 'common' charger
        'model' => 'Lib\Agenda\Model_Event',
        // ...
        // DEPLACER / FUSIONNER la clé 'dataset' dans common
        // ...
        'appdesk' => array(
            // ...
            // DEPLACER / FUSIONNER la clé 'grid' dans common
            // ...
        ),
    );


.. code-block:: php
   :emphasize-lines: 5

    <?php

    // Code du nouveau fichier ``event.config.php``
    return array(
        // Fusion de 'appdesk.dataset' et de 'appdesk.grid.columns'
        'data_mapping' => array(
            'id' => array(
                'title' => __('Id'),
                'column' => 'evt_id'
            ),
            'title' => array(
                'title' => __('Nom'),
                'column' => 'evt_title'
            ),
            'periode' => array(
                'title' => __('Dates'),
                'search_column' => 'evt_date_begin',
                'value'         => function ($object) {
                    // ...
                }
            ),
            'published' => array(
                'title' => __('Status'),
                'method' => 'publication_status'
            ),
        ),
    );

Quelques notes :
* ``headerText`` peut s'écrire ``title`` (plus facile / simple à retenir, utilisé dans les applis natives)
* ``datakey`` peut s'écrire ``column``
* ``value`` est toujours possible pour une fonction de callback
* ``method`` est une nouvelle option qui exécute une méthode au lieu de récupérer une ``column``



Actions
-------

Les actions sur le modèle principal (celui de la grid de l'appdesk) doivent également être déplacées dans le fichier common.

.. code-block:: php
   :emphasize-lines: 8-16

    <?php

    // Ancien code de appdesk.config.php
    return array(
        // ...
        'appdesk' => array(
            // ...
            // DEPLACER la clé 'actions' dans 'config/common/{{model_name}}.config.php'
            'actions' => array(
                'edit' => array(
                    // ...
                ),
                'delete' => array(
                    // ...
                ),
            ),
            // ...
        ),
        // ...
    );

.. code-block:: php
   :emphasize-lines: 8

    <?php

    // Nouveau code de appdesk.config.php
    return array(
        // ...
        'appdesk' => array(
            // ...
            // La clé 'actions' n'est plus ici
            // ...
        ),
        // ...
    );


.. code-block:: php
   :emphasize-lines: 9-17

    <?php

    // Nouveau code de 'config/common/event.config.php'
    return array(
        'data_mapping' => array(
            // ...
        ),

        // Tableau de configuration déplacé depuis 'appdesk.actions'
        'actions' => array(
            'Lib\Agenda\Model_Event.edit' => array(
                // ...
            ),
            'Lib\Agenda\Model_Event.delete' => array(
                // ...
            ),
        ),
    );



À partir du moment où le fichier ``common`` est utilisé, les actions génériques suivantes apparaissent :
* ``add``
* ``edit`` (et non pas ``update`` !)
* ``visualise`` (si approprié, c-à-d si le modèle possède le Behaviour Urlrnhancer)
* ``delete``
* ``share`` (si approprié)


Dans le cas de l'agenda et de ``Model_Event`` ce dernier possédait une action ``update`` qui apparait désormais en double... (parce qu'on avait mis le mauvais nom ``update`` au lieu de ``edit``).

Du coup, **dans le cas de l'agenda**, il faut :
* Renommer ``update`` en ``edit``
* Etant donné que les actions ``edit`` et ``delete`` font le traiement par défaut, **supprimer** les clés...
* Il est possible de garder uniquement les clés à redéfinir (pour les textes français dans ce cas...)

Notes :
* Dans la version de NOS utilisée, il faut préfixer les actions par le nom du modèle, ce n'est plus nécessaire dans la version finale
* ``{{controller_base_url}}`` est utilisable dans les URL d'actions. Dans le cas d'agenda, il sera remplacé par ``lib_agenda/admin/agenda/``
* Une nouvelle clé ``targets`` permet de définir où les actions doivent apparaître (cf. commentaires).

.. code-block:: php

    <?php

    // Exemple de placeholder {{controller_base_url}} + 'targets'
    array(
        'Lib\Agenda\Model_Event.edit' => array(
            'action' =>
                'action' => 'nosTabs',
                'tab' => array(
                    'url' => "{{controller_base_url}}insert_update/{{id}}",
                    'label' => __('Modifier'),
                ),
            ),
            'label' => __('Modifier'),
            'primary' => true,
            'icon' => 'pencil',
            // Nouvelle clé pour définir où cette action apparait
            'targets' => array(
                'grid' => true, // Dans la grid (dans la dernière colonne 'actions')
                'toolbar-grid' => true, // Sur l'appdesk, dans la toolbar (anciennement configuré via 'appdesk.button')
                'toolbar-edit' => true, // Sur le formulaire d'édition (en haut à droite)
            ),
        )
    );


Par défaut, les targets sont configurés comme suit pour les actions :
* ``grid`` : edit + visualise + delete
* ``toolbar-grid`` : add
* ``toolbar-edit`` : visualise + share + delete

Note : pour l'instant, ``appdesk.appdesk.buttons`` est toujours défini, il prend donc la main sur la configuration par défaut. Sachant que nous avons à la fois 'Ajouter un évènement' et 'Ajouter une catégorie', on ne peut pas (encore) le supprimer tout de suite.



I18N et traductions
-------------------

Les textes sont configurables via la clé ``i18n``.

Se référer à la documentation, ou (en attendant) au fichier ``framework/config/common_i18n.config.php`` pour la liste des clés possibles.

.. code-block:: php

    <?php

    return array(
        'i18n' => array(
            // Crud
            'notification item added' => __('And voilà! The page has been added.'),
            'notification item deleted' => __('The page has been deleted.'),

            // General errors
            'notification item does not exist anymore' => __('This page doesn’t exist any more. It has been deleted.'),
            'notification item not found' => __('We cannot find this page.'),

            // Blank slate
            'translate error parent not available in context' => __('We’re afraid this page cannot be added in {{context}} because its <a>parent</a> is not available in this context yet.'),
            'translate error parent not available in language' => __('We’re afraid this page cannot be added in {{language}} because its <a>parent</a> is not available in this language yet.'),

            // Deletion popup
            'deleting item title' => __('Deleting the page ‘{{title}}’'),

            # Delete action's labels
            'deleting button 1 item' => __('Yes, delete this page'),
            'deleting button N items' => __('Yes, delete these {{count}} pages'),

            '1 item' => __('1 page'),
            'N items' => __('{{count}} pages'),

            # Keep only if the model has the behaviour Contextable
            'deleting with N contexts' => __('This page exists in <strong>{{context_count}} contexts</strong>.'),
            'deleting with N languages' => __('This page exists in <strong>{{language_count}} languages</strong>.'),

            # Keep only if the model has the behaviours Contextable + Tree
            'deleting with N contexts and N children' => __('This page exists in <strong>{{context_count}} contexts</strong> and has <strong>{{children_count}} sub-pages</strong>.'),
            'deleting with N contexts and 1 child' => __('This page exists in <strong>{{context_count}} contexts</strong> and has <strong>one sub-page</strong>.'),
            'deleting with N languages and N children' => __('This page exists in <strong>{{language_count}} languages</strong> and has <strong>{{children_count}} sub-pages</strong>.'),
            'deleting with N languages and 1 child' => __('This page exists in <strong>{{language_count}} languages</strong> and has <strong>one sub-page</strong>.'),

            # Keep only if the model has the behaviour Tree
            'deleting with 1 child' => __('This page has <strong>1 sub-page</strong>.'),
            'deleting with N children' => __('This page has <strong>{{children_count}} sub-pages</strong>.'),
        ),
    );


Inspecteurs
-----------

En 0.1, les inspecteurs sont configurés à 3 endroits :
* La clé ``appdesk.appdesk.inspectors``
* La clé ``inputs``
* Le fichier de configuration ``inspector/{{model}}.config.php``

EN 0.2, les ``inputs`` doivent désormais être déplacé dans leur fichier ``inspector/{{model}}.config.php`` correspondant.



Category
^^^^^^^^

.. code-block:: php
   :emphasize-lines: 7-11

    <?php

    // Ancien code dans appdesk.config.php
    return array(
        // ...
        'inputs' => array(
            // Cet input correspond au filtre pour l'inspecteur catégorie
            // On déplace la clé (evt_cat_id) dans 'input.key' et la fonction de callback dans 'input.query'
            'evt_cat_id' => function($value, $query) {
                // ...
            },
        ),
        // ...
    );


.. code-block:: php

    <?php

    // Nouveau code dans config/controller/admin/inspector/category.config.php
    return array(
        // ...
        'input' => array(
            'key' => 'evt_cat_id',
            'query' => function($value, $query) {
                // ...
            },
        ),
        // ...
    );


Date
^^^^

.. code-block:: php

    <?php

    // Ancien code dans appdesk.config.php
    return array(
        // ...
        'appdesk' => array(
            'appdesk' => array(
                // ...
                'inspectors' => array(
                    // Il faut déplacer ce tableu dans le fichier de configuration de l'inspecteur, sous une nouvelle clé 'appdesk'
                    'startdate' => array(
                        'label' => __('Date de début'),
                        'url' => 'admin/lib_agenda/inspector/date/list',
                        'inputName' => 'startdate',
                        'vertical' => true
                    ),
                    // ...
                ),
            ),
            // ...
        ),
    );


Ici l'inspecteur date n'a pas encore de fichier de configuration, on va en créer un :


.. code-block:: php

    <?php

    // Nouveau fichier config/controller/admin/inspector/date.config.php
    return array(
        'input' => array(
            'key' => 'evt_date_begin',
            // Pas besoin de 'query', l'inspecteur date en génère un automatiquement en fonction de la key
        ),

        // Reprise de 'appdesk.appdesk.inspectors.startdate'
        'appdesk' => array(
            'label' => __('Date de début'),
        ),
    );


L'idée est d'encapsuler le tableau ``appdesk.appdesk.inspectors.{{inspector_name}}`` dans une clé ``appdesk`` du fichier de config de l'inspecteur.

published
^^^^^^^^^

.. code-block:: php

    <?php

    // Ancien code dans appdesk.config.php
    return array(
        // ...
        'inputs' => array(
            // ...
            'evt_published' => function($value, $query) {
                // ...
            },
        ),
        // ...
        'appdesk' => array(
            'appdesk' => array(
                // ...
                'inspectors' => array(
                    'published' => array(
                        'vertical' => true,
                        'url' => 'admin/lib_agenda/inspector/published/list',
                        'inputName' => 'evt_published',
                        'grid' => array(
                            'columns' => array(
                                'title' => array(
                                    'visible' => false,
                                    'dataKey' => 'title',
                                ),
                                'icon_title' => array(
                                    'headerText' => __('Status'),
                                    'dataKey' => 'icon_title',
                                ),
                                'id' => array(
                                    'visible' => false,
                                    'dataKey' => 'id',
                                ),
                            ),
                        ),
                    ),
                    // ...
                ),
                // ...
            ),
            // ...
        ),
    );


L'inspecteur ``published`` a déjà un fichier de configuration, complétons le en créant une nouvelle clé ``appdesk`` :


.. code-block:: php
   :emphasize-lines: 8,16

    <?php

    // Nouveau fichier config/controller/admin/inspector/date.config.php
    return array(
        'data' => array(
            // ...
        ),

        // Ici on reprend 'appdesk.appdesk.inspectors.published'
        'input' => array(
            'key' => 'evt_published',
            'query' => function($value, $query) {
                // ...
            },
        ),

        // Ici on reprend 'input.evt_published'
        'appdesk' => array(
            'vertical' => true,
            'inputName' => 'evt_published',
            'url' => 'admin/lib_agenda/inspector/published/list',
            'grid' => array(
                'columns' => array(
                    'title' => array(
                        'visible' => false,
                        'dataKey' => 'title',
                    ),
                    'icon_title' => array(
                        'headerText' => __('Status'),
                        'dataKey' => 'icon_title',
                    ),
                    'id' => array(
                        'visible' => false,
                        'dataKey' => 'id',
                    ),
                ),
            ),
        ),
    );







