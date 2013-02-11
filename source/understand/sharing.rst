Partage (Sharing)
*****************

.. seealso::

	`Partage dans Novius OS <http://novius-os.github.com/docs/fr/applications.html#sharing>`_


.. _sharing_content-nuggets:

Content nuggets
===============

Un content nuggets est un ensemble de données à partager.

Structure des données
---------------------

Les données d'un content nugget ont une structure standardisées :

* Titre
* URL
* Texte
* Image

Pour pouvoir partager un item, il suffit de lui assigner le :ref:`Behaviour Sharable <behaviours_sharable>`, qui va
définir comment extraire ces données standardisées.


.. _sharing_data-catchers:

Data catchers
=============

Les data catchers sont des composants qui exploitent les content nuggets (eux-mêmes générés par les modèles).

Ils sont définis par les applications dans leur fichier :file:`metadata.config.php`, exactement comme les gabarits, les enhancers et les launchers.

Inclus au logiciel
------------------

Déclenchés par l'utilisateur
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Twitter
* Facebook
* Google+
* Blog

Le data catcher ``Blog`` peut être utilisé pour créer des billets de blog à partir d'autres items, comme des singes (notre application bac-à-sable) ou des livres (celle-ci n'existe pas, c'est juste un exemple).


Exemple : **Twitter**
---------------------

Voici comment est définit le Data catcher pour Twitter :

.. code-block:: php

	<?php

	return array(
        'data_catchers' => array(
            'noviusos_simpletwitter' => array(
                'title' => 'Twitter',
                'description'  => '',
                'iconUrl' => 'static/apps/noviusos_simpletwitter/img/twitter.png',
                'action' => array(
                    'action' => 'window.open',
                    'url' => 'https://twitter.com/intent/tweet?text={{urlencode:'.\Nos\DataCatcher::TYPE_TITLE.'}}&url={{urlencode:absolute_url}}',
                ),
                'onDemand' => true,
                'specified_models' => false,
                'required_data' => array(
                    \Nos\DataCatcher::TYPE_TITLE,
                ),
                'optional_data' => array(
                    \Nos\DataCatcher::TYPE_URL,
                ),
            ),
        ),
	);

Le data catcher **Twitter** nécessite au content nuggets d'avoir un titre. L'URL est optionnelle (mais sera utilisée si elle est fournie).
