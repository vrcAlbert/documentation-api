Ajouter un champ
################

Nous allons partir d'un exemple pour l'explication.

Ajoutons un champ ``Source`` pour un billet de blog, qui permettra de renseigner une URL externe ayant produit le
contenu original.




Ajout dans la BDD
*****************

.. code-block:: sql

    ALTER TABLE `nos_blog_post` ADD `post_source` VARCHAR(255);


Ajout dans le formulaire
************************

Le formulaire d'ajout / édition d'un billet de blog est définit dans sa configuration CRUD. Pour l'étendre, nous allons
utiliser un évènement !

.. code-block:: php

    Event::register_function('config|noviusos_blog::controller/admin/post', function(&$config) {

        // Ajout du champ 'post_source' de type 'text'
        $config['fields']['post_source'] = array(
            'label' => 'Source originale :',
            'form' => array(
                'type' => 'text',
                'placeholder' => 'http://',
            ),
        );

        // Affichage du champ dans le formulaire
        // Nous créons une entrée intitulée 'Source' dans le menu de droite
        $config['layout']['menu']['Source'] = array('post_source');
    });


Ajout dans la visualisation
***************************

