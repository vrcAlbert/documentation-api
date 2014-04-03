.. _php/relations/twinnable_many_many:

Twinnable Many to Many
######################

The ``twinnable_many_many`` relation is the equivalent of the FuelPHP native ``many_many`` relation (moreover, it extends ``many_many``).
The difference is that the link is not made on primary keys but on context common IDs.

If you use the ``twinnable_many_many`` relation, the model must implement :doc:`Twinnable behaviour </php/behaviours/twinnable>`.

.. versionchanged:: 4.2
    Before the ``4.2 (Dubrovka)`` version, the linked model also need to implement Twinnable behaviour.

.. seealso::

    * :doc:`Twinnable behaviour </php/behaviours/twinnable>`
    * :doc:`/php/configuration/software/multi_context`.
    * `FuelPHP native many_many <http://fuelphp.com/docs/packages/orm/relations/many_many.html>`__

Configuration
*************

:key_from:                      The key used for the relation in the current model
:model_to:                      The full class name of the target model. Calculated from alias.
:key_to:                        Calculated from the behaviour Twinnable if ``model_to`` is twinnable.
:table_through:                 This is the table that connects the 2 models and has both their common IDs in it.
:key_through_from:              The key that matches the current model's common ID.
:key_through_to:                The key that matches the related model's common ID.
:column_context_from:           Calculated from the behaviour Twinnable if ``model_to`` is twinnable.
:column_context_common_id_to:   Calculated from the behaviour Twinnable if ``model_to`` is twinnable.
:column_context_to:             Calculated from the behaviour Twinnable if ``model_to`` is twinnable.
:column_context_is_main_to:     Calculated from the behaviour Twinnable if ``model_to`` is twinnable.

Use
***

When you use the relation in a find, you can add ``main context`` in conditions. If it's set to false, relation only retrieves related items of the same context.

.. code-block:: php

    <?php
    Model_Example::find('all', array(
        'related' => array(
            'manymany_twinnable' => array(
                'main_context' => false,
            ),
        ),
    );
