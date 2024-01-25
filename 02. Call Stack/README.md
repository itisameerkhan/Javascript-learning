# Call Stack

 A call stack is a mechanism for an interpreter (like the JavaScript interpreter in a web browser) to keep track of its place in a script that calls multiple functions — what function is currently being run and what functions are called from within that function, etc.

 JavaScript has its own Call stack. It behaves like a normal stack where we have Global Execution Context stored at a bottom of the stack whenever a JavaScript program is run.

 There are two kinds of Execution Context in JavaScript:

 *  Global Execution Context (GEC)
 * Function Execution Context (FEC)

 keyword `return` returns control of the program back to the place where a function was invoked. Whenever a function is invoked, a new execution context is created on the top of GEC. When a function returns a value, the function execution context is popped out of a stack and the control goes back to the Global Execution Context where it is left.

 Call stack maintains the order of execution of “Execution Contexts” and it is also known as:

 * Execution Context stack
 * Program stack
 * Control stack
 * Runtime stack
 * Machine stack

 [what is execution context in javascript](https://prototyp.digital/blog/what-is-execution-context-in-javascript)

 **Javascript maintains the order of execution of execution context**
 
 ![callstack](/assets/Call-stack.gif)
