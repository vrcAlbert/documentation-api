Set of radio buttons
####################

.. php:namespace:: Nos

.. php:class:: Renderer_Radioset

    | Extends :php:class:`Nos\\Renderer`.
    | This renderer is used to display a set of radio buttons.


.. image:: images/radioset.png
    :alt: Set of radio buttons UI


Configuration
*************

.. php:attr:: name

    Name for the radio input.

.. php:attr:: choices

    .. Strange syntax here, we need double-indentation for :label: or it will write 'Label' (uppercase L)

    List of radio buttons. Key is the value and value is an ``array``.

        :label: Text or image to display around the radio button
        :side_label: Text on the side for the selected option

.. php:attr:: value

    Value of the selected input.

.. php:attr:: class

    Class for the container ``div``.

Example
*******

Adding set of radio button in a CRUD form configuration:

.. code-block:: php

    <?php

    return array(
        'label' => __('Status:'),
        'renderer' => '\Nos\Renderer_Radioset',
        'renderer_options' => array(
            'choices' => array(
                'refused' => array(
                    'label' => '<img src="static/novius-os/admin/novius-os/img/icons/status-red.png" />',
                    'side_label' => __('Refused'),
                ),
                'pending' => array(
                    'label' => '<img src="static/apps/noviusos_comments/img/status-orange.png" />',
                    'side_label' => __('Pending'),
                ),
                'published' => array(
                    'label' => '<img src="static/novius-os/admin/novius-os/img/icons/status-green.png" />',
                    'side_label' => __('Published'),
                ),
            ),
            'class' => 'flat',
        ),
    );

