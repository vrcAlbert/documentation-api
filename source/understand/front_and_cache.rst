Front-Office et cache
#####################

Novius OS utilise le **mod_rewrite** d’:program:`Apache` (ou l’équivalent sur un autre serveur) pour afficher les pages en front-office.

Toutes les URLs finissant par ``.html``, la home et les répertoires sont redirigées vers le fichier :file:`NOSROOT/public/htdocs/novius-os/front.php`.

Ce fichier charge Novius OS et délègue le traitement de l'URL au :ref:`Controller_Front <api:php/classes/controller_front>`.

Le :ref:`Controller_Front <api:php/classes/controller_front>` analyse l'URL et détermine le chemin du fichier de cache correspondant.
À partir de là, plusieurs possibilités.

Exécution du cache
==================

Le fichier de cache correspondant à l'URL existe.

Le cache des pages est enregistré dans le répertoire :file:`NOSROOT/local/cache/page/`. Le premier niveau d'arborescence correspond aux domaines des URLS.
Le cache recrée ensuite l'arborescence de l'URL.

Le fichier de cache en lui-même est un fichier PHP. Le début du fichier contient toujours une vérification de la validité
du cache par rapport à sa durée de vie. Il contient également un mécanisme pour recréer les propriétés du :ref:`Controller_Front <api:php/classes/controller_front>`
qui étaient disponibles au moment de sa génération (page, URLs, status, headers, custom data).

Ce fichier de cache est exécuté et, s'il est toujours valide, ce qu'il affiche est renvoyé à l'internaute, avec le ``status`` et les ``headers`` enregistrés.

Génération du cache
===================

Si le fichier de cache correspondant à l'URL n'existe pas ou n'est plus valide.

Le :ref:`Controller_Front <api:php/classes/controller_front>` va déterminer la page appelée en fonction de l'URL. La page connue,
il récupère le template qui lui est lié. Puis le ou les WYSIWYG de la page venant s'insérer dans le template.

Si les WYSIWYG contiennent des enhancers, ces enhancers sont exécutés et leur résultat enregistré.

Puis le template est exécuté comme une View en prenant comme paramètre le tableau des WYSIWYG (``$wysiwyg``),
le titre de la page (``$title``), la page (``$page``) et le :ref:`Controller_Front <api:php/classes/controller_front>` (``$main_controller``).

Le contenu généré est enregistré dans le fichier de cache.

Puis le fichier de cache est exécuté comme expliqué ci-dessus, et renvoie le contenu à l'internaute, avec le ``status``
et les ``headers`` potentiellement spécifiés lors du processus de génération du cache (notamment par les enhancers).

Interactions possibles
======================

Au cours du processus, le :ref:`Controller_Front <api:php/classes/controller_front>` envoie différents événements à des moments clés.
En interceptant ces événements vous pouvez influencer ou modifier le traitement.

.. seealso:: :ref:`Événements front-office <api:php/events/front-office>`

Vous pouvez également influencer ou modifier le traitement par les méthodes du :ref:`Controller_Front <api:php/classes/controller_front>`
en récupérant son instance, soit par :ref:`\Nos\Nos::main_controller() <api:php/classes/nos/main_controller>`, soit via ``$this->main_controller`` dans un enhancer.

Modifier le contenu généré
--------------------------

Dans certains cas, vous pouvez vouloir générer un contenu de sortie sans tenir compte du template, par exemple pour
renvoiyer un flux RSS depuis un enhancer. Pour cela, utiliser la méthode ``sendContent()`` du :ref:`Controller_Front <api:php/classes/controller_front>`.

Voici un exemple de code d'un enhancer :

.. code-block:: php

    <?php

    $this->main_controller->setHeader('Content-Type', 'application/xml');
    $this->main_controller->setCacheDuration(60 * 30); // La durée de cache est fixée à 30 minutes
    return $this->main_controller->sendContent($rss); // La variable $rss contient le flux RSS

Le fichier de cache ne contiendra alors que le contenu du flux RSS et la réponse HTTP enverra un header pour spécifier le ``content-type``.

Exécution hors cache
====================

Dans certain cas, le système de cache peut-être trop efficace. Par exemple, si une partie du template ou d'un enhancer doit être différent en fonction
de si l'utilisateur est identifié ou non. Dans ce cas il est utile d'enregistrer dans le cache le code PHP a exécuter et non pas son résultat.

Pour cela, il suffit d'utiliser les méthodes ``callHmvcUncached()`` et ``viewForgeUncached`` de la classe :ref:`FrontCache <api:php/classes/frontcache>`.

.. code-block:: php

    <?php

    \Nos\FrontCache::callHmvcUncached(
        'uri/controller',
        array(
            'id' => \Front_Utilisateur::get_current_user_id() // C'est un exemple, la classe \Front_Utilisateur n'existe pas.
        )
    );

    // ou

    \Nos\FrontCache::viewForgeUncached(
        'uri/view', // Le chemin d'une vue
        array(
            'id' => \Front_Utilisateur::get_current_user_id()
        ),
        false
    );


Suffix Handler
==============

Si vous voulez que le chemin de cache tienne compte d'autre chose que de la simple URL. Par exemple, que le cache tienne compte d'un paramètre GET
(par défaut, le même cache est utilisé que l'URL ai ou n'ai pas de paramètre GET).

Pour cela, il suffit d'utiliser la méthode ``addCacheSuffixHandler()`` du :ref:`Controller_Front <api:php/classes/controller_front>`.

.. code-block:: php

    <?php

    \Nos\Nos::::main_controller->addCacheSuffixHandler(array(
        array(
            'type' => 'GET',
            'keys' => array('my_param'),
        ),
    ));

    // ou

    \Nos\Nos::::main_controller->addCacheSuffixHandler(array(
        array(
            'type' => 'callable',
            'callable' => array('MyClasse', 'myMethod'),
            'args' => array(
                'argument pour exemple'
            ),
        ),
    ));

Dans le 1er cas, le système de cache gérera un fichier différent pour une même URL ayant un paramètre GET ``my_param`` avec une valeur différente.

Dans le second cas, le système de cache appellera la méthode ``MyClasse::myMethod('argument pour exemple')``,
charge à la méthode de renvoyer un suffixe au fichier de cache si besoin.
