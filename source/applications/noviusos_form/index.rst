Form Application
################

Events
******

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

.. warning:: This function must return an array containing the detected validation errors.

.. php:function:: noviusos_form::data_validation(&$data, $fields, $form)

    Additional data validation after submitting a form from the Form application.

    :param array &$data: Received data (roughly $_POST)
    :param object $fields: Array of ``Model_Field`` Field instance, field names in keys
    :param object $form: ``Model_Form`` Form instance

    :return array: List of validation errors

    .. code-block:: php

        <?php

        Event::register_function('noviusos_form::data_validation', function(&$data, $fields,$form) {

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

        Event::register_function('noviusos_form::before_submission', array(&$data, $form, $enhancer_args) {

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

        Event::register('noviusos_form::after_submission', array(&$answer, $enhancer_args) {

            // ...
        });


noviusos_form::after_submission.<virtual_name>
==============================================

Same as ``noviusos_form::after_submission``, but only triggered for a form with the specified ``<virtual_name>``.
