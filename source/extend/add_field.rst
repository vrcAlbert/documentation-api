Ajouter un champ
################

Nous allons partir d'un exemple pour l'explication.

Ajoutons un champ ``Source`` pour un billet de blog, qui permettra de renseigner une URL externe ayant produit le
contenu original.




Dans la BDD
***********

.. code-block:: sql

    ALTER TABLE `nos_blog_post` ADD `post_source` VARCHAR(255);


Dans le formulaire
******************

Le formulaire d'ajout / édition d'un billet de blog est définit dans sa configuration CRUD. Pour l'étendre, nous allons
utiliser un évènement !


Dans le fichier :file:`local/bootstrap.php` (créez-le si nécessaire) :

.. code-block:: php

    <?php

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


Le formulaire possède désormais un champ éditable supplémentaire, comme vous pouvez le voir ci-dessous :

.. image:: images/blog_source_field.png
	:alt: Champ 'source' dans le formulaire d'un billet de blog
	:align: center


Dans la visualisation
*********************

Pour la vue, nous créer le fichier :file:`local/views/apps/noviusos_blognews/front/post/content.view.php`

.. code-block:: html+php

    <?php

    // On inclut le fichier d'origine (qui affiche le contenu)
    include APPPATH.'/applications/noviusos_blognews/views/front/post/content.view.php';

    // On rajoute la source à la fin
    if (!empty($item->post_source)) {
        ?>
        <p class="blognews_source">
            <?= __('Source:') ?>
            <a href="<?= htmlspecialchars($item->post_source) ?>">
                <?= htmlspecialchars($item->post_source) ?>
            </a>
        </p>
        <?php
    }

