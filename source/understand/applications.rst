Fondamentaux des applications
=============================

Une application se définit par ses modèles, mais aussi par les contrôleurs et vues associés. Ils dépendent de la nature de l’application. Néanmoins, certains éléments / principes sont génériques et réutilisables dans tous les cas.

Définition
----------

Pour pouvoir ajouter une application au gestionnaire d'applications, il faut créer un fichier metadata.php situé immédiatement dans le dossier “config” de votre application. Ce fichier doit contenir le namespace de l'application, qui doit être de la forme Provider\\NomApplication. Il faut y ajouter le nom de l’application, une version et le provider (caractérisé au minimum par un nom).

Il est également possible de définir d’autres éléments dans ce fichier metadata :

* **Launchers** : icônes de l'onglet d'accueil permet de lancer une application. Ils sont définis par un nom et l'URL du contrôleur appelé pour afficher la vue associée.
* **Data catchers** : composant d'une application permettant d'exploiter les données partagées par d'autres (dites sharable data)
* **Enhancers** : grâce aux enhancers, une application vient enrichir le contenu édité dans un WYSIWYG.
* **Templates** : modèles de pages pour le front-office.

`Voir aussi l'infographie 'Comprendre les applications' <http://novius-os.github.com/docs/fr/applications.html>`_

L’App Desk
----------

Avant tout, :doc:`consulter les principes ergonomiques <ergonomie>` pour comprendre l'App Desk.


La configuration de l’App Desk
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

L’App Desk est caractérisé par plusieurs éléments configurables :

- Le type d’affichage des données
- Les données à afficher
- Les actions principales et secondaires

Le tableau principal peut proposer plusieurs vues (à ne pas confondre avec le V de MVC) : liste, arborescence, vignettes.

Ces vues sont définies via un fichier de configuration PHP et un fichier JS. Le fichier de configuration PHP précise les données à afficher, là où le fichier JS définit l’organisation de l’App Desk d’un point de vue UI. Cependant, il s'agit là d'une explication rapide, simplifiée. En rentrant dans le détail, vous verrez que certaines éléments liés à l'affichage ont à être configurés dans le fichier PHP.

Le fichier JS permet également de définir les actions principales et secondaires. Ces actions sont obligatoirement définies par un lien vers un contrôleur.

Les inspecteurs sont également définis dans les deux fichiers. La configuration PHP permet d'indiquer sur quel attribut ou relation les données du tableau principal seront triées. Le fichier JS définit, en plus de l’UI, les actions associées aux éléments de l’inspecteur. A noter que les inspecteurs sont basés :
- Soit sur le même modèle que celui du tableau principal, l'inspecteur fait alors référence à des attributs (ex : date de création pour des billets de blog),
- Soit sur un autre modèle (ex : auteur pour des billets de blog).

Contrôleurs, formulaires et modèles
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Depuis l’App Desk, il est possible d’appeler des contrôleurs qui réalisent des opérations sur les données concernées.

Certaines opérations s'effectuent directement (ex : la suppression, seule une confirmation est demandée). Elles sont, dans ce cas, attribuées au contrôleur de l’App Desk.

D'autres opérations appelent une vue et sont alors attribuées au contrôleur du modèle. Généralement, la vue appelée est un formulaire (ajout / édition). Ce formulaire est construit grâce au fichier de configuration du modèle, qui peut être rempli grâce à une instance du modèle. Le contrôleur est de nouveau appelé lors de l’envoi du formulaire pour enregistrer les données.

Observers et behaviours
-----------------------

Les observers sont issus du framework `FuelPHP <http://dev-docs.fuelphp.com/packages/orm/observers/intro.html>`_.

Ce sont des procédures liées directement à un modèle. Elles sont appelées lorsque qu'un évènement identifié est déclenché. Ces procédures sont utilisées pour formater, modifier ou valider des propriétés du modèle (ex : reformatage des données avant l'insertion en base de données).

Les behaviours, implémentés pour Novius OS, reprennent et étendent ce principe. Là où les observers effectuent une action sur une propriété du modèle, les behaviours définissent un ensemble de méthodes qui établissent un comportement particulier sur le modèle (ex : translatable, publishable). Ces méthodes sont également déclenchées via des évènements.

Ces outils ont pour intérêt de mutualiser des méthodes pour plusieurs modèles distincts.