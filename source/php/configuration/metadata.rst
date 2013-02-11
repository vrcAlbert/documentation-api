Metadata
########


The :file:`metadata.config.php` file is how an application is defined. It tells what contains the application and what
it does.

The most important keys are:

- ``name``: the name of the application ;
- ``namespace``: in which PHP namespace all the classes of the application must be defined ;
- ``icons``: in the 3 standard sizes 16*16, 32*32 and 64*64.

.. code-block:: php

    <?php

    return array(
        'name'      => 'Webpages',
        'namespace' => 'Nos\Page',
        'version'   => '0.2',
        'provider'  => array(
            'name'  => 'Novius OS',
        ),
        'icons' => array(
            64 => 'static/apps/noviusos_page/img/64/page.png',
            32 => 'static/apps/noviusos_page/img/32/page.png',
            16 => 'static/apps/noviusos_page/img/16/page.png',
        ),
        'permission' => array(
            // Empty array for now. Leave it.
        ),
        'i18n_file' => 'noviusos_page::metadata',
        'launchers' => array(
            // Optional
        ),
        'enhancers' => array(
            // Optional
        ),
        'templates' => array(
            // Optional
        ),
        'data_catchers' => array(
            // Optional
        ),
    );

An application provides:


Launchers
=========

A :term:`launcher <Launcher>` is an icon on the home tab.

A launcher is defined with:

- a key: its ``identifier`` ;
- a ``name``: text to display for the icon ;
- an ``icon``: (optional) URL to a 64*64 image, default will use the 64*64 icon of the app ;
- an ``action``: what is done when clicking on the launcher.

.. todo::

    Mettre un lien vers la doc des actions PHP.

.. code-block:: php

    <?php

    return array(
        'launchers' => array(
            'noviusos_page' => array(
                'name' => 'Webpages',
                // 'icon' is not set, so the default icon will be used
                'action' => array(
                    // open a tab
                    'action' => 'nosTabs',
                    'tab' => array(
                        'url' => 'admin/noviusos_page/appdesk/index',
                        // 'iconUrl' is not set, so the default icon will be used
                    ),
                ),
            ),
        ),
    );


.. _metadata/enhancers:

Enhancers
=========

:term:`Enhancers <Enhancer>` are used in WYSIWYG editors. They provide functionalities for the front-office.

For example, the ‘Forms’ application allows users to insert forms in their web pages (using an enhancer).

:term:`URL enhancers <URL Enhancer>`, a specific type of enhancers, handle their own URLs. For example, every blog post
has an URL.


.. image:: images/metadata_enhancer.png
	:alt: The ‘Form’ enhancer
	:align: center

An enhancer is defined with:

- ``title``: title of the enhancer displayed when opening the ‘Application’ menu from the wysiwyg ;
- ``desc``: (optional) description of the enhancer ;
- ``iconUrl``: (optional)  URL to a 16*16 icon, displayed when opening the ‘Application’ menu from the wysiwyg, default
  will use the 16*16 icon of the app ;
- ``enhancer`` or ``urlEnhancer``: URL of the front-office controller used to render the enhancer. Only one of the two
  keys can is used, depending if you want an URL enhancer or just a plain regular enhancer ;
- ``previewUrl``: (optional)  URL of the controller used to render the preview in the wysiwyg ;
- ``dialog`` : (optional) If you want a configuration popup, URL of the controller used to display and save the
  enhancer configuration. See :js:func:`$container.nosDialog` for the list of parameters.


.. code-block:: php

    <?php

    return array(
        'noviusos_form' => array(
            'title' => 'Form',
            'desc'  => '',
            // Here it's just a regular enhancer
            'enhancer' => 'noviusos_form/front/main',
            //'urlEnhancer' => 'noviusos_form/front/main',
            'iconUrl' => 'static/apps/noviusos_form/img/icons/form-16.png',
            // We'll use our controller to generate the preview
            'previewUrl' => 'admin/noviusos_form/enhancer/preview',
            // And the user has to configure it
            'dialog' => array(
                'contentUrl' => 'admin/noviusos_form/enhancer/popup',
                'width' => 450,
                'height' => 400,
                'ajax' => true,
            ),
        ),
    );



Templates
=========

:term:`Templates <Template>` are similar to other CMS' templates or themes. They provide a view for the front-office.




Data catchers
=============

.. todo::
    Voir comment faire pour cette section

