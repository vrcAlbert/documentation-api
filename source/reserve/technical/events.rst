Évènements
##########

.. contents::
	:local:
	:backlinks: top
	:depth: 2


.. only:: not_rtd

	.. todo::

		Déplacer la partie Formulaires dans une page dédiée à l'application (quand ça existera).

Novius OS fournit un mécanisme d'évènements destiné à interagir avec le moteur.

Il existe 2 types d'évènements :

* Ceux qui servent à modifier une / des valeur(s) ;
* Ceux qui notifient qu'une action s'est produite.


.. code-block:: php

	<?php

	// Exemple d'évènement qui écoute une action
	Event::register('event_name', function($value)
	{
	    // L'action 'event_name' s'est produite
	});


.. code-block:: php

	<?php

	// Exemple d'évènement qui modifie une valeur
	Event::register_function('event_name', function(&$value)
	{
	    // $value peut être modifiée
	});


Configuration
*************

Les évènements concernant le chargement de fichiers de configuration sont très utilisés.

.. _events_configuration:

config|<path>
=============

Lancé lors du chargement d'un fichier de configuration.

.. code-block:: php

    <?php

    // Écoute de l'évènement
    Event::register_function('config|nos::controller/admin/page/page', function(&$config)
    {
        // ...
    }
    // Lancement de l'évènement
    $config = Config::load('nos::controller/admin/page/page', true);


Ceci fonctionne également avec des chemins absolus :

.. code-block:: php

    <?php

    // Écoute de l'évènement
    Event::register_function('config|/data/www/novius-os/local/config/test.php', function(&$config)
    {
        // ...
    }
    // Lancement de l'évènement (le fichier doit exister)
    $config = Config::load('/data/www/novius-os/local/config/test.php', true);


config|<group>
==============

Chargement d'un tableau de configuration.

.. code-block:: php

	<?php

    // Écoute de l'évènement
    Event::register_function('config|group', function(&$config)
    {
        // ...
    }
    // Lancement de l'évènement
    Config::load(array(), 'group');



Front-office
************

front.start
===========

Demande d'une page.

Modification possible de l'URL.

* ``&$url``


.. code-block:: php

	<?php

    /**
     * @param  string  $url  URL de la page courante (sans le nom de domaine et avec le .html)
     */
	Event::register_function('front.start', function($params)
	{
	    $url =& $params['url'];
	    // ...
	});


front.parse_wysiwyg
===================

Post-traitement d'un Wysiwyg.

Modification possible du contenu.


.. code-block:: php

	<?php

    /**
     * @param  string  $content  Contenu HTML du WYSIWYG, déjà traité par le moteur
     */
	Event::register_function('front.parse_wysiwyg', function(&content)
	{
	    // ...
	});


front.display
=============

Post-traitement du contenu HTML de la page.

Modification possible du contenu.

.. code-block:: php

	<?php

    /**
     * @param  string  $content  Contenu HTML de la page à écrire dans le cache
     */
	Event::register_function('front.display', function(&content)
	{
	    // ...
	});


front.404NotFound
=================

La page demandée n'existe pas.

Notification seulement.

.. code-block:: php

	<?php

    /**
     * @param  array  $args  Tableau contenant 'url'
     */
	Event::register_function('front.404NotFound', function($params)
	{
	    $url = $params['url'];
	    // ...
	});



Emails
******

email.before_send
=================

Avant l'envoi d'un mail.

.. code-block:: php

    <?php

    /**
     * @param  object  $email  Instance de Email_Driver
     */
    Event::register_function('email.before_send', function($email)
    {
        // ...
    }


email.after_send
================

Après l'envoi d'un mail

.. code-block:: php

    <?php

    /**
     * @param  object  $email  Instance de Email_Driver
     */
    Event::register_function('email.after_send', function($email)
    {
        // ...
    }


Formulaires
***********

noviusos_form::rendering
========================

Cet évènement est lancé par l'enhancer avant d'afficher le formulaire.

Il permet de modifier le ``layout`` et les ``fields``. Les variables ``item`` (instance de Model_Form) et ``enhancer_args`` (position des label, etc.) sont en lecture seule.

.. code-block:: php

    <?php

    /**
     * @param  array  $args  Tableau contenant 'fields', 'layout', 'form' et 'enhancer_args'
     */
    Event::register_function('noviusos_form::rendering', function(array &$args)
    {
        $fields =& $args['fields'];
        $layout =& $args['layout'];
        $form   =  $args['item']; // Instance of Nos\Form\Model_Form
        $enhancer_args = $args['enhancer_args'];

        // This is an exemple of what $layout contains
        $layout = 'noviusos_form::foundation';

        foreach ($fields as &$field) {

            // This is an example of what $field contains
            $field = array(
                'label' => array(
                    'callback' => array('Form', 'label'),
                    'args' => array('Label:', 'technical_id', array(
                        'for' => 'field_technical_id',
                    )),
                ),
                'field' => array(
                    'callback' => array('Form', 'input'),
                    'args' => array('field_name', 'field_value', array(
                        'id'          => 'field_technical_id',
                        'class'       => 'field_technical_css',
                        'title'       => 'Label:',
                        'placeholder' => 'Label:',
                        'required'    => 'required',
                    )),
                ),
                'instructions' => array(
                    'callback' => 'html_tag',
                    'args' => array('p', array('class' => 'instructions'), 'Instructions for the user'),
                ),
                'new_row' => true,
                'new_page' => true,
                'width' => 4,
                'item' => $item, // Instance of Nos\Form\Model_Field
            );
        }

        // ...
    }

noviusos_form::rendering.<virtual_name>
=======================================

Même chose que ``noviusos_form::rendering``, mais n'est déclenché que pour le formulaire ayant le ``<virtual_name>`` spécifié.


noviusos_form::data_validation
==============================

**Attention !** Cette fonction doit retourner un tableau avec les erreurs de validation détectées.

.. code-block:: php

    <?php

    /**
     * @params  array  $data  Les données reçues
     * @params  Model  $form  Instance de Nos\Form\Model_Form
     *
     * @return  array  La liste des erreurs repérées
     */
    Event::register_function('noviusos_form::data_validation', function(&$data, $form) {

        $errors = array();
        // Ceci mettra tous les champs en erreur
        foreach ($data as $name => $value) {
            $errors[$name] = '{{label}}: ‘{{value}}’ non toléré.';
        }
        return $errors;
    });

Les messages d'erreurs retournés peuvent contenir les *placeholders* ``{{label}}`` et ``{{value}}`` (ils seront remplacés de manière adéquate).


noviusos_form::data_validation.<virtual_name>
=============================================

Même chose que ``noviusos_form::data_validation``, mais n'est déclenché que pour le formulaire ayant le ``<virtual_name>`` spécifié.



noviusos_form::before_submission
================================

.. code-block:: php

    <?php

    /**
     * @param  array  $data           Les données reçues (à enregistrer en BDD)
     * @param  Model  $form           Instance de Nos\Form\Model_Form
     * @param  array  $enhancer_args  La configuration de l'enhancer
     *
     * @return  bool  false => la réponse ne sera pas enregistrée
     */
    Event::trigger_function('noviusos_form::before_submission', array(&$data, $form, $enhancer_args) {

        // Modification possible de $data avant l'enregistrement en BDD.

        // Si vous retournez 'false', la réponse ne sera pas enregistrée.
        return false;
    });


noviusos_form::before_submission.<virtual_name>
===============================================

Même chose que ``noviusos_form::before_submission``, mais n'est déclenché que pour le formulaire ayant le ``<virtual_name>`` spécifié.


noviusos_form::after_submission
===============================

.. code-block:: php

    <?php

    /**
     * @param  Model  $answer         Instance de Nos\Form\Model_Answer
     * @param  array  $enhancer_args  La configuration de l'enhancer
     */
    Event::trigger_function('noviusos_form::after_submission', array(&$answer, $enhancer_args) {

        // ...
    });


noviusos_form::after_submission.<virtual_name>
==============================================

Même chose que ``noviusos_form::after_submission``, mais n'est déclenché que pour le formulaire ayant le ``<virtual_name>`` spécifié.
