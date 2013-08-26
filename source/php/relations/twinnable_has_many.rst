.. _php/relations/twinnable_has_many:

Twinnable Has Many
##################

The ``twinnable_has_many`` relation is the equivalent of the FuelPHP native ``has_many`` relation (moreover, it extends ``has_many``).
The difference is that the link is not made on the primary key but on the context common ID.

If you use the ``twinnable_has_many`` relation, the model and the model linked must implement :doc:`Twinnable behaviour </php/behaviours/twinnable>`.

.. seealso::

    * :doc:`Twinnable behaviour </php/behaviours/twinnable>`
    * :doc:`/php/configuration/software/multi_context`.
    * `FuelPHP native has_many <http://fuelphp.com/docs/packages/orm/relations/has_many.html>`__

Configuration
*************

:key_from:                      Calculated from the behaviour Twinnable.
:model_to:                      The full class name of the target model. Calculated from alias.
:key_to:                        The key used for the relation in the linked model.
:column_context_from:           Calculated from the behaviour Twinnable.
:column_context_to:             Calculated from the behaviour Twinnable.
:column_context_common_id_to:   Calculated from the behaviour Twinnable.
:column_context_is_main_to:     Calculated from the behaviour Twinnable.

