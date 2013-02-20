Crud
####

Configuration for :php:class:`Nos\\Orm\\Model`'s appdesk.

Associative array:

:controller_url: Url of CRUD controller
:model: Model to be handled by the controller
:environment_relation:
:tab: tab informations, see :ref:`javascript/$/nosAction/nosTabs`
:layout: Where fields are displayed on form. Optional if `layout_insert` and `layout_update` are defined.
:layout_insert: Optional.
:layout_update: Optional.
:views: Optional. Views locations.
:fields:

environment_relation
********************



layout
******

Defines how fields are displayed on form. It is an associative array:

:title: Upper field of the form.
:large: Is form large or not ?
:medias: Array of medias fields at the right of the field.
:save: Which field is the save button.
:subtitle: Fields under title.
:content: Main fields.
:menu: Groups of fields on the right menu.