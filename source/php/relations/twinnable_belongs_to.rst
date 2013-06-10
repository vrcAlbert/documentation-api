Twinnable Belongs To
####################

The ``twinnable_belongs_to`` relation is the equivalent of the FuelPHP native ``belongs_to`` relation (moreover, it extends ``belongs_to``).
The difference is that the link is not made on the primary key but on the context common ID.

If you use the ``twinnable_belongs_to`` relation, the model and the model linked must implement :doc:`Twinnable behaviour </php/behaviours/twinnable>`.
The field ``key_from`` must be declared common field in the twinnable behaviour.

.. seealso::

    * :doc:`Twinnable behaviour </php/behaviours/twinnable>`
    * :doc:`/php/configuration/software/multi_context`.
    * `FuelPHP native belongs_to <http://fuelphp.com/docs/packages/orm/relations/belongs_to.html>`__

Configuration
*************

:key_from:                  The key used for the relation in the current model.
:model_to:                  The full class name of the target model. Calculated from alias.
:key_to:                    Calculated from the behaviour Twinnable.
:column_context_from:       Calculated from the behaviour Twinnable.
:column_context_to:         Calculated from the behaviour Twinnable.
:column_context_is_main_to: Calculated from the behaviour Twinnable.

Examples
========

The ``Model_Monkey`` belongs to a ``Model_Species`` independently of context. A monkey, in one context, has the same species than in other,
just the translation can be changed. If the species not exists in the same context that the monkey, the relation returns
the species in the main context.

.. code-block:: php

    <?php
    protected static $_twinnable_belongs_to = array(
        'species' => array(
            'key_from' => 'monk_species_common_id',
            'model_to' => 'Nos\Monkey\Model_Species',
            'cascade_save' => false,
            'cascade_delete' => false,
        ),
    );