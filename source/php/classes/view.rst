View
##########

.. php:class:: View

	Allows to redirect views.

Methods
*******

.. php:staticmethod:: redirect($from, $to, $callback = true)

	:param string $from: Redirected view.
	:param mixed $to: View to show instead (optional). It can be set to false, the callback will be used to decide it.
	:param mixed $callback: Callback to decide whether to redirect or not (optional). Can be set to "true" to always redirect the view. If the second params is set to false, the callback must return a path view.

Example
*******

.. code-block:: php

	<?php

	View::redirect('a', 'b') // always redirect a to b
	
	View::redirect('a', 'b', function($data, $filter) { return false; }) //will not redirect a to b
	
	//will not redirect a to b, but will redirect a to c
	View::redirect('a', 'b', function($data, $filter) { return false; });
	View::redirect('a', 'c', function($data, $filter) { return true; });
	
	//will redirect a to d on conditions
	View::redirect('a', false, function($data, $filter) { return 'd'; })
	// can also be written like this :
	View::redirect('a', function($data, $filter) { return 'd'; })
	

	View::forge('!a')//prevent from any redirection
