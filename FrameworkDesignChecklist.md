# Framework Design Rules
Clarity: Unclear options or multiple options that do the same thing can cause analysis paralysis.
Consistency: Consistency makes a codebase more intuitive to work with.
## Naming
### Capitalization
---
1. Local variable identifiers must be in camelCase.
    * Rationale: Distinguishability from instance variables.
    * Enforcement: SA1313, SA1312.
---
2. Field identifiers must be in camelCase (they must also begin with an _, refer to Naming > Entity Specific Rules >
14).
    * Rationale: Distinguishability from properties and local variables.
    * Enforcement: SA1306.
---      
3. Property identifiers must be in PascalCase
    * Rationale: Distinguishability from fields and local variables.
    * Enforcement: SA1300.
---
4. For an acronym in a position that must begin with an uppercase character, if it has more 
than 2 characters, only its first character is capitalized. 
E.g *Html*. If it has 2 characters both must be capitalized, e.g *IO*.
    * Rationale: Consistency.
    * Enforcement: Manual.
---
5. For an acronym in a position that must begin with a lowercase character, all its characters should be
in lowercase, e.g *htmlWriter*.
    * Rationale: Consistency.
    * Enforcement: Manual.
---
6. Closed-form compound words must be capitalized in the same manner as single words. E.g 
*Lowercase*, not *LowerCase*.
    * Rationale: Consistency.
    * Enforcement: Manual.
---
### Grammar
---
1. Identifiers must be intuitively understandable. E.g a type that maps
floats to properties should be named *FloatMapper*, not *MapperFloat*.
    * Rationale: Ease of understanding.
    * Enforcement: Manual.
---
2. Identifiers must use complete words. E.g *IsDefault* instead of *Def*.
    * Rationale: Ease of understanding.
    * Enforcement: Manual.
---
3. Identifiers must not be in Hungarian notation.
    * Rationale: Ease of understanding.
    * Enforcement: Manual.
---
4. Identifiers must not contain uncommon acronyms.
    * Rationale: Ease of understanding.
    * Enforcement: Manual.
---
### Entity Specific Rules
---
1. Namespace names must be of the form \<company>.\<technology>[.\<feature>][.\<subfeature>]. E.g
*JeremyTCD.DotNet.Utils.Console*.  
    * Rationale: Distinguishability from other namespace names. Also makes the scope of a namespace obvious.
    * Enforcement: Manual (**Prepending with company name should be automated**).
---
2. Assembly names must be the common prefix of all namespaces in the assembly. E.g an
assembly with namespaces *JeremyTCD.DotNet.Utils.Console* and *JeremyTCD.DotNet.Utils.Datastructures*
should be named *JeremyTCD.DotNet.Utils*.  
    * Rationale: Consistency.
    * Enforcement: Manual (**can be automated**).
---
3. Class, Interface and Struct identifiers must be nouns or noun phrases. E.g *Printer*, *PrinterFactory*, 
*IParser*, not *Print*, *Create* or *IParse*.
    * Rationale: Grammatical correctness. These entities represent things.
    * Enforcement: Manual.
---
4. Interface identifiers must be prepended with *I*. E.g *IParser*.
    * Rationale: Distinguishability from classes and structs.
    * Enforcement: SA1302.
---
5. The identifier of the default implementation of an interface must differ from the interface's
identifier by *I*. E.g *IParser*'s  default implementation must be named *Parser*.
    * Rationale: Consistency.
    * Enforcement: Manual (**can be automated**).
---
6. Some identifiers of derived classes must be appended with identifiers of their base classes. E.g 
*OptionAttribute* for a class that extends *System.Attribute*.
    * Rationale: Consistency.
    * Enforcement: Manual, check convention for a class when implementing it.
---
7. Non-flag enum identifiers should be singular. E.g *Size*.
    * Rationale: Distinguishability from flag enums. Also grammatical correctness.
    * Enforcement: Manual (**can be automated**).
