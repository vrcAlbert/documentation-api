.. _php/classes/config:

Config
######

.. php:class:: Config

	Extends `FuelPHP config class <http://fuelphp.com/docs/classes/config.html>`__ and provides new functionalities.

::mergeWithUser($key, $config)
------------------------------

.. php:staticmethod:: mergeWithUser($key, $config)

    :param string $key: Key in which the user's configuration is saved.
    :param mixed $config: Configuration to merge.
    :returns: The configuration merged.

    Merge configuration with the one saved in user in the key `$key`.

::getDbName($key)
------------------------------

.. php:staticmethod:: getDbName($key)

    :param string $key: Key to be transformed.
    :returns: Valid user configuration key.

::configFile($class)
--------------------

.. php:staticmethod:: configFile($class)

    :param string $class: Class we want to retrieve the configuration from.
    :returns: Returns a two element array: first element is the class's application, and the second element is the
        relative path of the configuration file.

::loadConfiguration($application_name, $file_name)
--------------------------------------------------

.. php:staticmethod:: loadConfiguration($application_name, $file_name = null)

    :param string $application_name: If `file_name` is not null, it application where we want to load the configuration.
        Otherwise, it is the full path of the configuration file.
    :param string $file_name: Relative path of the configuration file.
    :returns: The configuration merged with the application extending the configuration's application.

::metadata($application_name)
-----------------------------

.. php:staticmethod:: metadata($application_name)

    :param string $application_name: Application we want to retrieve the metadata configuration from.
    :returns: The metadata configuration.

::application($application_name)
--------------------------------

.. php:staticmethod:: application($application_name)

    :param string $application_name: Application we want to retrieve the global configuration from (located at
        `application::config`)
    :returns: The global configuration.

::actions($params)
------------------

.. php:staticmethod:: actions($params = array())

    :param array $params: Set of filters on actions.

        :models: ``array``  Models on which we retrieve actions list.
        :item: ``object`` (optional) Item which we want to associate the actions with (will allow to process the
            ``disabled`` key).
        :all_targets: ``boolean``  Specify if we want to retrieve all actions (no matter target or visible value).
        :target: ``string``  Which target we want to filter the actions on.
    :returns: The filtered actions.

::getActionDisabledState($disabled, $item)
------------------------------------------

.. php:staticmethod:: getActionDisabledState($disabled, $item)

    :param mixed $disabled: Disabled value to be processed.
    :param object $item: Item necessary to process the disabled value.
    :returns: The processed disabled value.

::processCallbackValue($value, $positive_value, $argument_1, $argument_2, ...)
------------------------------------------------------------------------------

.. php:staticmethod:: getActionDisabledState($value, $positive_value, $argument_1, $argument_2, ...)

    :param mixed $value: Value to process.
    :param object $positive_value: If the value is an array of callbacks, it defines which value is expected. If
        callback return the expected value, then we call next callback. Otherwise, we return the value.
    :param mixed $arguments: All appended parameters are sent to the callback functions (if there is any).
    :returns: The first value which is different of `$positive_value`, otherwise `$positive_value`.

    For instance:

    .. code-block:: php

        <?php

        // ----- With a simple value
        getActionDisabledState(true, true); // returns true
        getActionDisabledState(true, false); // returns true

        // ----- With a callback
        $value = function() {
            return true;
        }

        getActionDisabledState($value, true); // returns true
        getActionDisabledState($value, false); // returns true

        // ----- With a list of callbacks
        $value = array(
            function() {
                return true;
            },
            function() {
                return false;
            }
        );

        getActionDisabledState($value, true); // returns false, since second callback is different from positive_value
        getActionDisabledState($value, false); // returns true, since first callback is different from positive_value

        // ----- With a list of mixed values
        $value = array(
            true,
            function() {
                return false;
            }
        );

        // the first value is equivalent to a callback returning true, so there is no difference with previous example
        getActionDisabledState($value, true); // returns false, since second value is different from positive_value
        getActionDisabledState($value, false); // returns true, since first callback is different from positive_value

        // ----- With additionnal parameters
        $value = array(
            function($param1, $param2) {
                return $param1 == $param2;
            },
            function ($param1, $param2) {
                return $param1 != $param2;
            }
        );

        getActionDisabledState($value, true, 1, 1); // returns false, since second value is different from positive_value
        getActionDisabledState($value, true, 1, 2); // returns false, since first value is different from positive_value
        getActionDisabledState($value, false, 1, 1); // returns false, since first value is different from positive_value
        getActionDisabledState($value, false, 1, 2); // returns false, since second value is different from positive_value

::placeholderReplace($to_be_replaced, $placeholders, $remove_unset)
-------------------------------------------------------------------

.. php:staticmethod:: placeholderReplace($to_be_replaced, $placeholders, $remove_unset = true)

    :param mixed $to_be_replaced: Value to replace placeholders into. Can be a `string` or `array`.
    :param array $placeholders: Associative array containing replacements.
    :param boolean $remove_unset: If set to `true`, all placeholders which have not a associated replacements are
        replaced by an empty string. Otherwise, they are not replaced.
    :returns: The replaced value.

::icon($application_or_model_name, $icon_key)
---------------------------------------------

.. php:staticmethod:: icon($application_or_model_name, $icon_key)

    :param string $application_or_model_name: Application or model name on which we want to retrieve the icon.
    :param array $icon_key: Icon size.
    :returns: The icon url.