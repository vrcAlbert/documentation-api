nosNotify
#########

.. js:function:: $.nosNotify(message[, type])

	Display notifications to the user. This is a wrapper of jQuery plugin `Pines Notify <http://pinesframework.org/pnotify/>`_.

	:param mixed message: The string message to display or a JSON for special configuration.
	:param string type: Type of the message. Can be ``notice`` (default), ``info``, ``success`` or ``error``.

	.. code-block:: js

		$.nosNotify('message');

		$.nosNotify('message', 'error');

		$.nosNotify({
			title : 'It\'s work',
			type : 'success'
			sticker: false, // Not provide a button for the user to manually stick the notice.
			hide: false, // Not remove the notification after a delay.
		});

