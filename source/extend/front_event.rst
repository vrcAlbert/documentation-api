Modifier un comportement en front-office
########################################


Novius OS fournit un mécanisme d'évènements destiné à interagir avec le moteur.

Il existe 2 types d'évènements :

- Ceux qui servent à modifier une / des valeur(s) ;
- Ceux qui notifient qu'une action s'est produite.


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


Pour une liste des évènements, il faut se référer la documenation API associée.

.. seealso::

    :ref:`api:php/events`



Faire une redirection 301 en fonction de l'URL
**********************************************

Il est possible de créer une page en back-office avec comme type :guilabel:`Lien externe` pour faire une redirection 301.

Il est également possible de les configurer via un fichier :file:`./htaccess`.

Enfin, on peut aussi le faire directement via le code, comme présenté ci-dessous.

.. code-block:: php

	<?php

	Event::register_function('front.start', function($params)
	{
	    // Utilisation de la classe Str de FuelPHP
	    if (Str::starts_with($params['url'], 'an-old-url'))
	    {
	        // Note : 10 == strlen('an-old-url')
	        $new_url = 'my-new-url'.substr($params['url'], 10);

	        // Utilisation de la classe Response de FuelPHP
	        \Response::redirect($new_url, 'location', 301);
	    }
	});


Envoyer un mail remerciement dans un formulaire de contact
**********************************************************

.. code-block:: php

	<?php

	Event::register_function('noviusos_form::after_submission', function(&$answer, $enhancer_args)
	{
	    foreach ($answer->fields as $field)
	    {
	        if ($field->anfi_field_type == 'email' && !empty($field->anfi_value)
	        {
	            $email = Email::forge();
                $email->from('mon@email.me', 'Mon Nom');
                $email->to($field->anfi_value);
                $email->subject('Votre demande de contact');

                // Email au format texte (use html_body() instead if you want to send HTML email)
                $email->body('Merci pour votre demande de contact, elle a bien été reçue. Nous allons y répondre prochainement.');

                try
                {
                    $email->send();
                }
                catch(\Exception $e)
                {
                    // Could not send the email
                }
	        }
	    }
	});

