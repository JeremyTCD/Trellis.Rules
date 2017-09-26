# Framework Design Rules
Clarity: Unclear options or multiple options that do the same thing can cause analysis paralysis.
Consistency: Consistency makes a codebase more intuitive to work with.
## Naming
#### Capitalization
---
1. Local variable identifiers must be in camelCase.
    * Rationale: Distinguishability from properties.
    * Enforcement: SA1313, SA1312.
---
2. Field identifiers must be in camelCase.
    * Rationale: Distinguishability from properties.
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
#### Grammar
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
#### Entity Specific Rules
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
    * Rationale: Grammatical correctness; these entities represent things.
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
    * Rationale: Grammatical correctness; methods represent actions.
    * Enforcement: Manual.
---
10. Property identifiers must be nouns, noun phrases or adjectives. E.g *Printer*, *StringBuilder* or
*IsDefault*.
    * Rationale: Grammatical correctness; properties are either things or descriptions.
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
    * Rationale: Grammatical correctness; fields are either things or descriptions.
    * Enforcement: Manual.
---
16. Resource identifiers must have the format \<feature>_\<subfeature>. E.g *OptionName_Help* or
*ArgumentException_IllegalCharacters*.
    * Rationale: Consistency.
    * Enforcement: Manual.
---
## Type Design
### Classes, Interfaces and Enums
---
1. A type should have only one responsibility. E.g *MyCustomType* should not have a static method that builds
*MyCustomType* instances. Such a method should be placed in a factory type.
    * Rationale: Types with smaller scopes are easier to reuse and test.
    * Enforcement: Manual.
---
2. Avoid static classes, apart from service registration classes.
    * Rationale: Static class members can only be mocked using specialized libraries.
    * Enforcement: Manual (**can be automated**).
---
3. Use enums for sets of related constants. Do not use static constants.
    * Rationale: Strong typing. 
    * Enforcement: Manual.
---
4. Do not use nested types.
    * Rationale: Nested types are tightly coupled with their containing types. They are not extensible and are difficult to test.
    * Enforcement: Manual (**can be automated**).
---
#### Overloading
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
#### Properties
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
    * Rationale: Analysis paralysis prevention.
    * Enforcement: Manual (**can be automated**).
#### Constructors
---
1. Constructors must be internal if a factory or builder exists for the type.
    * Rationale: Factories and builders perform validation and preparation. Object validity cannot be ensured if an instance
if instantiated manually.
    * Enforcement: Manual (**can be automated**).
---
2. Constructor parameter identifiers should be the same as the identifiers of properties or field they are assigned to.
    * Rationale: Consistency.
    * Enforcement: Manual (**can be automated**).
---
3. Do as little work as possible in constructors, ideally just assignment.
    * Rationale: Testability and reusability; if work is done in a constructor, everytime an instance of the type is instantiated,
work occurs. This makes unit testing members difficult, especially if the constructor's work has side effects. Also, doing work in a constructor violates
the single responsibility principle. An object should not have to build itself. This responsibility should be offloaded to a factory or 
builder that can be used independently.
---
4. Declare a parameterless constructor explicitly if it is used.
    * Rationale: Adding a constructor with parameters prevents the compiler addition of an implicit parameterless constructor declaration.
    * Enforcement: Manual (**can be automated**).
---
5. Abstract classes must not have public constructors.
    * Rationale: Abstract classes cannot be instantiated.
    * Enforcement: Manual (**can be automated**).
---
#### Fields
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
#### Extension Methods
---
1. Avoid extension methods, apart from service registration extension methods.
    * Rationale: Testability. Extension methods can only be mocked using specialized libraries.
    * Enforcement: Manual (**can be automated**).
---
#### Methods
---
1. Return types must be the most specific type. E.g return *List\<T>*, not *IEnumerable\<T>*.
    * Rationale: Ease of use. The more specific the return type, the more functions a consumer has access to without having to manually
convert the returned object.
    * Enforcement: Manual (**can be automated**).
---
#### Accessibility
---
1. Avoid sealed.
    * Rationale: Extensibility; it is impossible to predict how consumers may use a framework. 
    * Enforcement: Manual (**can be automated**).
---
<!-- Check for performance issues, if programming off interfaces, does virtual further slow things?-->
<!--https://github.com/dotnet/coreclr/blob/master/Documentation/botr/virtual-stub-dispatch.md
https://blogs.msdn.microsoft.com/vancem/2016/05/13/encore-presentation-measure-early-and-often-for-performance/-->
<!-- Its possible to use moq without making internal methods virtual https://stackoverflow.com/questions/4769928/using-moq-to-mock-only-some-methods -->
2. Public members should be virtual (other than constructors).
    * Rationale: Extensibility and testability; virtual members can be overidden, as a result they can be mocked by testing frameworks.
