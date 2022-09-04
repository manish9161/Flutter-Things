1. What is the difference between Hot Reload and Hot Restart? 

-> Hot reload loads code changes into the VM and re-builds the widget tree, preserving the app state; it doesn’t rerun main() or initState(). 
-> Hot restart loads code changes into the VM, and restarts the Flutter app, losing the app state. It takes more time.

2.  What are the different ways we can create a custom widget?

-> 1. Flutter Outline -> Select Widget -> Extract Widget.
-> 2. Create new dart file -> Extends StatelessWidget.
-> 3. Create new dart file -> Extends StatefulWidget.

Points:
-> Create Stateless and statefull with as per need.
-> Create widget with required and optinal parameters.

3. How can I access platform(iOS or Android) specific code from Flutter? 

-> Messages are passed between the client (UI) and host (platform) using platform channels.
-> On the client side, MethodChannel enables sending messages that correspond to method calls. 
-> On the platform side, MethodChannel on Android (MethodChannelAndroid) and FlutterMethodChannel on iOS (MethodChanneliOS) enable receiving method calls and sending back a result.
-> These classes allow you to develop a platform plugin with very little ‘boilerplate’ code.

4.  What do you know about eventloop and what is the relationship with isolates?

-> To manage code execution, Dart uses something called Event Loop. It is the queue of actions that need to be performed.
-> An event loop’s job is to take an item from the event queue and handle it, repeating these two steps for as long as the queue has items.
-> A Dart app has a single event loop with two queues—the event queue and the microtask queue.
-> The event queue contains all outside events: I/O, mouse events, drawing events, timers, messages between Dart isolates, and so on.
-> The microtask queue is necessary because event-handling code sometimes needs to complete a task later, but before returning control to the event loop.

-> Relationship with Isolates

-> An isolate is what all Dart code runs in. It’s like a little space on the machine with its own, private chunk of memory and a single thread running an event loop.
-> Two isolates, each with its own memory and thread of execution.
-> Isolates can send messages to other isolates.



