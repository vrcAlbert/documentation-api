Model_Link
###########

.. php:namespace:: Nos\Media

.. php:class:: Model_Link

	| Link between a :php:class:`Model_Media` and a :php:class:`Nos\\Orm\\Model`.
	| Extends :php:class:`Nos\\Orm\\Model`.

Columns
*******

:medil_id:         Model_Link primary key.
:medil_from_table: DB table name of the model which the media is linked to.
:medil_foreign_id: ID of the model which the media is linked to.
:medil_key:        ``string`` key identifying the linked media.
:medil_media_id:   ID of the linked media.

Relations
*********

.. php:attr:: media

	* Relation type: :term:`belongs_to`.
	* Model: :php:class:`Model_Media`
