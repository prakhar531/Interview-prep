# ReactJS Virtual DOM

React JS Virtual DOM is an **in-memory representation** of the DOM. DOM refers to the Document Object Model that represents the content of XML or HTML documents as a tree structure so that the programs can be read, accessed and changed in the document structure, style, and content.

## What is DOM ?

DOM stands for ‘Document Object Model’. In simple terms, it is a structured representation of the HTML elements that are present in a webpage or web app. DOM represents the entire UI of your application. The DOM is represented as a tree data structure. It contains a node for each UI element present in the web document. It is very useful as it allows web developers to modify content through JavaScript, also it being in structured format helps a lot as we can choose specific targets and all the code becomes much easier to work with.

## Disadvantages of real DOM

Every time the DOM gets updated, the updated element and its children have to be rendered again to update the UI of our page. For this, each time there is a component update, the DOM needs to be updated and the UI components have to be re-rendered.  
\***\*Example:\*\***

// Simple getElementById() method  
document.getElementById('some-id').innerValue = 'updated value';

When writing the above code in the console or in the JavaScript file, these things happen:

- The browser parses the HTML to find the node with this id.
- It removes the child element of this specific element.
- Updates the element(DOM) with the ‘updated value’.
- Recalculates the CSS for the parent and child nodes.
- Update the layout.
- Finally, traverse the tree and paint it on the screen(browser) display.

Recalculating the CSS and changing the layouts involves complex algorithms, and they do affect the performance. So React has a different approach to dealing with this, as it makes use of something known as Virtual DOM.

## \***\*Virtual DOM\*\***

React uses Virtual DOM exists which is like a lightweight copy of the actual DOM(a virtual representation of the DOM). So for every object that exists in the original DOM, there is an object for that in React Virtual DOM. It is exactly the same, but it does not have the power to directly change the layout of the document.

\***\*Manipulating DOM is slow, but manipulating Virtual DOM is fast\*\*** as nothing gets drawn on the screen. So each time there is a change in the state of our application, the virtual DOM gets updated first instead of the real DOM.

## \***\*How does virtual DOM actually make things faster?\*\***

When anything new is added to the application, a virtual DOM is created and it is represented as a tree. Each element in the application is a node in this tree. So, whenever there is a change in the state of any element, a new Virtual DOM tree is created. This new Virtual DOM tree is then compared with the previous Virtual DOM tree and make a note of the changes. After this, it finds the best possible ways to make these changes to the real DOM. Now only the updated elements will get rendered on the page again.

## \***\*How virtual DOM Helps React?\*\***

In React, everything is treated as a component be it a [functional component](https://www.geeksforgeeks.org/reactjs-functional-components/) or [class component.](https://www.geeksforgeeks.org/reactjs-class-based-components/) A component can contain a state. Whenever the state of any component is changed react updates its Virtual DOM tree. Though it may sound like it is ineffective the cost is not much significant as updating the virtual DOM doesn’t take much time.

React maintains two Virtual DOM at each time, one contains the updated Virtual DOM and one which is just the pre-update version of this updated Virtual DOM. Now it compares the pre-update version with the updated Virtual DOM and figures out what exactly has changed in the DOM like which components have been changed. This process of comparing the current Virtual DOM tree with the previous one is known as [\***\*‘diffing’\*\***](https://www.geeksforgeeks.org/explain-dom-diffing/). Once React finds out what exactly has changed then it updates those objects only, on real DOM.

React uses something called batch updates to update the real DOM. It just means that the changes to the real DOM are sent in batches instead of sending any update for a single change in the state of a component.

We have seen that the re-rendering of the UI is the most expensive part and React manages to do this most efficiently by ensuring that the Real DOM receives batch updates to re-render the UI. This entire process of transforming changes to the real DOM is called [\***\*Reconciliation\*\***](https://www.geeksforgeeks.org/reactjs-reconciliation/)\***\*.\*\***

This significantly improves the performance and is the main reason why React and its Virtual DOM are much loved by developers all around.

The diagrammatic image below briefly describes how the virtual DOM works in the real browser environment

![](https://media.geeksforgeeks.org/wp-content/uploads/20230725135348/Browser-DOM-Virtual-DOM-copy.webp)

Real DOM to Virtual DOM

## Virtual DOM Key Concepts :

- Virtual DOM is the virtual representation of Real DOM
- React update the state changes in Virtual DOM first and then it syncs with Real DOM
- Virtual DOM is just like a blueprint of a machine, can do changes in the blueprint but those changes will not directly apply to the machine.
- Virtual DOM is a programming concept where a virtual representation of a UI is kept in memory synced with “Real DOM ” by a library such as ReactDOM and this process is called reconciliation
- Virtual DOM makes the performance faster, not because the processing itself is done in less time. The reason is the amount of changed information – rather than wasting time on updating the entire page, you can dissect it into small elements and interactions

## Differences between Virtual DOM and Real DOM

| Virtual DOM                                            | Real DOM                                                    |
| ------------------------------------------------------ | ----------------------------------------------------------- |
| It is a lightweight copy of the original DOM           | It is a tree representation of HTML elements                |
| It is maintained by JavaScript libraries               | It is maintained by the browser after parsing HTML elements |
| After manipulation it only re-renders changed elements | After manipulation, it re-render the entire DOM             |
| Updates are lightweight                                | Updates are heavyweight                                     |
| Performance is fast and UX is optimised                | Performance is slow and the UX quality is low               |
| Highly efficient as it performs batch updates          | Less efficient due to re-rendering of DOM after each update |
