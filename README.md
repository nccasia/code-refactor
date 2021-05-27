## Duplicated code
The simplest duplicated code problem is when you have the same expression in two methods of the same class
## Long Function
## Long Parameter List
## Global Data
## Mutable Data
Changes to data can often lead to unexpected consequences and tricky bugs 
=> we can use functional program 
=> all updates occur through narrow functions that can be easier to monitor and evolve
If a variable is being updated to store different things, use Split Variable (240) both to keep them separate and avoid the risky update
## Divergent change
When we make a change, we want to be able to jump to a single clear point in the system and make the change.
When you can’t do this, you are smelling one of two closely related pungencies.
Divergent change occurs when one module is often changed in different ways for different reasons. 
If you look at a module and say, “Well, I will have to change these three functions every time I get a new database; 
I have to change these four functions every time there is a new financial instrument
## SHOTGUN SURGERY
Shotgun surgery is similar to divergent change but is the opposite.
You whiff this when, every time you make a change,
you have to make a lot of little edits to a lot of different classes.
When the changes are all over the place, they are hard to find, and it’s easy to miss an important change.
## FEATURE ENVY
When we modularize a program, we are trying to separate the code into zones to maximize the interaction inside a zone and minimize interaction between zones
A classic case of Feature Envy occurs when a function in one module spends more time communicating with functions or data inside another module than it does within its own module
Of course not all cases are cut-and-dried. Often, a function uses features of several modules, so which one should it live with? The heuristic we use is to determine which module has most of the data and put the function with that data
## DATA CLUMPS
you’ll see the same three or four data items together in lots of places: as fields in a couple of classes, as parameters in many method signatures
A good test is to consider deleting one of the data values. If you did this, would the others make any sense? If they don’t, it’s a sure sign that you have an object that’s dying to be born.
## PRIMITIVE OBSESSION
We thus see calculations that treat monetary amounts as plain numbers, or calculations of physical quantities that ignore units (adding inches to millimeters), or lots of code doing if (a < upper && a > lower)
A telephone number is more than just a collection of characters. If nothing else, a proper type can often include consistent display logic for when it needs to be displayed in a user interface
## REPEATED SWITCHES
Replace Conditional with Polymorphism
## LOOPS
we can use Replace Loop with Pipeline (231) to retire those anachronisms. We find that pipeline operations.
such as filter and map, help us quickly see the elements that are included in the processing and what is done with them.
## LAZY ELEMENT
We like using program elements to add structure—providing opportunities for variation, reuse, or just having more helpful names. But sometimes the structure isn’t needed
It may be a function that’s named the same as its body code reads, or a class that is essentially one simple function
## SPECULATIVE GENERALITY
If you have abstract classes that aren’t doing much, use Collapse Hierarchy (380). Unnecessary delegation can be removed with Inline Function (115) and Inline Class
functions with unused parameters should be subject to Change Function Declaration (124) to remove those parameters
You should also apply Change Function Declaration (124) to remove any unneeded parameters, which often get tossed in for future variations that never come to pass.
Speculative generality can be spotted when the only users of a function or class are test cases
## TEMPORARY FIELD
Sometimes you see a class in which a field is set only in certain circumstances. Such code is difficult to understand, because you expect an object to need all of its fields
Trying to understand why a field is there when it doesn’t seem to be used can drive you nuts.
## MESSAGE CHAINS
You see message chains when a client asks one object for another object, which the client then asks for yet another object, which the client then asks for yet another another object, and so on
You may see these as a long line of getThis methods, or as a sequence of temps. Navigating this way means the client is coupled to the structure of the navigation. Any change to the intermediate relationships causes the client to have to change.
## MIDDLE MAN
One of the prime features of objects is encapsulation—hiding internal details from the rest of the world. Encapsulation often comes with delegation
ou ask a director whether she is free for a meeting; she delegates the message to her diary and gives you an answer. All well and good. There is no need to know whether the director uses a diary, an electronic gizmo, or a secretary to keep track of her appointments.
However, this can go too far, You look at a class’s interface and find half the methods are delegating to this other class
 After a while, it is time to use Remove Middle Man (192) and talk to the object that really knows what’s going on, use Inline Function (115) to inline them into the caller. If there is additional behavior, you can use Replace Superclass with Delegate (399) or Replace Subclass with Delegate (381) to fold the middle man into the real object. That allows you to extend behavior without chasing all that delegation.
 ## INSIDER TRADING
 Software people like strong walls between their modules and complain bitterly about how trading data around too much increases coupling. To make things work, some trade has to occur, but we need to reduce it to a minimum and keep it all above board
 ## LARGE CLASS
 When a class is trying to do too much, it often shows up as too many fields. When a class has too many fields, duplicated code cannot be far behind.
 Choose variables to go together in the component that makes sense for each
 For example, “depositAmount” and “depositCurrency” are likely to belong together in a component. More generally, common prefixes or suffixes for some subset of the variables in a class suggest the opportunity for a component
 If the component makes sense with inheritance, you’ll find Extract Superclass (375) or Replace Type Code with Subclasses (362) (which essentially is extracting a subclass) are often easier.
 The simplest solution (have we mentioned that we like simple solutions?) is to eliminate redundancy in the class itself. If you have five hundred-line methods with lots of code in common, you may be able to turn them into five ten-line methods with another ten two-line methods extracted from the original.
 ## ALTERNATIVE CLASSES WITH DIFFERENT INTERFACES
 One of the great benefits of using classes is the support for substitution, allowing one class to swap in for another in times of need
 But this only works if their interfaces are the same
 ## DATA CLASS
 These are classes that have fields, getting and setting methods for the fields, and nothing else. Such classes are dumb data holders and are often being manipulated in far too much detail by other classes
 Look for where these getting and setting methods are used by other classes. Try to use Move Function (198) to move behavior into the data class
 If you can’t move a whole function, use Extract Function (106) to create a function that can be moved.
 Data classes are often a sign of behavior in the wrong place, which means you can make big progress by moving it from the client into the data class itself
 Immutable fields don’t need to be encapsulated and information derived from immutable data can be represented as fields rather than getting methods.
 ## REFUSED BEQUEST
 Subclasses get to inherit the methods and data of their parents. But what if they don’t want or need what they are given? They are given all these great gifts and pick just a few to play with.
 The traditional story is that this means the hierarchy is wrong. You need to create a new sibling class and use Push Down Method (359) and Push Down Field (361) to push all the unused code to the sibling
 That way the parent holds only what is common. Often, you’ll hear advice that all superclasses should be abstract.
 ## COMMENTS
 Don’t worry, we aren’t saying that people shouldn’t write comments. In our olfac-tory analogy, comments aren’t a bad smell; indeed they are a sweet smell. The reason we mention comments here is that comments are often used as a deodorant. It’s surprising how often you look at thickly commented code and notice that the comments are there because the code is bad
 If you need a comment to explain what a block of code does, try Extract Function (106). If the method is already extracted but you still need a comment to explain what it does, use Change Function Declaration (124) to rename it. If you need to state some rules about the required state of the system, use Introduce Assertion (302).
 When you feel the need to write a comment, first try to refactor the code so that any comment becomes superfluous.
