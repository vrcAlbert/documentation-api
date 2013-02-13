Principes du multi-Contextes
############################

| Novius OS peut nativement gérer plusieurs sites, chacun de ces sites pouvant avoir plusieurs versions linguistiques.
| Un contexte est un binome site / langue.

Exemple
*******

Votre instance de Novius OS peut gérer votre site vitrine qui se décline en 3 langues (français, anglais et espagnol),
votre site pour mobile disponible qu'en français, et un site événementiel en anglais.

============= ======== ======= ========
Site / Langue Français Anglais Espagnol
============= ======== ======= ========
Vitrine       X        X       X
Mobile        X
Événementiel           X
============= ======== ======= ========

Votre instance Novius OS gérera alors **5** contextes :

* Vitrine / Français
* Vitrine / Anglais
* Vitrine / Espagnol
* Mobile / Français
* Événementiel / Anglais

Configuration
*************

Pour configurer les différents contextes de votre instance Novius OS, veuillez vous référer à la :ref:`documentation d'API <api:php/configuration/multi_contexts>`.

Cas particuliers
****************

Qui peut le plus peut le moins. Votre Novius OS peut gérer :

* un seul site dans plusieurs langues
* plusieurs sites dans une seule langue
* un seul site dans une seule langue

| L'interface du back-office tient compte de ses différents cas. Le terme _contexte_ s'effacera alors pour ne parler plus
  que de sites ou de langues.
| Il disparaitra même complètement en cas d'un seul site et de une seule langue.

Ajouter des contextes
*********************

Vous pouvez ajouter à n'importe quel moment de nouveaux contextes, sites ou langues à votre configuration.
Modifiez simplement votre fichier ``contexts.config.php``, les nouveaux contextes sont aussitôt pris en compte.

.. todo::

	Lien vers la configuration de la doc d'API

