Model_Wysiwyg
#############

.. php:class:: Model_Wysiwyg

	| Extend :php:class:`Model`.
	| Belongs to the namespace :php:ns:`Nos`

Columns
*******

:wysiwyg_id: Model_Wysiwyg primary key.
:wysiwyg_join_table: DB Table name of model in which the wysiwyg is linked.
:wysiwyg_foreign_id: ID of the model in which the wysiwyg is linked.
:wysiwyg_key: String key identifying the wysiwyg linked.
:wysiwyg_text: Wysiwyg content.
