Model_Wysiwyg
#############

.. php:namespace:: Nos

.. php:class:: Model_Wysiwyg

	Extend :php:class:`Nos\\Orm\\Model`.

Columns
*******

:wysiwyg_id:                        Model_Wysiwyg primary key.
:wysiwyg_join_table:                DB table name of the model which the wysiwyg is linked to.
:wysiwyg_foreign_id:                ID of the model which the wysiwyg is linked to.
:wysiwyg_foreign_context_common_id: Common ID of the model which the wysiwyg is linked to.
:wysiwyg_key:                       ``string`` key identifying the linked wysiwyg.
:wysiwyg_text:                      Wysiwyg content.

One of ``wysiwyg_foreign_id`` and ``wysiwyg_foreign_context_common_id`` columns is NULL for each row.