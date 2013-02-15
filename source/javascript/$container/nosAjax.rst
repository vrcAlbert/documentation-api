nosAjax
#######

.. js:function:: $container.nosAjax(options)

	Perform an asynchronous HTTP (Ajax) request. This is a wrapper of `jQuery.ajax() <http://api.jquery.com/jQuery.ajax/>`_.

	:param JSON options:

		JSON that configure the Ajax request. Same that ``jQuery.ajax()`` with some differences:

		* Some defaults options.
		* Callbacks functions ``success`` and ``error`` are `monkey-patched <http://en.wikipedia.org/wiki/Monkey-Patch>`_ to execute defaults operations.

			* Function :js:func:`$container.nosAjaxSuccess` is automatically call if the request success and return type is JSON.
			* Function :js:func:`$container.nosAjaxError` is automatically call if the request fails.

	.. code-block:: js

		$(domContext).nosAjax({
			dataType: 'json', // datatype is default 'json'.
			type: 'POST', // The request is made in POST by default.
			data: {}
		});

nosAjaxSuccess
##############

.. js:function:: $container.nosAjaxSuccess(options)

	Processes a return JSON of an AJAX request successed.

	:param JSON options:

		:notify: A ``string`` or ``[string]``. Use for call :js:func:`$.nosNotify`.
		:error: A ``string`` or ``[string]``. Use for call :js:func:`$.nosNotify` with ``error`` for notification type.
		:action: A ``string`` or ``[string]``. Use for call :js:func:`$container.nosAction`.
		:closeDialog: ``Boolean``. If ``true``, call :js:func:`nosDialog.close`.
		:closeTab: ``Boolean``. If ``true``, call :js:func:`nosTabs.close`.
		:replaceTab: ``{}``. Use to call :js:func:`nosTabs.update`.
		:redirect: ``string``. Redirect browser window to this URL.
		:dispatchEvent: Use to call :js:func:`$container.dispatchEvent`.
		:internal_server_error: Display error and backtrace in the browser console.

nosAjaxError
############

.. js:function:: $container.nosAjaxError(jqXHR, textStatus)

	Processes a AJAX request in error.

	| Display the popup reconnection if the error comes to an end of the authentication session.
	| Display a notification otherwise.

	:param jqXHR jqXHR: An XMLHttpRequest object.
	:param string textStatus: Text status of the AJAX request.