Keeping members non-virtual has little benefit for open source projects. For such projects, the onus for ensuring that member implementations 
are valid falls on implementors since they have full access to source code.
---
#### Parameters
---
1. Parameter types must be the least specific type. E.g *IEnumerable\<T>*, not *List\<T>*.
    * Rationale: The less specific the parameter type, the more types consumers can pass as arguments.
    * Enforcement: Manual (**can be automated**).
---
2. Avoid out. Use tuples to return multiple return values.
    * Rationale: With tuples it is immediately obvious what a method returns. 
    * Enforcement: Manual (**can be automated**).
---
3. Overloads and implementations must have the same parameter identifiers as base members.
    * Rationale: Ease of use. 
    * Enforcement: Manual (**can be automated**).
---
4. Parameters for exposed members (public or protected) must be validated. 
    * Rationale: Catching misuse as close to its occurence makes for easier fixes.
    * Enforcement: Manual (**can be automated**).
---
5. Params parameters from exposed members must be validated to not be null. 
    * Rationale: Catching misuse as close to its occurence makes for easier fixes. 
    * Enfocement: Manual (**can be automated**).
---
6. Enum type parameters must be validated to be within the enum's range.
    * Rationale: Catching misuse as close to its occurence makes for easier fixes. 
    * Enforcement: Manual (**can be automated**).
---
7. Avoid ref. Return a tuple if multiple return values are required.
    * Rationale: ref isn't common, consumers may not be familiar with it.
    * Enforcement: Manual (**can be automated**).
---
8. Avoid pointers. Return a tuple if multiple return values are required.
    * Rationale: Pointers aren't common, consumers may not be familiar with it.
    * Enforcement: Manual (**can be automated**).
---
## Exceptions
---
1. Throw exceptions when and only when, a member cannot do what it is supposed to do, in otherwords, if a member encounters a non-recoverable situation, throw.
E.g if a function *OpenFile* is unable to locate the requested file, it must throw. Note that even if the calling member can recover, the member
that is unable to do what it is supposed to do must throw.
    * Rationale: Convention; consumers expect exceptions to be thrown by methods if they are unable to do what they are supposed to do.
    * Enforcement: Manual.
---
2. Do not use exceptions for flow control. E.g call *FileExists* before attempting *OpenFile*; *OpenFile* must not be a defacto check for
the existence of a file. A corollary to this is: types with members that throw exceptions must provide ways to verify that calls will not throw,
such as *FileExists* in the above example or documentation specifying what is expected of arguments.
    * Rationale: Performance. 
    * Enforcement: Manual.
---
3. Try methods must be provided on top of existing methods if verifying that calls will not throw is expensive. E.g if *FileExists* is called before attempting *OpenFile* and *OpenFile*
implicitly checks if the file exists again, the verification occurs twice. If the verification is expensive, a *TryOpenFile* method must be
added. 
    * Rationale: Performance. Note that try methods must be added on top of existing methods so that if a consumer has verified that an exception
will not be thrown, the re-verification can be avoided. 
    * Enforcement: Manual.
---
## Type Specific Rules
### Attributes
---
1. Attribute identifiers must be appended with the suffix "Attribute".
    * Rationale: Convention.
    * Enforcement: Manual (**can be automated**).
---
2. Concrete Attribute types must have the *AttributeUsageAttribute*.
    * Rationale: Ease of use.
    * Enforcement: Manual (**can be automated**).
---
3. Optional arguments must be set-only properties.
    * Rationale: Convention.
    * Enforcement: Manual.
---
4. Required arguments must be get-only properties populated from constructor parameters.
    * Rationale: Convention.
    * Enforcement: Manual.
---
### Collections
---
1. Use *Collection\<T>*, *KeyedCollection\<TKey, TItem>* or their subclasses for read/write public members or public member return values.
    * Rationale: Classes like *List\<T>* and *Dictionary<TKey, TValue>* have non-overridable methods for performance sake,
this inhibits their extensibility.
    * Enforcement: Manual (**can be automated**).
---
2. Identifiers of types that implement *IDictionary<TKey, TItem>* must be appended with the suffix "Dictionary".
    * Rationale: Convention.
    * Enforcement: Manual (**can be automated**).
---
3. Identifiers of types that implement *IEnumerable\<T>* must be appended with the suffix "Collection".
    * Rationale: Convention.
    * Enforcement: Manual (**can be automated**).
---
## Patterns
#### Dependency Injection Pattern
5. Types with behaviours (methods and non-auto properties) must implement interfaces.
    * Rationale: See "Dependency Injection". Also, interfaces are easier to mock when testing.
    * Enforcement: Manual (**can be automated**).
---
#### Factory Pattern
#### Builder Pattern
#### Localization Pattern
## Testing
#### Unit Testing
#### Integration Testing
#### End to End Testing
## Documentation
