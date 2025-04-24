---
title: 'Salesforce Interview Prep'
slug: 'sf-interview-prep'
description: 'scratchpad for salesforce interview prep'
pubDate: 'Mar 05 2025'
heroImage: '../../assets/images/blog/sf-int-prep/intprep.png'
---

## SOQL Example

```sql
SELECT Id, Name, (SELECT Id, Subject FROM Cases WHERE Status = 'Open'), 
       (SELECT Id, Amount FROM Opportunities WHERE StageName = 'Closed Won')
FROM Account
WHERE Id IN (SELECT AccountId FROM Contact WHERE LastName = 'Smith')
AND Industry = 'Technology'
ORDER BY Name DESC
LIMIT 10
```

## SOSL Example

```sql
FIND {Acme* OR "Web Development"} 
IN ALL FIELDS 
RETURNING Account(Id, Name, Industry WHERE Industry = 'Technology'), 
          Contact(Id, FirstName, LastName WHERE LastName = 'Smith'), 
          Opportunity(Id, Name, StageName WHERE StageName = 'Closed Won')
```

### Key Differences Between SOQL and SOSL

SOQL (Salesforce Object Query Language):

- Used for querying structured data.
- Works with a single object at a time but can include related objects.
- Supports filtering, sorting, and limiting results.

SOSL (Salesforce Object Search Language):

- Used for searching unstructured data.
- Can search across multiple objects simultaneously.
- Supports text-based searches and can return results from multiple objects in a single query.

## Querying from Parent, Child

```sql
SELECT Id, Name, 
       (SELECT Id, Subject FROM Cases) 
FROM Account

SELECT Id, Subject, Account.Name, Account.Industry 
FROM Case
```

### Key Points to Remember

- Subqueries are used to retrieve child records related to a parent object.
- Dot notation is used to traverse from a child object to its parent object and retrieve parent fields.
- Filters can be applied on both parent and child records.
- Relationship names are used to reference related objects:
- For standard objects, use the default relationship name (e.g., Cases for Account to Case).
- For custom objects, append __r to the relationship name (e.g., Opportunities__r for a custom child object).

## Apex Classes

| Type of Apex Class         | Key Use Cases                                            |
|----------------------------|----------------------------------------------------------|
| Regular Class              | General-purpose logic and methods.                       |
| Virtual Class              | Base class with overridable methods.                     |
| Abstract Class             | Template for subclasses with abstract methods.           |
| Interface                  | Contract for implementing classes.                       |
| Controller Class           | Logic for Visualforce pages or Lightning components.     |
| Extension Class            | Extends functionality of standard or custom controllers. |
| Batch Class                | Processes large datasets asynchronously.                 |
| Schedulable Class          | Schedules Apex jobs to run at specific times.            |
| Test Class                 | Writes unit tests for Apex code.                         |
| Web Service Class          | Exposes Apex methods as SOAP or REST APIs.               |
| Invocable Class            | Exposes Apex methods to Flows or Process Builder.        |
| With/Without Sharing Class | Controls enforcement of sharing rules.                   |
| Singleton Class            | Ensures a single instance of the class.                  |

1. Regular Apex Classes
These are standard classes used to define custom logic, methods, and properties. They can be instantiated and used in various contexts, such as triggers, controllers, and other classes.

Example:

```java
public class MyClass {
    public String myMethod() {
        return 'Hello, World!';
    }
}
```

Use Case: General-purpose logic, utility methods, or service classes.

2. Virtual Apex Classes
A virtual class is a class that can be extended by other classes. It allows for method overriding in child classes.

Example:

```java
public virtual class Animal {
    public virtual void makeSound() {
        System.debug('Animal sound');
    }
}

public class Dog extends Animal {
    public override void makeSound() {
        System.debug('Bark');
    }
}
```

Use Case: When you want to create a base class with default behavior that can be overridden by subclasses.

3. Abstract Apex Classes
An abstract class cannot be instantiated directly and is meant to be extended by other classes. It can contain abstract methods (methods without implementation) that must be implemented by subclasses.

Example:

```java
public abstract class Shape {
    public abstract void draw();
}

public class Circle extends Shape {
    public override void draw() {
        System.debug('Drawing a circle');
    }
}
```

Use Case: When you want to define a template or contract for subclasses to follow.

