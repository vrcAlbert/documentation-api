Events
######

The back-office of Novius OS is a "big HTML page". Actions preformed in one tab can affect displayed by a other (ex: adding, modifying or deleting an item).

An event system has been established to enable the various interface elements communicate with each other.

| On the one hand, the interface elements are listening events (by binding callbacks functions) by connecting to :term:`dispatcher`.
| The other, the different actions trigger events, usually returned by AJAX requests (see :js:func:`$context.nosAjax`),
  which are then dispatched to all interface elements via :term:`dispatchers <dispatcher>`.

Events dispatched are executed immediately on active tab or popup (has focus).
On the other tabs or popups, they are executed only when the tab or popup becomes active.

.. glossary::

	dispatcher
		| A DOM element that receives system events. The child elements of the dispatcher can listen for events by connecting to it.
		| Each tab and popup have a dispatcher.

Structure of an event
*********************

.. js:data:: Event

.. js:attribute:: Event.name

	| ``string``
	| Required
	| Event name.	For events on a ``Model``, the name is the Model name, including PHP namespace.

.. js:attribute:: Event.id

	| ``int`` or ``[int]``
	| For events on a ``Model``, ID(s) of the item to which they relate event.

.. js:attribute:: Event.action

	| ``string``
	| Name of the action item that triggered the event. Ex: ``insert``, ``update`` or ``delete``.

.. js:attribute:: Event.context

	| ``string`` or ``[string]``
	| Context of the item that triggered the event. See :doc:`/configuration/common/multi_context`.


nosListenEvent
**************

.. js:function:: $context.nosListenEvent(event, callback [, caller ])

	| Listen one (or many) event, ie register a callback function to be called when the event occurs.
	| Listening will be on current :term:`dispatcher` (closest relatives in the DOM element in jQuery).

	For the callback function is triggered, events listened and triggered should not match exactly.
	The event listened can just match one property of the event triggered.

	:param mixed event: ``{}`` or ``[{}]``. Required. JSON event to listen.
	:param function callback: Required. The callback function to execute when the event occurs. The function takes as parameter the event trigger.
	:param string caller: Caller name. If set, can stop listening to specific listener. See :js:func:`$context.nosUnlistenEvent`.

	.. code-block:: js

		// Listen all events with name 'Nos\Model_Page'
		$(domContext).nosListenEvent({
			name: 'Nos\Model_Page'
		}, function(event) {
			// ...
		}, 'caller');

		// Listen all events with name 'Nos\Model_Page' and action 'insert' or 'delete'
		$(domContext).nosListenEvent({
				name: 'Nos\Model_Page',
				action: ['insert', 'delete']
			},
			function(event) {
				// ...
			});

		// Listen all events with name 'Nos\Model_Page' and action 'insert' or 'delete',
		// or events with name 'Nos\Model_Page' and context 'main::en_GB'
		$(domContext).nosListenEvent([
			{
				name: 'Nos\Model_Page',
				action: ['insert', 'delete']
			},
			{
				name; 'Nos\Model_Page',
				context; 'main::en_GB'
			}
		], function(event) {
			// ...
		});

nosUnlistenEvent
****************

.. js:function:: $context.nosUnlistenEvent(caller)

	Stop listen events for a specific caller. See :js:func:`caller param of nosListenEvent <$context.nosListenEvent>`.

	:param string caller: Caller name.

	.. code-block:: js

		$(domContext).nosUnlistenEvent('caller');

nosDispatchEvent
****************

.. js:function:: $.nosDispatchEvent(event)

	Dispatch an event to all available :term:`dispatchers <dispatcher>`.

	:param JSON event: See :js:data:`Event`.

	.. code-block:: js

		// Dispatch event, page with ID 4 has been create with 'main::en_GB' context
		$.nosDispatchEvent({
			name: 'Nos\Model_Page',
			action: 'insert',
			id: 4,
			context: 'main::en_GB',
		});

