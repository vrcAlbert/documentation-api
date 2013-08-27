Configuration
*************

To modify the comments API configuration, you need to extend the configuration file :file:`noviusos_comments::api`.

:default:
    :default_state: ``published`` or ``pending`` (if you want moderation)
    :use_recaptcha: false
    :anti_spam_identifier:
        :failed: 548
        :passed:  327
    :rss:
        :model:
            :nb: 20
        :item:
            :nb: 20
    :send_email:
        :to_author: true
        :to_commenters: true
    :gravatar:
        :size: 64
:setups: Array. The setup id in key, array like ``default`` for the value.

You can modify the ``default`` configuration, or add a setup for a specific model or a specific context.

If you want to change configuration for all cases:

.. code-block:: php

    <?php
    array(
        'default' => array(
            'use_recaptcha' => true,
        ),
    );

If you want to change configuration only for a specific model:

.. code-block:: php

    <?php
    array(
        'setups' => array(
            'My\Namespace\Model_Item' => array(
                'use_recaptcha' => true,
            ),
        ),
    );

If you want to change configuration only for a specific context:

.. code-block:: php

    <?php
    array(
        'setups' => array(
            'main::en_GB' => array(
                'use_recaptcha' => true,
            ),
        ),
    );

.. note:: If you want to activate Recaptcha, you have to install `this package <https://github.com/fuel-packages/fuel-recaptcha>`__ in :file:`local/packages`.