
# nCino Salesforce Style Guide #

<!-- MarkdownTOC depth=0 autolink=true autoanchor=true bracket=round -->

- [Introduction](#intro)
  - [Goals](#goals)
  - [Sources](#sources)
  - [Updates](#updates)
- [File Basics](#basics)
  - [Naming](#file-naming)
  - [Structure](#file-structure)
	  - [Column Limit](#column-limit)
	  - [Order of Members](#order-of-members)
  - [Whitespace](#whitespace)
- [Formatting](#formatting)
  - [Line Wrapping](#line-wrapping)
  - [Indentation](#indentation)
  - [Spaces](#spaces)
- [SOQL](#soql)
- [Tests](#tests)
	- [Code Coverage](#coverage)
	- [Test Separation](#test-separation)
	- [`@isTest`](#istest)
	- [Test.startTest() and Test.stopTest()](#teststarttest-and-teststoptest)
- [Naming Conventions](#naming-conventions)
  - [Capitalization](#capitalization)
  - [Custom sObjects and Custom Fields](#sobjects)
  - [Classes](#class)
  - [Methods](#methods)
  - [Test classes](#test-classes)
  - [Exceptions](#exceptions)
  - [Beans](#beans)
- [Programming Practices](#programming-practices)
	- [Modifiers](#modifiers)
	- [Getters and Setters](#getters-and-setters)
	  - [Explicit Getters and Setters](#explicit)
	  - [Implicit Getters and Setters](#implicit)
	- [SObject Constructor Syntax](#sobject-constructor-syntax)
- [Deprecation](#deprecation)
	- [Deprecating Fields](#deprecating-fields)
	- [Deprecating Classes](#deprecating-classes)
	- [Deprecating Methods](#deprecating-methods)
	- [Deprecating Validation Rules](#deprecating-validation)
- [Refactoring](#refactoring)
  
<!-- /MarkdownTOC -->

<a name="intro"></a>
## Introduction

> “Programs are meant to be read by humans and only incidentally for computers to execute.”
> 
> — H. Abelson and G. Sussman (in “Structure and Interpretation of Computer Programs”)

<a name="goals"></a>
### Goals
The goal of this style guide is to define the aesthetic (formatting) and non-aesthetic standards (naming, conventions, etc.) that should be considered "hard-and-fast" rules for coding at nCino. Such standards are important in that they help ensure that:

1. New and old developers, and outside contractors of all sorts can easily read, understand, and maintain our growing code base.
2. By establishing a consistent structure, it becomes easier to focus on the meaning rather than appearance of the code.
3. Code merges are easy to handle and are content-ful, not style-ful.

For more information on the importance of style guides, read ["Why Coding Style Matters"](http://www.smashingmagazine.com/2012/10/why-coding-style-matters/) by Nicholas Zakas.

<a name="sources"></a>
### Sources
The nCino Style Guide was started by Jaco Raubenheimer and expanded by the developers at nCino. Because Apex is based on Java, the guide is founded on the original [Oracle Java Conventions](http://www.oracle.com/technetwork/java/codeconventions-150003.pdf). Formatting and additional standards are based on the [PolarisProject/salesforceStyleGuide](https://github.com/PolarisProject/salesforceStyleGuide) repository.

<a name="updates"></a>
### Updates
This guide is a living document. Changes to the guide should not be made unilaterally, but any problems or omissions should be raised to the Development Manager or a Lead Developer.

<a name="basics"></a>
## File Basics

<a name="file-naming"></a>
### Naming
The source file name for a class consists of the case-sensitive name of the top-level class it contains, plus the `.cls` extension.

<a name="file-structure"></a>
### Structure

<a name="column-limit"></a>
#### Column Limit
Files should have a column limit of either 100 characters.

<a name="order-of-members"></a>
#### Order of Members
```
// class definition
// instance variables
  // global instance variables
  // public instance variables
  // protected instance variables
  // private instance variables
// constructors (global, public, protected, private)
// methods
  // global methods (abstract, virtual, final)
  // public methods (abstract, virtual, final)
  // protected methods (abstract, virtual, final)
  // private methods
  // static methods
// static variables (global, public, protected, private)
// inner classes (global, public, protected, private)
// static constants (global, public, protected, private)
```
<a name="whitespace"></a>
### Whitespace
The only permissible whitespace characters in source code are newline and space (0x20).  Inside of a string literal, only a space is allowed.  Line must not end with spaces (`/ +$/` must not match anything in the file).  Classes should all end with a newline.

<a name="formatting"></a>
## Formatting

<a name="line-wrapping"></a>
###Line Wrapping
When code that might otherwise legally occupy a single line is divided into multiple lines to avoid overflowing the column limit, this is called line-wrapping.

There is no comprehensive, deterministic formula showing exactly how to line-wrap in every situation. Very often there are several valid ways to line-wrap the same piece of code. There are, however, guiding principles that should be followed:

 - Prefer higher-level breaks to lower-level breaks
 - Break after a comma.
 - Break before an operator.

<a name="indentation"></a>
### Indentation
All blocks of code should be indented with a tab. In order to ensure that indentations appear the same on everyone's screen, you must configure the settings of your IDE to set a tab as equivalent to **3 spaces**.

<a name="spaces"></a>
###Spaces
Blank spaces should be used in the following circumstances:

 - A keyword followed by a parenthesis should be separated by a space. The parenthetical clause in `if`, `while`, `do`, `catch`, etc. statements should be preceded and followed by a single space. Example:
```
while (true) {
	...
}
```
 - In method calls and definitions, there should not be whitespace between the name of the method and the open parenthesis. This helps distinguish keywords from method calls. Example:
```
public static Integer calculateTotal(List<Integer> vals){
	...
}
calculateTotal(vals);
```
 - A blank space should appear after commas in argument lists. There should be no whitespace before commas. Example:
```
System.debug(LoggingLevel.INFO, 'fsdfs');
```
 - A single space should separate binary operators from the surrounding elements (e.g., `+`, `||`, `=`, `>=`).  Unary operators (e.g., `++`, `--`) should be attached to their parameters.  Example:
```
a += c + d;
a = (a + b) / (c * d);
while (d++ = s++) {
	n++;
}
```
 - The expressions in a `for` statement should be separated by blank spaces. A colon inside a `for each` loop should have one space on either side. Example:
```
for (expr1; expr2; expr3) {}
for (Contact c : contacts) {}
```
 - Casts should be followed by a blank space. Example:
```
myMethod((byte) aNum, (Object) x);
```
 - Open braces should have a space before them and not a newline.  The matching close brace should line up with the start of the opening brace's line.
 - `else` and `else if` statements do not get a new-line before them.  Neither do `catch` or `while` statements in a `do...while` loop. Example:
```
if (val < 10) {
	...
} else {
	...
}
```

<a name="soql"></a>
## SOQL

In general, SOQL should be declared inline where it is used.  In some cases, like when referencing FieldSets, it's necessary to build SOQL queries dynamically.  The same rules will generally apply.

SOQL keywords (e.g., `SELECT`, `WHERE`, `TODAY`) should always be written in `ALL CAPS`.  Objects, fields and bind variables should be referenced as declared.  Each clause of the SOQL Query should be on its own line so that finding what changed in a diff is easier.  That is, each `SELECT`, `FROM`, `WHERE`, `AND`, `OR`, `GROUP BY`, `HAVING`, `ROLL UP`, `ORDER BY`, etc., with the exception of the first `SELECT` should start a new line.  That line should start in the same column as the most relevant `SELECT`.

Long lists of fields in a `SELECT` clause should be ordered in a logical manner and broken to fit within page width, with subsequent lines aligned with the first field.  Always select `Id`, and always select it first.

Example:

```java
String typeToSelect = 'abcde';
List<Contact> cnts = [
	SELECT
		Id,
		FirstName,
		LastName,
		Phone,
		Email,
		MailingCity,
		MailingState
	FROM
	    Contact
    WHERE
	    CreatedDate >= TODAY];
```

<a name="tests"></a>
##Tests

<a name="coverage"></a>
### Code Coverage
Although Salesforce requires at least 75% test code coverage, the minimum allowable test code coverage at nCino is 90%.

<a name="test-separation"></a>
### Tests Separation
A test should never be in the same file as the class/method that it is testing.

<a name="istest"></a>
### `@isTest`
In a test method, use the `@isTest` attribute instead of the `testmethod` modifier.

<a name="teststarttest-and-teststoptest"></a>
### `Test.startTest()` and `Test.stopTest()`
When writing test cases, always use `Test.startTest();` and `Test.stopTest();`.  Do not indent the code between those method calls, but do use one line of vertical whitespace above and below those method calls to separate those lines from surrounding code.

<a name="naming-conventions"></a>
## Naming Conventions

<a name="capitalization"></a>
### Capitalization

We follow the Java standard of capitalization with the listed exceptions.  That means that statements (`for`, `if`, etc.) should be lowercase, constants should be `UPPER_CASE_WITH_UNDERSCORES`, classes and class-level variables should be declared as `UpperCamelCase`, and methods, parameters and local variables should all be declard as `lowerCamelCase`.

Native Apex methods and classes should generally be referenced as written in official Salesforce documentation.  This means that schemas and classes are `UpperCamelCase` and methods are `lowerCamelCase`. 

However, when referencing any metadata (SObject, SObjectField, FieldSet, Action, Class, Page, etc.), use the declared capitalization.  Even when referencing a method, field, etc., that is not capitalized according to these rules, still use the declared capitalization.

<a name="sobjects"></a>
### Custom sObjects and Custom Fields
The names of sObjects and sObject fields should be capitalized with underscores separating the words (e.g. `My_Object_Name` and `My_Field_Name`).

<a name="class"></a>
### Classes
Name a class or trigger after what it does. Names should be CamelCase with the first letter capitalized (e.g. `MyApexClass`). Controllers and Controller Extensions should end with the word `Controller`.

<a name="methods"></a>
### Methods
Method names should all be verbs. Names should be camelCase with the first letter lowercased. Getters and setters should have no side effects (with the exception of setting up cached values and/or logging) and should begin with `get` or `set`.

<a name="test-classes"></a>
### Test classes
Test classes should be named with the word Test preceding the name of the class being tested (e.g. `TestClassUnderTest`).

<a name="exceptions"></a>
### Custom Exceptions
Custom exception names should begin with a capital X and end with Exception. Names should be camelCase with the first letter lowercased (e.g. `XCustomApplicationException`).

<a name="beans"></a>
### Beans
The unique name of the bean should be a concatenation of the name of the interface and the name of the function, separated by a colon (e.g. `IPipelineComponent:account-trigger-pipeline'`).

The BeanRegistry class contains a helper function to create the unique name. When registering a particular trigger pipeline: 
```java
BeanRegistry.getInstance().registerBean(
	BeanRegistry.getInstance().generateUniqueBeanName(
		IPipelineContainer.class,
		'account-trigger-pipeline'
	),
	IPipelineContainer.class,
    TriggerPipeline.class,
    new Map<String, Object>{
		'pipelineClassUniqueNames'=> new String[]{
	    	'IPipelineComponent:account-trigger-0',
    	    'IPipelineComponent:account-trigger-1'
    	} // unique names of the pipeline beans registered above
    },
    true
)
```

 <a name="programming-practices"></a>
## Programming Practices

<a name="modifiers"></a>
### Modifiers
We prefer the explicit declaration of modifiers. Always specify:

* `global`/`public`/`protected`/`private` modifiers - prefer `private`, and if possible, `static`
* `with sharing`/`without sharing`
* `this` when calling local methods or setting local members/properties.

<a name="getters-and-setters"></a>
### Getters and Setters
Unless creating an interface or POJO, we prefer implicit getters and setters.

<a name="explicit"></a>
#### Explicit Getters and Setters
Always declare the getter, then the setter.

<a name="implicit"></a>
#### Implicit Getters and Setters

 - Always declare the getter, then the setter.
 - If there is no logic, it should read `{ get; set; }`.
 - If there is logic for a clause, there should be a line-break before the clause and a line-break before and after each close-brace.
 - If one clause has logic and one does not, place the clause without logic on its own line.

Example:
```java
public Boolean isEditable {
	get {
		if (isEditable == null) {
			isEditable = Utility.hasPermissionSet(EDIT);
		}
		return isEditable;
	}
	protected set;
}
```

<a name="sobject-constructor-syntax"></a>
### SObject Constructor Syntax
When creating an SObject, generally prefer the Apex-specific syntax wherein all fields can be initialized from the constructor.  When using this syntax, choose a different line for each property so that diff-ing and versioning is easier.

Example:

```java
Contact c = new Contact(
	RecordTypeId = CONTACT_RECORDTYPE_ID,
    FirstName = firstName,
    LastName = surname,
    MailingCountry = DEFAULT_COUNTRY
);
```

<a name="deprecation"></a>
##Deprecation

<a name="deprecating-fields">
###Deprecating Fields

1. Find the field that you wish to deprecate in your Salesforce Dev Org.
2. Add `-D` to the beginning of the field label.
3. Add `--DEPRECATED--` to the beginning of the description. 

	> If you are deprecating a field that will be replaced with another field, add the field that will be replacing this field to the description as well.

4. Click Save.
5. In your IDE, pull down the latest .object file and the object translation file for the object that the field is on. If the field is on a standard Salesforce object, there will be no object translation file to pull into your IDE.
6. In your IDE, look at all of the .layout files for the object that the field is on. If the field exists in any of these files, remove it.
7. Verify that packaged validation rules are not affected by the deprecated field.

<a name="deprecating-classes"></a>
###Deprecating Apex Classes
To deprecate a class, add a javadoc style `Deprecated` tag to the top of the class and remove all logic from the class. If the class has been superseded by another, include that name in the comment.

> If there are global virtual methods in the class, the method declarations must remain; just remove the logic inside of these methods.

If there is an associated test class, add the javadoc style `Deprecated` tag to the top of the test class and remove all logic inside test class so that only the class declaration remains. If there are associated test methods within a shared test class, remove only the test methods specific to your deprecated Apex Class.

Run all of the tests in your Dev Org to ensure that you have removed all the test cases linked to the newly deprecated Apex Class.

Example:
```
/** 
* @Deprecated to OpportunityHistoryTriggerHandler
*/

global class OpportunityHistoryDeletionTrigger extends ATriggerHandler{
	/**
	 * @Deprecated
	 */
	global override void beforeDelete(List<sObject> objs, Set<Id> objIds){}
}
``` 

<a name="deprecating-methods"></a>
###Deprecating Apex Methods
1. Find the Apex method you wish to deprecate.
2. Add a javadoc style Deprecated tag to the top of the method like the one below.

	    /**
	    * @Deprecated
	    */

3. Remove all logic from the method.
4. If the method returns a value, return a null or appropriate Boolean.
5. If there are associated test methods, replace test methods with a new test that confirms the deprecated method returns null (or the appropriate Boolean).
6. Run all tests in your Dev Org to ensure that there are no other test cases linked to the newly deprecated Apex method.
7. If there are test methods within test classes that test more classes than the one being deprecated, remove the test methods specific to your deprecated Apex Class.

<a name="deprecating-validation"></a>
###Deprecating Validation Rules
1. Find the validation rule that you wish to deprecate in your Salesforce Dev Org.
2. Add `--DEPRECATED--` to the beginning of the description.

	> If you are deprecating a validation rule that will be replaced with another validation rule, add the rule that will be replacing this rule to the description as well. 

3. Uncheck the 'Active' checkbox.
4. Update the Error Condition Formula to be `false`.
5. Add `--DEPRECATED--` to the beginning of the Error Message
6. Click Save.
7. In your IDE, pull down the latest .object file for the object that the validation rule is on.

<a name="refactoring"></a>
##Refactoring
Every time you touch a file, you should find a way to improve it.

Fixing poor formatting--like brackets, braces, inconsistencies in line breaks, poorly formatted SOQL, etc--is encouraged. These types of formatting fixes are a pretty easy win when you’re looking to “always make it better.”

When you need to reformat whitespace, make those changes in isolation so that those changes are in a pull request of their own. (Whitespace changes typically have to be made to many lines in the file. When whitespace changes and meaningful code changes are made simultaneously, it is hard to distinguish between those changes in the code review diff.)

> Written with [StackEdit](https://stackedit.io/).