---
8. Flag enum identifiers should be plural. E.g *Sizes*.
    * Rationale: Distinguishability from non-flag enums. Also grammatical correctness.
    * Enforcement: Manual (**can be automated**).
---
9. Method identifiers must be verbs or verb phrases. E.g *Add* or *CreatePrinter*.
    * Rationale: Grammatical correctness. Methods represent actions.
    * Enforcement: Manual.
---
10. Property identifiers must be nouns, noun phrases or adjectives. E.g *Printer*, *StringBuilder* or
*IsDefault*.
    * Rationale: Grammatical correctness. Properties are either things or descriptions.
    * Enforcement: Manual.
---
11. Collection property identifiers should be plural.
    * Rationale: Grammatical correctness. 
    * Enforcement: Manual (**can be automated**).
---
12. Boolean property identifiers should be affirmative to avoid double negation. E.g *IsDefault*, 
not *IsNotDefault*.
    * Rationale: Ease of understanding.
    * Enforcement: Manual (**can be automated**).
---
13. If a type has only one property of a custom type, its identifier should be identical to the property's 
type's identifier. 
    * Rationale: Consistency.
    * Enforcement: Manual (**can be automated**).
---
14. Field identifiers must be prepended with an _.
    * Rationale: Distinguishability from local variables.
    * Enforcement: SX1309.
---
15. Field identifiers must be nouns, noun phrases or adjectives. E.g *_printer*, *_stringBuilder* or
*_isDefault*.
    * Rationale: Grammatical correctness. Fields are either things or descriptions.
    * Enforcement: Manual.
---
16. Resource identifiers must have the format \<feature>_\<subfeature>. E.g *OptionName_Help* or
*ArgumentException_IllegalCharacters*.
    * Rationale: Consistency.
    * Enforcement: Manual.
---
## Type Design
---
1. A type should have only one responsibility. E.g *MyCustomType* should not have a static method that builds
*MyCustomType* instances. Such a method should be placed in a factory.
    * Rationale: Reusability and testability.
    * Enforcement: Manual.
---
2. Abstract classes must not have public constructors.
    * Rationale: Abstract classes cannot be instantiated.
    * Enforcement: Manual (**can be automated**).
---
3. Avoid static classes, apart from service registration classes.
    * Rationale: Testability. Static class members can only be mocked using specialized libraries.
    * Enforcement: Manual (**can be automated**).
---
4. Use enums for sets of related constants. Do not use static constants.
    * Rationale: Strong typing. 
    * Enforcement: Manual.
---
5. Do not use nested types.
    * Rationale: Nested types are tightly coupled with their containing types. They are not extensible and are difficult to test.
    * Enforcement: Manual (**can be automated**).
---
## Member Design
### Overloading
---
1. Prefer optional parameters over overloading. 
    * Rationale: Overloading creates numerous methods that each have to be documented and tested.
Morever, overloads do not work well with intellisense. Optional parameters have their own issues, E.g optional values are only added to
consuming assemblies at compile time. Therefore, prefer optional parameters but overload when required.
    * Enforcement: Manual (**can be automated**).
2. Overloads must have the same parameter names and orders.
    * Rationale: Ease of use.
    * Enforcement: Manual (**can be automated**).
3. Make only the longest overload virtual (if extensibility is required).
    * Analysis paralysis prevention.
---
### Properties
---
1. Properties must not have broader set accessibility than get accessibility, in such cases setting should be done in a set method.
    * Rationale: Convention.
    * Enforcement: Manual (**can be automated**).
---
2. Getters must not throw. Use a get method instead if an exception may be thrown.
    * Rationale: Exceptions are not expected from getters. Therefore they often go uncaught.
    * Enforcement: Manual (**can be automated**).
---
3. Interrelated properties must not be validated until they are used.
    * Rationale: There is no way to enforce the order that properties are set in. Attempting to validate them while they are being set
causes convoluted code.
    * Enforcement: Manual.
