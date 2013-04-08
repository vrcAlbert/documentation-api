Guide de migration de la version 0.2 à la version 0.2.1
#######################################################

Peu de modification a réaliser pour passer à la version suivante. La nouvelle API est compatible avec l'ancienne.
À partir de cette version, Novius OS gère les dépréciations. En voici une liste :

* Le renderer ``Nos\Renderer_Media`` est à renommer en ``Nos\Media\Renderer_Media``.
* Dans la configuration des launchers, la clé ``url`` est dépréciée au profit de ``action``.
* Les clés ``widgets`` et ``widget_options`` sont à remplacer par ``renderer`` et ``renderer_options``.
* La fonction ``\Config::extendable_load()`` est dépréciée et doit être remplacée par ``\Config::loadConfiguration``.
* Dans la configuration du behaviour ``Orm_Behaviour_Publishable``, la clé ``publication_bool_property`` est dépréciée.
  Utilisez à la place la clé ``publication_state_property``.

Les pages sont maintenant mises en cache par défaut (d'une durée de 10 minutes) ; celà peut entrainer des comportements
inatendus dans certaines applications avec affichage en front (hors celles du coeur et celles installées par défaut).

Quelques fichiers migrations doivent être exécutées. Si vous utilisez ``oil``, merci d'utiliser la commande ``php oil
refine migrate -m`` car l'organisation des migrations a été modifiée.