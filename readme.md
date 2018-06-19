# Code convention - CaseNine

## First

Based upon the Google Java Style Guide: [https://google.github.io/styleguide/javaguide.html](https://google.github.io/styleguide/javaguide.html)

We have a few Apex specials that are described in this document.

## Content

First

Sobject initialization

SOQL Query

Column limit

Salesforce API names

Use of repositories



## Sobject initialization

We see a Sobject initialization as an initialization of a Map &lt;Y, Z&gt;. How you can see a Map or List construct like: https://google.github.io/styleguide/javaguide.html#s4.8.3.1-array-initializers. So we assume that a Sobject initialization is a Block-like construct. (https://google.github.io/styleguide/javaguide.html#s4-formatting)
```java
Message__c message = new Message__c(
  User__c = [SELECT Id FROM User LIMIT 1].Id,
  RecordTypeId = recordTypeId,
  Status__c = 'Started',
  Send_Method__c = 'API',
  Type__c = 'Invoice',
  Start_Date__c = Date.today()
);
```
## SOQL Query

We see a query as a non-block-like statement. So here you must use continuation indents: ( [https://google.github.io/styleguide/javaguide.html#s4.5.2-line-wrapping-indent](https://google.github.io/styleguide/javaguide.html#s4.5.2-line-wrapping-indent))
```java
List<Message__c> messages = [
    SELECT Name
    FROM Message__c
    WHERE User__c = :originalMessage.User__c
        AND Type__c = :originalMessage.Type__c
        AND Started__c = false
        OR Item__c = 'Test case'
];
```



## Column limit

We currently use a column limit of 120. And not the 80/100 from Google. This because it fits better within the use of Apex.

[http://google.github.io/styleguide/javaguide.html#s4.4-column-limit](http://google.github.io/styleguide/javaguide.html#s4.4-column-limit)



## Salesforce API names

All API names are written in [PascalCase](http://wiki.c2.com/?PascalCase).

For example, FieldTest\_\_c or FakeObject\_\_c.



## Use of repositories

The use of repositories is a must in order to execute SOQL queries or DML statements. So all interactions with the database will be done in these repositories and not directly in business logic classes.

In addition, the unit test classes will use fake mock repositories instead, so the use of interfaces for this repositories is also required.



## Testing

Repositories require fake repositories to test application classes that use repositories. All Test classes should have IsParallel=true, except Repository test classes. Only use Test.startTest() / Test.stopTest() when needed.