---
4. Avoid having public get/set methods that correspond to a public property. E.g if there is a public 
method *GetPrinter*, there should not be a public property *Printer*. 
    * Rationale: Analysis paralysis preventionEnforcement
    * Enforcement: Manual (**can be automated**).
### Constructors
---
1. Constructors must be internal if a factory or builder exists for the type.
    * Rationale: Factories and builders perform validation and preparation. Object validity cannot be ensured if an instance
if instantiated manually.
    * Enforcement: Manual (**can be automated**).
---
2. Constructor parameter identifiers should be similar to the identifiers of properties or field they are assigned to.
    * Rationale: Consistency.
    * Enforcement: Manual (**can be automated**).
---
3. Do as little work as possible in constructors, ideally just assignment.
    * Rationale: Testability and ease of understanding. If work is done in a constructor, everytime an instance of the type is instantiated,
work occurs. This makes unit testing members difficult, especially if the work has side effects. Also, doing work in a constructor violates
the single responsibility principle. An object should not have to build itself. This responsibility should be offloaded to a factory or 
builder that can be tested independently. Consistently respecting the single responsibility principle makes a codebase easier to understand.
---
4. Declare a parameterless constructor explicitly if it is used.
    * Rationale: Adding a constructor with parameters prevents the compiler addition of an implicit parameterless constructor declaration.
    * Enforcement: Manual (**can be automated**).
---
### Fields
---
1. Fields must not be public or protected.
    * Reusability. If a field develops a need for get or set logic, all codebases that depend on it will break. In contrast, a property can
have get or set logic added at anytime.
    * Enforcement: SA1401.
---
2. Use const for fields that never change.
    * Performance. The compiler inlines such fields.
    * Enforcement: Manual (**can be automated**).
---
3. Use static readonly for predefined fields that hold object instances.
    * Performance. One instance shared by all instance of the type. Static fields are also faster than instance fields.
    * Enforcement: Manual (**can be automated**).
---
### Extension Methods
---
1. Avoid extension methods, apart from service registration extension methods.
    * Rationale: Testability. Extension methods can only be mocked using specialized libraries.
    * Enforcement: Manual (**can be automated**).
---
### Methods
---
1. Return types must be the most specific type. E.g return *List\<T>*, not *IEnumerable\<T>*.
    * Rationale: Ease of use. The more specific the return type, the more functions a consumer has access to without having to manually
convert the returned object.
    * Enforcement: Manual (**can be automated**).
---
### Parameters
---
1. Parameter types must be the least specific type. E.g *IEnumerable\<T>*, not *List\<T>*.
    * Rationale: Ease of use. The less specific the parameter type, the more types consumers can pass as arguments.
    * Enforcement: Manual (**can be automated**).
---
2. Avoid out. Use tuples to return multiple return values.
    * Rationale: Ease of use. With tuples it is immediately obvious what a method returns. 
    * Enforcement: Manual (**can be automated**).
---
3. Overloads and implementation must have the same parameter identifiers as base members.
    * Rationale: Ease of use. 
    * Enforcement: Manual (**can be automated**).
---
4. Parameters for exposed members (public or protected) must be validated. 
    * Rationale: Ease of use. Catching misuse as close to its occurence makes for easier fixes.
    * Enforcement: Manual (**can be automated**).
---
5. Params parameters from exposed members must be validated to not be null. 
    * Rationale: Ease of use. Catching misuse as close to its occurence makes for easier fixes. 
    * Enfocement: Manual (**can be automated**).
---
6. Enum type parameters must be validated to be within the enum's range.
    * Rationale: Ease of use. Catching misuse as close to its occurence makes for easier fixes. 
    * Enforcement: Manual (**can be automated**).
---
7. Avoid ref. Return a tuple if multiple return values are required.
    * Rationale: Ease of use. ref isn't common, consumers may not be familiar with it.
    * Enforcement: Manual (**can be automated**).
---
8. Avoid pointers. Return a tuple if multiple return values are required.
    * Rationale: Ease of use. Pointers aren't common, consumers may not be familiar with it.
    * Enforcement: Manual (**can be automated**).
---
