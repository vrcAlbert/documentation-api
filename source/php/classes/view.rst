View
####

.. php:class:: View

	Extends `FuelPHP view class <http://fuelphp.com/docs/classes/view.html>`__ and provides new functionalities.

__construct($file, $data, $filter)
------------------------------------

.. php:method:: __construct($file = null, $data = null, $filter = null)

    Same specifications as in `FuelPHP view class <http://fuelphp.com/docs/classes/view.html#/method_construct>`__,
    except when you prefix the view name by `!`, view redirections are ignored.

::redirect($from, $to, $callback)
---------------------------------

.. php:staticmethod:: redirect($from, $to, $callback = true)

    :param string $from: The view to redirect from.
    :param mixed $to: The view to redirect to or callback.
    :param mixed $callback: Callback

    The function can redirect views: you can, for instance, make `\View::forge('a')` return the content of view `b`.

    Usages examples:

    .. code-block:: php

        <?php

        View::redirect('a', 'b'); // redirects view `a` to `b`


        View::redirect('a', 'b', function($data, $filter) { return false; }); // won't have any effect


        View::redirect('a', 'b', function($data, $filter) { return false; });
        View::redirect('a', 'c', function($data, $filter) { return true; });
        // will redirect `a` to `c`


        View::redirect('a', false, function($data, $filter) { return 'd'; })
        // or
        View::redirect('a', function($data, $filter) { return 'd'; })
        // will redirect `a` to `d`