4. Interface Classes
An interface is a contract that defines a set of methods that implementing classes must provide. Unlike abstract classes, interfaces cannot contain any implementation.

Example:

```java
public interface MyInterface {
    void myMethod();
}

public class MyClass implements MyInterface {
    public void myMethod() {
        System.debug('Implementing interface method');
    }
}
```

Use Case: When you want to enforce a specific structure or behavior across multiple classes.

5. Controller Classes
Controller classes are used in Salesforce Visualforce pages or Lightning components to handle user interactions and business logic.

Example:

```java
public class MyController {
    public String message { get; set; }

    public MyController() {
        message = 'Hello from Controller';
    }

    public void updateMessage() {
        message = 'Message updated!';
    }
}
```

Use Case: To manage the logic and data for Visualforce pages or Lightning components.

6. Extension Classes
Extension classes are used to extend the functionality of standard or custom controllers in Visualforce pages.

Example:

```java
public class MyExtension {
    private final Account acc;

    public MyExtension(ApexPages.StandardController stdController) {
        this.acc = (Account) stdController.getRecord();
    }

    public String getGreeting() {
        return 'Hello, ' + acc.Name;
    }
}
```

Use Case: To add additional functionality to a Visualforce page without modifying the standard controller.

7. Batch Apex Classes
Batch Apex classes are used to process large volumes of data asynchronously in smaller chunks.

Example:

```java
public class MyBatchClass implements Database.Batchable<SObject> {
    public Database.QueryLocator start(Database.BatchableContext bc) {
        return Database.getQueryLocator('SELECT Id, Name FROM Account');
    }

    public void execute(Database.BatchableContext bc, List<Account> scope) {
        for (Account acc : scope) {
            // Process each account
        }
    }

    public void finish(Database.BatchableContext bc) {
        // Post-processing logic
    }
}
```


Use Case: For processing large datasets, such as data cleanup or mass updates.

8. Schedulable Apex Classes
Schedulable classes are used to schedule Apex jobs to run at specific times.

Example:

```java
public class MyScheduledClass implements Schedulable {
    public void execute(SchedulableContext sc) {
        // Logic to execute
    }
}
```


Use Case: For scheduling recurring tasks, such as nightly data updates.

9. Test Classes
Test classes are used to write unit tests for Apex code. They are annotated with @isTest and ensure that your code works as expected.

Example:
```java
@isTest
public class MyTestClass {
    @isTest
    static void testMyMethod() {
        // Test logic
        System.assertEquals('Hello, World!', new MyClass().myMethod());
    }
}
```


Use Case: To validate the functionality of your Apex code and ensure it meets the required test coverage.

10. Web Service Classes
Web service classes are used to expose Apex methods as SOAP or REST web services.

Example (REST):

```java
@RestResource(urlMapping='/myService/*')
global class MyWebService {
    @HttpGet
    global static String doGet() {
        return 'Hello from REST service';
    }
}
```

Use Case: To integrate Salesforce with external systems using APIs.

11. Invocable Apex Classes
Invocable classes are used to expose Apex methods to declarative tools like Flow or Process Builder.

Example:

```java
public class MyInvocableClass {
    @InvocableMethod(label='My Method' description='An invocable method')
    public static List<String> myMethod(List<String> inputs) {
        List<String> outputs = new List<String>();
        for (String input : inputs) {
            outputs.add('Processed: ' + input);
        }
        return outputs;
    }
}
```

Use Case: To call Apex logic from Flows or Process Builder.

12. With Sharing and Without Sharing Classes
These classes control whether the sharing rules of the current user are enforced.

With Sharing: Enforces sharing rules (default behavior).

Without Sharing: Ignores sharing rules.

Example:

```java
public with sharing class MyWithSharingClass {
    public void myMethod() {
        // Enforces sharing rules
    }
}

public without sharing class MyWithoutSharingClass {
    public void myMethod() {
        // Ignores sharing rules
    }
}
```

Use Case: To control access to records based on sharing rules.

13. Singleton Classes
Singleton classes ensure that only one instance of the class is created and provide a global point of access to it.

Example:

```java
public class MySingleton {
    private static MySingleton instance;

    private MySingleton() {
        // Private constructor
    }

    public static MySingleton getInstance() {
        if (instance == null) {
            instance = new MySingleton();
        }
        return instance;
    }
}
```

Use Case: When you need a single instance of a class to manage shared resources or configurations.