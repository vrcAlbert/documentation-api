Attachment
##########

Binds files to model instances. Based on the :doc:`attachment class </php/classes/attachment>`.


Configuration
*************

:key_from:          Calculated from the primary key.
:attachment_config: Array for attachment configuration. ``dir`` key is optional, calculated from model and relation names.

	.. seealso:: :doc:`Attachment class </php/classes/attachment>`.

Examples
========

In this case, each item of the model have 2 attachments: avatar and cv.

.. code-block:: php

    <?php
    protected static $_attachment = array(
        'avatar' => array(),
        'cv' => array(),
    );
