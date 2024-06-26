
| CS-665       | Software Design & Patterns |
|--------------|----------------------------|
| Name         | Dhruv Prajapati       |
| Date         | 04/2/2024                 |
| Course       | Spring      |
| Assignment 5 |                            |

# Assignment Details
The open-source project for used in this assignment is 
-   **JUnit 4**
https://github.com/junit-team/junit4
JUnit is a simple framework to write repeatable tests. It is an instance of the xUnit architecture for unit testing frameworks.

# GitHub Repository Link:
https://github.com/Dhruv-praju/CS665-Assignment-5

# Implementation
The following design patterns were identified in `package junit`.

## 1. Observer Pattern
The Observer pattern is used in `package junit.framework`. Here is a comprehensive description:

-   **TestResult** class acts as Subject and **TestListner** is an Observer interface. The TestResult keeps track of observers by keeping a list of TestListners in fListners which is an ArrayList object. **ResultPrinter** and **BaseTestRunner** are concrete implementations of **TestListner**. The TestListner interface listens to **Test** Result class.
-   The TestResult class has methods like **addListener** and **removeListener** to manage a list of **TestListener** observers. TestResult informs listeners about the result that a test will be started with **startTest** method. similarly **endTest** method informs the result that a test was completed.This allows the **TestListener** and **ResultPrinter** classes to be notified and perform their respective tasks in response to the events occurring in the TestResult class.
-   **TestListener** interface is separate from the **TestResult** class, which is the Subject. This separation makes it easy to introduce new observer classes that implement the **TestListener** interface. A new observer class can be added to the project by implementing the TestListener interface and providing its own implementation for the methods like **addFailure, startTest, and addError**.The new observer class can then be registered with the **TestResult** class using the **addListener** method, allowing it to receive notifications and perform custom actions based on the events occurring in the **TestResult** class.

The Observer pattern is useful in this context because it allows the TestResult class to be decoupled from the specific observer classes (TestListener and ResultPrinter). This makes the code more modular and easier to maintain. New observers can be added without modifying the TestResult class, and existing observers can be removed or replaced without affecting the core functionality of the TestResult class.



## 2. Decorator Pattern
The Decorator pattern is used in `package junit.extensions`. Here is a comprehensive description:

-   The **Test** class plays the role of the Component (the core object being decorated). The **TestDecorator** class plays the role of the Decorator (it wraps the **Test** object and extends its behavior). The **TestSetup** and **RepeatedTest** classes are concrete Decorators that extend the **TestDecorator** class.
-   The **TestDecorator** class has a reference to a **Test** object, which could be either a plain **Test** object or another **TestDecorator** object. The **TestDecorator** implements the same methods as the **Test** class (**run**, **countTestCases**, etc.) but can perform additional operations before or after delegating the method calls to the wrapped **Test** object. The **TestSetup** and **RepeatedTest** classes extend the **TestDecorator** class and provide their own implementations of the decorator methods, potentially adding new behavior or modifying the existing behavior of the wrapped **Test** object. The basicRun method in **TestDecorator** is likely used to execute the core functionality of the wrapped **Test** object.
-   Since the **TestDecorator** class is an abstract class, it is straightforward to create a new concrete decorator class that extends **TestDecorator**. The new decorator class can implement its own logic for the methods defined in the **TestDecorator** class, potentially adding new behavior or modifying the existing behavior. The new decorator can be composed with the existing decorators (**TestSetup**, **RepeatedTest**, or any other decorators) by wrapping them around a **Test** object or another decorator. This allows for flexible and dynamic composition of behavior, where new decorators can be easily added without modifying the existing code.

The Decorator pattern is useful in this context because it allows you to add or modify the behavior of the **Test** objects dynamically, without changing the core **Test** class. This promotes the Open/Closed principle, where the **Test** class is closed for modification but open for extension through decorators. By using decorators, you can create different combinations of behavior by wrapping the **Test** object with various decorators, such as **TestSetup**, **RepeatedTest**, or any other decorators that may be added in the future. This can help in creating complex test scenarios or adding specific setup or teardown logic without cluttering the core **Test** class.

## 3. Adapter Pattern

The Adapter pattern is used in `package junit.framework`. The **JUnit4TestAdapter** class acts as an adapter, enabling JUnit 4-style tests to be run using a JUnit 3-style test runner. Here is a comprehensive description:


-   The **Test** class represents the interface that the client (in this case, the **Runner** class) expects to work with. The **JUnit4TestAdapter** class plays the role of the Adapter. It adapts the JUnit 4-style tests to the **Test** interface expected by the **Runner** class.
-   The **JUnit4TestAdapter** class implements the **Test** interface, which is expected by the **Runner** class.
The **Runner** class interacts with the **JUnit4TestAdapter** as if it were a regular **Test** object, calling methods like run, countTestCases, etc. Internally, the **JUnit4TestAdapter** class delegates or translates the method calls to the corresponding JUnit 4-style test implementation. For example, the **run** method in **JUnit4TestAdapter** likely executes the JUnit 4-style tests and handles the results appropriately, conforming to the expected behavior of the **Test** interface.
-   If there is a need to support running tests from another testing framework (e.g., TestNG) using the same **Runner** class, a new adapter class can be created. The new adapter class would implement the **Test** interface and adapt the TestNG-style tests to the expected interface. This new adapter class could be added to the project without modifying the existing **Runner** or **Test** classes, following the Open/Closed principle. By adding another adapter, the **Runner** class can seamlessly execute tests from different testing frameworks, as long as the adapters conform to the **Test** interface.

The Adapter pattern is useful in this context because it allows the existing **Runner** class, which expects tests to conform to the **Test** interface (likely designed for JUnit 3-style tests), to run JUnit 4-style tests without modifying the **Runner** class itself. The **JUnit4TestAdapter** acts as a bridge between the two different testing frameworks, adapting the JUnit 4-style tests to the expected **Test** interface.

This promotes code reuse and allows the **Runner** class to work with different testing frameworks without being tightly coupled to any specific implementation. By introducing new adapters, the system can be extended to support additional testing frameworks in the future, without changing the core **Runner** or **Test** classes.