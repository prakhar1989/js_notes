Browser Event Loop
====

- The browser event loop is single-threaded. 
- Every event that is placed into the event queue is placed for its turn to come in FIFO order
- For example, when the users clicks a few buttons, the browser will push these events into the event queue. When its the turn for these events to be executed the browser will executed them and then call the event listeners that were attached to this event (if any).
