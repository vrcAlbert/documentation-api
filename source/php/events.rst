
.. _php/events:

Events
######


Configuration
*************

.. _events_configuration:


config|<path>
=============

.. php:function:: config|<path>($config)

    A configuration file is loaded.

    :param array &$config: The loaded array from the file

    .. code-block:: php

        <?php

        // Listening to the event
        Event::register_function('config|nos::controller/admin/page/page', function(&$config)
        {
            // ...
        }
        // Triggering the event
        $config = Config::load('nos::controller/admin/page/page', true);


    Also works with absolute paths :

    .. code-block:: php

        <?php

        // Listening to the event
        Event::register_function('config|/data/www/novius-os/local/config/test.php', function(&$config)
        {
            // ...
        }
        // Triggering the event (file must exists)
        $config = Config::load('/data/www/novius-os/local/config/test.php', true);


config|<group>
==============


.. php:function:: config|<group>($config)

    A configuration array is loaded.

    :param array &$config: The loaded array

    .. code-block:: php

        <?php

        // Listening to the event
        Event::register_function('config|group', function(&$config)
        {
            // ...
        }
        // Triggering the event
        Config::load(array(), 'group');



Front-office (website)
**********************


front.start
===========

.. php:function:: front.start($params)

    An .html page is requested.

    :param array $params:

        :&$url: ``string``  Current URL (without leading domain, with trailing .html)
        :&$cache_path: ``string``  Which entry should be checked / written in the cache

    .. code-block:: php

        <?php

        Event::register_function('front.start', function($params)
        {
            $url =& $params['url'];
            $cache_path =& $params['cache_path'];
            // ...
        });


front.parse_wysiwyg
===================

.. php:function:: front.parse_wysiwyg($html)

    Additional processing on a WYSIWYG (HTML content).

    :param string $html: HTML content, already pre-processed by the core

    .. code-block:: php

        <?php

        Event::register_function('front.parse_wysiwyg', function(&$content)
        {
            // ...
        });


front.display
=============

.. php:function:: front.display($html)

    Additional processing on the page (HTML content).

    :param string $html: HTML content of the page (will be written in the cache)

    .. code-block:: php

        <?php

        Event::register_function('front.display', function(&$html)
        {
            // ...
        });


front.404NotFound
=================

.. php:function:: front.404NotFound($params)

    An .html page was requested, but not found.

    :param array $params:

        :&$url: ``string``  Current URL (without leading domain, with trailing .html)

    .. code-block:: php

        <?php

        Event::register('front.404NotFound', function($params)
        {
            $url = $params['url'];
            // ...
        });

404 entry point
***************

.. versionadded:: 0.2.0.2

404.start
===========

.. php:function:: 404.start($params)

    A inexistant file is requested. Can be media or attachment file.

    :param array $params:

        :&$url: ``string``  URL requested (without leading domain)

    .. code-block:: php

        <?php

        Event::register_function('404.start', function($params)
        {
            $url =& $params['url'];
            // ...
        });


404.mediaNotFound
=================

.. php:function:: 404.mediaNotFound($url)

	A inexistant media file is requested.

    :param string $url: URL requested (without leading domain)

    .. code-block:: php

        <?php

        Event::register('404.mediaNotFound', function($url)
        {
            // ...
        });


404.attachmentNotFound
======================

.. php:function:: 404.attachmentNotFound($url)

	A inexistant attachment file is requested.

    :param string $url: URL requested (without leading domain)

    .. code-block:: php

        <?php

        Event::register('404.attachmentNotFound', function($url)
        {
            // ...
        });


404.end
=======

.. php:function:: 404.end($url)

	A inexistant file is requested. No attachment or media file matched the URL.

    :param string $url: URL requested (without leading domain)

    .. code-block:: php

        <?php

        Event::register('404.end', function($url)
        {
            // ...
        });


Emails
******


email.before_send
=================

.. php:function:: email.before_send($email)

    Before sending an email.

    :param object $email: Email_Driver instance

    .. code-block:: php

        <?php

        Event::register('email.before_send', function($email)
        {
            // ...
        }


email.after_send
================

.. php:function:: email.after_send($email)

    After a mail was sent.

    :param object $email: Email_Driver instance

    .. code-block:: php

        <?php

        Event::register('email.after_send', function($email)
        {
            // ...
        }


Forms application
*****************

noviusos_form::rendering
========================

.. php:function:: noviusos_form::rendering($params)

    Triggered by the enhancer before displaying the form to the user.

    Allows to modify the ``$fields`` and the ``$layout``. The ``$item`` (Model_Form instance) and ``$enhancer_args`` (label_position, etc.) variables are read-only.

    :param array $params:

        :&$fields: Fields list

            :label: Callback used to generate the label

                :callback: ``string`` Callback function name
                :args: ``array`` Callback function args

            :field: Callback used to generate the field

                :callback: ``string`` Callback function name
                :args: ``array`` Callback function args

            :instructions:  Callback used to generate the instructions

               :callback: ``string`` Callback function name
               :args: ``array`` Callback function args

            :new_row: ``bool`` Should the field be on a new row?
            :new_page: ``bool`` Should the field be on a new page?
            :width: ``int`` Column size (value between 1 and 4)
            :item: ``Model_Field`` Field instance

        :&$layout: ``string``  Path to the view used to render the form
        :$item: ``Model_Form`` Form instance

    .. code-block:: php

        <?php

        Event::register_function('noviusos_form::rendering', function(array &$args)
        {
            $fields =& $args['fields'];
            $layout =& $args['layout'];
            $form   =  $args['item']; // Instance of Nos\Form\Model_Form
            $enhancer_args = $args['enhancer_args'];

            // This is an exemple of what $layout contains
            $layout = 'noviusos_form::foundation';

            foreach ($fields as &$field) {

                // This is an example of what $field contains
                $field = array(
                    'label' => array(
                        'callback' => array('Form', 'label'),
                        'args' => array('Label:', 'technical_id', array(
                            'for' => 'field_technical_id',
                        )),
                    ),
                    'field' => array(
                        'callback' => array('Form', 'input'),
                        'args' => array('field_name', 'field_value', array(
                            'id'          => 'field_technical_id',
                            'class'       => 'field_technical_css',
                            'title'       => 'Label:',
                            'placeholder' => 'Label:',
                            'required'    => 'required',
                        )),
                    ),
                    'instructions' => array(
                        'callback' => 'html_tag',
                        'args' => array('p', array('class' => 'instructions'), 'Instructions for the user'),
                    ),
                    'new_row' => true,
                    'new_page' => true,
                    'width' => 4,
                    'item' => $item, // Instance of Nos\Form\Model_Field
                );
            }

            // ...
        }

noviusos_form::rendering.<virtual_name>
=======================================

Same as ``noviusos_form::rendering``, but only triggered for a form with the specified ``<virtual_name>``.


noviusos_form::data_validation
==============================

**warning !** This function must return an array containing the detected validation errors.

.. php:function:: noviusos_form::data_validation(&$data, $form)

    Additional data validation after submitting a form from the Form application.

    :param array &$data: Received data (roughly $_POST)
    :param object $form: ``Model_Form`` Form instance

    :return array: List of validation errors

    .. code-block:: php

        <?php

        Event::register_function('noviusos_form::data_validation', function(&$data, $form) {

            $errors = array();
            // This will mark all fields as error
            foreach ($data as $name => $value) {
                $errors[$name] = '{{label}}: ‘{{value}}’ non valid.';
            }
            return $errors;
        });

    The messages can contain the ``{{label}}`` and ``{{value}}`` *placeholders* (they will be replaced appropriately).


noviusos_form::data_validation.<virtual_name>
=============================================

Same as  ``noviusos_form::data_validation``, but only triggered for a form with the specified ``<virtual_name>``.



noviusos_form::before_submission
================================

.. php:function:: noviusos_form::data_validation(&$data, $form)

    Before saving the answer in the database

    :param array &$data: Received data (to save in DB)
    :param object $form: ``Model_Form`` Form instance
    :param array $enhancer_args: Enhancer configuration

    :return bool: false to prevent saving the answer in the database

    .. code-block:: php

        <?php

        Event::trigger_function('noviusos_form::before_submission', array(&$data, $form, $enhancer_args) {

            // You can alter $data before saving them into the database

            // Or you can return 'false' if you don't want the answer to be saved in the database
            return false;
        });


noviusos_form::before_submission.<virtual_name>
===============================================

Same as ``noviusos_form::before_submission``, but only triggered for a form with the specified ``<virtual_name>``.


noviusos_form::after_submission
===============================


.. php:function:: noviusos_form::after_submission(&$answer, $enhancer_args)

    After the answer has been created (not saved in the DB yet)

    :param object &$answer: ``Model_Answer`` Answer instance
    :param array $enhancer_args: Enhancer configuration

    .. code-block:: php

        <?php

        Event::trigger_function('noviusos_form::after_submission', array(&$answer, $enhancer_args) {

            // ...
        });


noviusos_form::after_submission.<virtual_name>
==============================================

Same as ``noviusos_form::after_submission``, but only triggered for a form with the specified ``<virtual_name>``.
