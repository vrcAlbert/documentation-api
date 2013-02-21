Créer un enhancer
#################



1. Définition dans le fichier :file:`metadata`
==============================================

Les metadata d'un enhancer sont décrites dans la :ref:`documentation d'API <api:metadata/enhancers>`.


2. [Back-office] Créer un contrôleur pour l'enhancer
====================================================

Pour gérer la popup de configuration et la prévisualisation de l'enhancer, nous avons besoin d'un contrôleur.

Créez donc le fichier :file:`mon_appli::classes/controller/admin/enhancer.ctrl.php` en étendant le ``Controller_Admin_Enhancer``
adéquat.

.. code-block:: php

    <?php

    namespace Mon\Appli;

    class Controller_Admin_Enhancer extends \Nos\Controller_Admin_Enhancer
    {

    }

Comme tous les contrôleurs de Novius OS, ajoutons lui un fichier de configuration
:file:`mon_appli::config/controller/admin/enhancer.config.php`

.. code-block:: php

    <?php

    return array(
        // Vide pour l'instant, nous allons le remplir plus bas
    );

Popup de configuration
----------------------

L'affichage ou non d'une popup de configuration est conditionnée par la présence ou non de la clé ``dialog`` dans le
fichier :file:`metadata.config.php`. Ajoutons cette information :

.. code-block:: php

    <?php

    return array(
        'enhancers' => array(
            'mon_appli' => array(
                'dialog' => array(
                    'contentUrl' => 'admin/mon_appli/enhancer/popup',
                    'ajax' => true,
                ),
            ),
        ),
    );

Ici, la popup fera appel à la méthode ``action_popup()`` de la classe ``Mon\Appli\Controller_Admin_Enhancer``. Ce
dernier est prévu pour fonctionner en Ajax.

Comme pour toute modification du fichier :file:`metadata.config.php`, il faut aller appliquer les changements depuis
le gestionnaire d'applications.

Désormais, lorsqu'on ajoute notre enhancer dans un WYSIWYG, une popup s'affiche, mais il n'y a aucune option à
configurer !

Le contrôleur standard que nous avons étendu prévoit d'être configuré pour ajouter les options de l'enhancer.
Rendez-vous dans le fichier de configuration :file:`mon_appli::config/controller/admin/enhancer.config.php` :

.. code-block:: php
   :emphasize-lines: 4-9

    <?php

    return array(
        // Configuration de la popup
        'popup' => array(
            'layout' => array(
                'view' => 'mon_appli::enhancer/popup',
            ),
        ),
    );

Ce fichier fait référence à la vue ``mon_appli::enhancer/popup`` qui n'existe pas, et qu'il faut donc créer. Cette
dernière contiendra des champs de formulaire avec nos options configurables :

.. code-block:: html+php

    <h3>Options</h3>
    <p>
        <label for="item_per_page"><?= __('Item per page:') ?></label>
        <input type="text" name="item_per_page" id="item_per_page" value="<?= \Arr::get($enhancer_args, 'item_per_page', 10) ?>" />
    </p>

L'ancienne configuration de l'enhancer est disponible dans la variable ``$enhancer_args`` (utile pour pré-remplir le
formulaire en cas de modification des options de configuration et de réouverture de la popup).


.. _app_create/enhancer/preview:

Modifier la prévisualisation
----------------------------

.. image:: images/metadata_enhancer.png
	:alt: L'enhancer « Formulaire »
	:align: center

La prévisualisation ajoutée dans le WYSIWYG est chargée en faisant appel à la valeur ``previewUrl`` configurée  dans le
fichier :file:`metadata.config.php`.

Généralement, vous ferez appel au même contrôleur que celui de la popup, mais en appelant la méthode
``action_preview()`` au lieu de ``action_popup()``.

La vue fournie par défaut utilise un icône, un titre (les valeurs par défaut reprennent l'icône 64*64 de
l'application, ainsi que le titre de l'enhancer) et un ``layout`` (fichiers de vues additionnels appelés).

:file:`mon_appli::config/controller/admin/enhancer.config.php` :

.. code-block:: php
   :emphasize-lines: 8-18

    <?php

    return array(
        // Configuration de la popup
        'popup' => array(
            // Ce qu'on avait configuré plus tôt
        ),
        // Configuration de la prévisualisation
        'preview' => array(
            // (facultatif) vue à utiliser pour le rendu (valeur par défaut en exemple)
            //'view' => 'nos::admin/enhancer/preview',
            // (facultatif) fichiers de vues additionnels (inclus par la view au-dessus)
            //'layout' => array(),
            'params' => array(
                // (optionnel) reprend le titre de l'enhancer par défaut
                'title' => "Mon super enhancer",
                // 'icon' (optionnel) reprend celui de l'application en taille 64*64 par défaut
            ),
        ),
    );


À noter qu'il est possible de spécifier une fonction de callback à la fois pour le titre ou pour l'icône. Elle reçoit
alors un paramètre : la configuration de l'enhancer ``$enhancer_args``.

Par exemple, pour l'enhancer « Formulaire », le titre du formulaire sélectionné s'affiche.

.. _app_create/enhancer/front:

3. [Front-office] Afficher votre contenu sur le site
====================================================

Une fois le WYSIWYG enregistré et la page publiée, l'enhancer va s'exprimer sur le site.

Le contenu sera généré par le contrôleur configuré dans une des clés ``enhancer`` ou ``urlEnhancer`` du fichier
:file:`metadata.config.php` (selon si on voulait un enhancer simple ou un URL enhancer). N'oubliez pas de prendre
en compte les changements dans le gestionnaires d'applications si vous faites des modification sur ce fichier.

Par exemple, l'application « Formulaires » a pour configuration ``noviusos_form/front/main`` ce qui fera appel à la
méthode ``action_main()`` du ``Controller_Front`` de l'application ``noviusos_form`` (qui correspond en fait au
contrôleur ``Nos\Form\Controller_Front``).

Cette action prend en paramètre le tableau de configuration qui a été défini dans la popup de configuration
``$enhancer_args``.

Créons le contrôleur :file:`mon_appli::controller/front.ctrl.php`


.. code-block:: php

    <?php

    namespace Nos\Blog;

    class Controller_Front extends \Nos\Controller_Front_Application
    {
        public function action_main($enhancer_args = array())
        {
            // Pour tester
            return print_r($enhancer_args, true);
        }
    }


.. _app_create/enhancer/url:

4. URL enhancers
================

Dans le cas d'un URL enhancer, ce dernier sera capable de gérer des URL.

Lorsqu'on parle du billet de blog ``toto`` ou de la catégorie ``ski``, on fait en réalité référence au billet de blog
dont le nom virtuel est ``toto`` et  à la catégorie dont le nom virtuel est ``ski``.

Prenons un exemple : si votre URL enhancer a été ajouté sur la page :file:`mon/blog.html`, alors il sera en mesure de
gérer des URL qui commencent par :file:`mon/blog/**.html`, comme :

- :file:`mon/blog.html` (liste de tous les billets) ;
- :file:`mon/blog/toto.html` (billet de blog ``toto``) ;
- :file:`mon/blog/page/2.html` (2\ :sup:`e`\  page de la liste des billets) ;
- ou encore :file:`mon/blog/category/ski.html` (liste des billets de la catégorie ``ski``).

Comme précédemment, le contenu est généré par l'action ``main``, mais il est possible de récupérer l'URL étendue avec
``$this->main_controller->getEnhancerUrl();``.

Ensuite, le contrôleur peut générer du contenu différent en fonction de l'URL demandée. Voici un exemple (simplifié)
tiré de l'application « Blog » :


.. code-block:: php

    <?php

    namespace Nos\Blog;

    class Controller_Front extends \Nos\Controller_Front_Application
    {
        public function action_main($enhancer_args = array())
        {
            // URL complète de la page == 'mon/blog/category/ski.html'
            // => $enhancer_url == 'category/ski' (sans .html)
            $enhancer_url = $this->main_controller->getEnhancerUrl();
            $segments = explode('/', $enhancer_url);

            if (empty($enhancer_url))
            {
                // URL 'mon/blog.html' (URL de la page sur laquelle a été ajouté l'enhancer)
                // Affichage de la liste des billets (page 1)
            }
            else if (count($segments) == 1)
            {
                // URL 'mon/blog/toto.html'
                // Affichage du billet de blog 'toto'
            }
            else if (count($segments) == 2)
            {
                if ($segments[0] == 'page')
                {
                    // URL 'mon/blog/page/2.html'
                    $page = $segments[1];
                    // Affichage de la page 2 de la liste des billets
                }
                else if ($segments[0] == 'category')
                {
                    // URL 'mon/blog/category/ski.html'
                    $category = $segments[1];
                    // Affichage de la liste des billets de la catégorie 'ski'
                }
            }

            // L'URL demandé n'est pas gérée par cet enhancer (erreur 404 pour cet enhancer)
            throw new \Nos\NotFoundException();
        }
    }


.. _app_create/enhancers:

Lorsque l'enhancer gère des URL pour certains modèles (ORM), c'est lui qui connait la procédure de génération des ces
dernières. Pour ce faire, il faut alors implémenter une méthode statique ``get_url_model()`` qui va s'en occuper :

.. code-block:: php
   :emphasize-lines: 7-26

    <?php

    namespace Nos\Blog;

    class Controller_Front extends \Nos\Controller_Front_Application
    {
        public static function get_url_model($item, $params = array())
        {
            $model = get_class($item);
            $page = isset($params['page']) ? $params['page'] : 1;

            switch ($model)
            {
                // URL pour un billet de blog particulier
                case 'Nos\Blog\Model_Post' :
                    return urlencode($item->virtual_name()).'.html';
                    break;

                // URL pour la liste des billets d'une catégorie (avec optionnellement une page)
                case 'Nos\Blog\Model_Category' :
                    return 'category/'.urlencode($item->virtual_name()).($page > 1 ? '/'.$page : '').'.html';
                    break;
            }

            return false;
        }
    }

Cette fonction est liée à la ``Behaviour_Urlenhancer`` et aux méthodes ``url()`` et ``urls()`` des modèles. Pour voir
comment les configurer, il faut se référer à la :ref:`documentation d d'API associée <api:php/behaviours/urlenhancer>`.


Exemple :

.. code-block:: php

    <?php

    // Sélection de la catégorie ayant pour ID 1
    $category = Nos\Blog\Model_Category::find(1);

    $url = $category->url(array('page' => 2));

``$url`` aura pour valeur ``mon/blog/category/ski/2.html``. Si on décompose :

- ``mon/blog`` : URL de la page sur laquelle est présent l'enhancer ;
- ``ski`` : URL virtuelle de la catégorie ayant pour ID 1 ;
- ``2`` : numéro de page demandée dans les paramètes.




