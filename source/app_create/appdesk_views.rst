Ajouter des vignettes dans l'App Desk
#####################################


C'est en réalité très simple. Il faut définit deux clés spéciales dans votre ``data_mapping`` :

- ``thumbnail`` : chemin vers la vignette de l'item ;
- ``thumbnailAlternate`` : chemin vers une image de remplacement lorsqu'il n'y a pas de vignette.

Pour ce faire, rendez-vous dans le fichier :file:`config/common/item.config.php` :

.. code-block:: php

    <?php

    return array(
        'data_mapping' => array(
            'thumbnail' => array(
                'value' => function ($item) {
                    foreach ($item->medias as $media) {
                        return $media->get_public_path_resized(64, 64);
                    }
                    return false;
                },
            ),
            'thumbnailAlternate' => array(
                'value' => function ($item) {
                    return 'static/apps/mon_appli/icons/64.png';
                }
            ),
        ),
    );


Il faut ensuite activer la vue vignette dans la configuration de l'App Desk
:file:`mon_appli::config/controller/admin/appdesk.config.php` :


.. code-block:: php
   :emphasize-lines: 8

    <?php

    return array(
        'model' => '',
        'query' => array(),
        'inspectors' => array(),
        'i18n' => array(),
        'thumbnails' => true,
    );


Facultativement, il est possible de mettre la vue vignette par défaut (au lieu de la vue liste) :

.. code-block:: php
   :emphasize-lines: 9-13

    <?php

    return array(
        'model' => '',
        'query' => array(),
        'inspectors' => array(),
        'i18n' => array(),
        'thumbnails' => true,
        'appdesk' => array(
            'appdesk' => array(
                'defaultView' => 'thumbnails',
            ),
        ),
    );