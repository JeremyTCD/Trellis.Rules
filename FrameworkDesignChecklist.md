# Framework Design Rules
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
4. For an acronym in a position that begins with an uppercase character, if it has more 
than 2 characters, only its first character must be in uppercase. 
E.g *Html*. If it has 2 characters, both must be in uppercase, e.g *IO*.
    * Rationale: Consistency.
    * Enforcement: Manual.
---
5. For an acronym in a position that must begin with a lowercase character, all of its characters must be
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
2. Identifiers must use complete words. E.g *IsDefault* instead of *IsDef*.
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
3. Class, Interface and Struct identifiers must be nouns or noun phrases. E.g *Printer*, *PrinterFactory* and
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
16. Resource identifiers must have the format \<feature>_\<description>. E.g *OptionName_Help* or
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
5. Types with behaviours (methods and non-auto properties) must implement interfaces.
    * Rationale: Testability, interfaces are easier to mock.
    * Enforcement: Manual (**can be automated**).
---
#### Overloading
---
1. Prefer optional parameters over overloading. 
    * Rationale: Overloading creates numerous methods that each have to be documented and tested.
Morever, overloads do not work well with intellisense. Optional parameters have their own issues, E.g optional values are only added to
consuming assemblies at compile time and it is impossible to mandate that certain parameters are required when others are provided/missing. Therefore, prefer optional 
parameters but overload when required.
    * Enforcement: Manual (**can be automated**).
2. Overloads must have the same parameter names and orders.
    * Rationale: Ease of use.
    * Enforcement: Manual (**can be automated**).
---
#### Properties
---
1. Properties must not have broader set accessibility than get accessibility, in such cases setting should be done in a set method.
    * Rationale: Convention.
    * Enforcement: Manual (**can be automated**).
---
2. Getters must not throw. Use a get method instead if an exception may be thrown.
    * Rationale: Exceptions are not expected from getters, they often go uncaught.
    * Enforcement: Manual (**can be automated**).
---
3. Interrelated properties must not be validated until they are all set.
    * Rationale: There is no way to enforce the order that properties are set in. Attempting to validate them while they are being set
causes convoluted code.
    * Enforcement: Manual.
---
4. Avoid having public get/set methods that correspond to a public property. E.g if there is a public 
method *GetPrinter*, there must not be a public property *Printer*. 
    * Rationale: Analysis paralysis prevention.
    * Enforcement: Manual (**can be automated**).
#### Constructors
---
1. Constructors must be internal if a factory or builder exists for the type.
    * Rationale: Factories and builders perform validation and preparation. Object validity cannot be ensured if an instance
if instantiated manually.
    * Enforcement: Manual (**can be automated**).
---
2. Constructor parameter identifiers should be the same as the identifiers of properties or fields they are assigned to (ignoring case and prepended characters such as _).
    * Rationale: Consistency.
    * Enforcement: Manual (**can be automated**).
---
3. Do as little work as possible in constructors, ideally just assignment.
    * Rationale: Testability and reusability; if work is done in a constructor, everytime an instance of the type is instantiated,
work occurs. This makes unit testing members difficult, especially if the constructor's work has side effects. Also, doing work in a constructor violates
the single responsibility principle. An object should not have to build itself. This responsibility should be offloaded to a factory or 
builder so that it can be tested and used independently.
    * Enforcement: Manual (**can be automated**).
---
4. Declare a parameterless constructor explicitly if it is used.
    * Rationale: Adding a constructor with parameters prevents the automatic addition of an implicit parameterless constructor declaration.
    * Enforcement: Manual (**can be automated**).
---
5. Abstract classes must not have public constructors.
    * Rationale: Abstract classes cannot be instantiated.
    * Enforcement: Manual (**can be automated**).
---
#### Fields
---
1. Fields must not be public or protected.
    * Rationale: Reusability; if a field develops a need for get or set logic, all codebases that depend on it will break. In contrast, a property can
have get or set logic added at anytime.
    * Enforcement: SA1401.
---
2. Use const for fields that never change.
    * Rationale: Performance; The compiler inlines such fields.
    * Enforcement: Manual (**can be automated**).
---
3. Use static readonly for predefined fields that hold object instances.
    * Rationale: Performance; one instance shared by all instance of the type. Static fields are also faster than instance fields.
    * Enforcement: Manual (**can be automated**).
---
#### Extension Methods
---
1. Avoid extension methods, apart from service registration extension methods.
    * Rationale: Testability; extension methods can only be mocked using specialized libraries.
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
2. Public properties and methods must be virtual.
    * Rationale: Extensibility and testability; virtual members can be overidden. Also, they can be mocked by testing frameworks.
One commonly raised issue with virtual members is that they raise the probability of misuse. This isn't relevant for open source projects. For such projects, the onus for 
ensuring that implementations are valid falls on implementors since they have full access to source code. Another commonly cited issue with virtual members is performance.
This isn't relevant for projects with proper inversion of control since most public members should be implementations, which are already marked virtual by the compiler.
    * Enforcement: Manual (**can be automated**).
---
3. Non public methods must be internal virtual.
    * Rationale: Testability; they must be mockable when testing the members that use them.
    * Enforcement: Manual (**can be automated**).
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
    * Rationale: Catching misuse close to their occurences makes for easier fixes.
    * Enforcement: Manual (**can be automated**).
---
5. Params parameters from exposed members must be validated to not be null. 
    * Rationale: Catching misuse close to their occurences makes for easier fixes.
    * Enfocement: Manual (**can be automated**).
---
6. Enum type parameters must be validated to be within the enum's range.
    * Rationale: Catching misuse close to their occurences makes for easier fixes.
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
#### Attributes
---
1. *Attribute* identifiers must be appended with the suffix "Attribute".
    * Rationale: Convention.
    * Enforcement: Manual (**can be automated**).
---
2. Concrete *Attribute* types must have the *AttributeUsageAttribute*.
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
#### Collections
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
---
1. *new* must not be used in classes other than factories and builders.
    * Rationale: *new* causes coupling which makes testing and extending difficult.
    * Enforcement: Manual (**can be automated**).
---
2. Services must be concrete types mapped to interfaces.
    * Rationale: Interfaces are easier to mock and implement than base or abstract classes.
    * Enforcement: Manual (**can be automated**).
---
3. Injected objects must be assigned to private readonly fields.
    * Rationale: Injected objects should not be publically exposed or replaced after injection. 
    * Enforcement: Manual (**can be automated**).
---
4. Services must be registered in an *IServiceCollection* extension method.
    * Rationale: All major third party dependency injection frameworks support *IServiceCollection*.
    * Enforcement: Manual (**can be automated**).
---
#### Factory Pattern
---
1. Types that need runtime data to have a valid state and that can be created in a single step must be instantiated using factories.
    * Rationale: Testability and extensibility. Other solutions for instantiating types that need runtime data tend to make testing harder by convoluting the effective 
dependency graph, e.g by registering functions that ultimately do what a factory would do. 
    * Enforcement: Manual (**can be automated**).
---
2. Factories must have at least one method with identifier *Create*. This method can be overloaded.
    * Rationale: Consistency.
    * Enforcement: Manual (**can be automated**).
---
3. Create methods must return interfaces.
    * Rationale: Extensibility; factories should not be coupled to concrete types.
    * Enforcement: Manual (**can be automated**).
---
#### Builder Pattern
---
1. Types that need runtime data to have a valid state and that cannot be created in a single step must be instantiated using builders.
    * Rationale: Testability and extensibility.
    * Enforcement: Manual (**can be automated**).
---
2. Builders must have at least two add methods. Add methods must have identifiers of the form *\<Add>\<noun>*.
    * Rationale: Consistency; if only one add method is required, use a factory.
    * Enforcement: Manual (**can be automated**).
---
3. Builders must have one and only one build method with identifier *Build*.
    * Rationale: Consistency. 
    * Enforcement: Manual (**can be automated**).
---
4. Builder public methods must return the builder.
    * Rationale: Ease of use; allows for chaining.
    * Enforcement: Manual (**can be automated**).
---
5. Build methods must return interfaces.
    * Rationale: Extensibility; builders should not be coupled to concrete types.
    * Enforcement: Manual (**can be automated**).
---
#### Localization Pattern
---
1. Consumer facing strings must be defined in a resx file. E.g strings to be printed to the console, logs, or exception messages. Strings meant for
internal use such as arguments for a console application should be embedded in code.
    * Rationale: Reusability and management; strings in a resx file can be tuned or translated together more easily than strings scattered
through a codebase.
    * Enforcement: Manual.
---
## Testing
#### Naming
---
1. Test class identifiers must be of the form *\<name of class under test>(UnitTests|IntegrationTests|EndToEndTests)*.
    * Rationale: Consistency, uniqueness.
    * Enforcement: Manual (**can be automated**).
---
2. Test method identifiers must be of the form *\<name of method under test>_\<test case>*, e.g *Run_ThrowsInvalidOperationExceptionIfArgumentsDoNotContainCommand*.
    * Rationale: Consistency, uniqueness.
    * Enforcement: Manual (**can be automated**).
---
3. *MemberData* method identifiers must be of the form *\<test method identifier>Data*.
    * Rationale: Consistency, uniqueness.
    * Enforcement: Manual (**can be automated**).
---
4. *dummy* must be prepended to identifiers of local variables that will not have their behaviours verified. *mock* must be prepended to
identifiers of local variables that will have their behaviours verified.
    * Rationale: Consistency.
    * Enforcement: Manual (**can be automated**).
---
5. *Dummy* must be prepended to identifiers of types declared for use as dummies in tests.
    * Rationale: Consistency.
    * Enforcement: Manual (**can be automated**).
---
#### Parameterized Test
---
1. Use *MemberData* for parameterized tests.
    * Rationale: More flexible than *InlineData* and less verbose than *ClassData*.
    * Enforcement: Manual (**can be automated**).
---
2. Tests that can be parameterized without adding flow control statements must be parameterized.
    * Rationale: Maintainability and ease of use; standard don't repeat yourself. Note that adding flow control for parameters convolutes tests, in such cases
use multiple tests. 
    * Enforcement: Manual.
---
#### Parallelism
---
1. As far as possible, run tests in parallel.
    * Rationale: Performance; tests from different classes within the same assembly should be run in parallel. Over the course of a project's lifespan, time spent ensuring that 
tests can run in parallel is typically less than the time spent waiting for tests to run both locally and in continuous integration. 
    * Enforcement: Manual (**can be automated**).
---
2. <!-- enable parallelization between assemblies (instructions online are unclear, try on a test project) -->
---
3. Avoid using console output in assertions. Wrap *Console* methods in a service and stub it out when testing.
    * Rationale: Output from different threads in a process is written to the same *TextWriter*. This makes console output unreliable for testing.
    * Enforcement: Manual (**can be automated**).
---
4. Class or collection fixtures must be used if setup or teardown incurs significant overhead.
    * Rationale: Performance.
    * Enforcement: Manual.
---
#### Helper Methods
---
1. Every test class must have a create method that creates an instance of the type under test as well as its constructor parameters. This method must be called in the
test class' constructor. The resulting instance and its constructor parameters must be assigned to local fields.
    * Rationale: Ease of use; this way each test only needs to setup the constructor parameters that are relevant to the test. Triggering of null assertions and the like
are avoided and the addition of parameters will not require updates to all tests.
    * Enforcement: Manual (**can be automated**).
---
#### Temporary Files and Folders
---
1. Temporary folders must have names of the form \<guid>.
    * Rationale: Uniqueness.
    * Enforcement: Manual (**can be automated**).
---
2. Temporary files and folders must be deleted in a *Dispose* method.
    * Rationale: Prevent build up of test artifacts.
    * Enforcement: Manual.
---
#### Unit Testing
---
1. All methods must be unit tested (getters and setters of non-auto properties as well as indexers included).
    * Rationale: Maintainability.
    * Enforcement: Manual (**can be automated**).
---
2. A unit test's scope must be a single method. Therefore, a method's mockable dependencies must be mocked. Un-mockable dependencies such as types with static/extension methods and 
non overridable methods must be wrapped in services that are then mocked. E.g *System.IO.File* must be wrapped in a *FileService* type.
CoreFX and CoreCLR types from which only members that have no side effects are used are exempt from mocking.
    * Rationale: Fine-grained, deterministic tests are allow root causes of issues to be pinpointed more accurately.
    * Enforcement: Manual.
---
3. Mock behaviours must be verified.
    * Rationale: Behaviour verification causes brittleness, which makes it harder to break a codebase without breaking tests. This is useful for open 
source projects, where contributors often do not have a full mental model of the framework they are making changes to.
    * Enforcement: Manual (**can be automated**).
---
5. *MockRepository* must be used for mock creation and behaviour verification.
    * Rationale: Consistency.
    * Enforcement: Manual.
---
#### Integration Testing
---
1. An integration test must only be used to check for correctness in cross boundary interactions between units. E.g if *File.WriteAll* is used in a method, unit tests will mock it out.
If it is necessary to verify that output is actually written to disk in the right format/location etc, then an integration test can be used. In this case the units are the method
that calls *File.WriteAll* and *File.WriteAll*. Each is tested individually but the results of their interactions need to be tested as well.
    * Rationale: Efficiency.
    * Enforcement: Manual.
---
#### End to End Testing
---
1. End to end tests must only be used to check for correctness in the end to end behaviour of an entire product or library. In otherwords, they must test scenarios that consumers of the 
product or library will encounter. E.g for a console application, end to end tests should involve entering console arguments and parsing console output or checking for changes to the file system
to ensure that the application works as expected.
    * Rationale: Efficiency.
    * Enforcement: Manual.
---
## Documentation
#### Targets
---
1. Public members must be documented. Documentation can be explicit or inherited.
    * Rationale: Ease of use.
    * Enforcement: CS1591.
---
2. Non-implemented and non-override members must have explicit documentation. Implementors and overriders must inherit their documentation.
    * Rationale: Ease of use and consistency; consumers interact with interfaces. Also, documentation on abstract types serve as a guide for implementors and overriders.
    * Enforcement: Manual (**can be automated**, also consider a code analysis tool that copies documentation and keeps it in sync since \<inheritdoc/> does not work 
without plugins).
---
#### Grammar and Punctuation
---
1. Contents of all tags must have proper punctuation. E.g sentences must end with full stops.
    * Rationale: Ease of use.
    * Enforcement: Manual.
---
2. Use plural subjects. E.g *Commands must implement ICommand*, not *A command must implements ICommand*.
    * Rationale: Consistency and concision.
    * Enforcement: Manual.
---
3. Always use the definite article *the* over the indefinite articles *a* or *an* when referring to the entity being documented or its conceptual parents. 
E.g *The application's entry method*, not *An application's entry method*.
    * Rationale: Grammatical correctness; consumers typically read summaries through intellisense, at that point the entity and its conceptual parents already exist.
    * Enforcement: Manual.
---
4. Non general statements must start with an article. E.g *The default command*, not *Default command*.
    * Rationale: Consistency.
    * Enforcement: Manual.
---
#### Summary Tag
---
1. Member documentation must include a summary in a *\<summary>* tag.
    * Rationale: Ease of use; intellisense displays the contents of the summary tag. 
    * Enforcement: SA1604, SA1606.
---
2. *\<summary>* tag contents must describe what the member does, not how the member does what it does. E.g *Parser.Parse: parses specified arguments into a ParseResult*, not 
*Parser.Parse: maps arguments to a model, verifies validity of model, creates ParseResult and finally returns ParseResult*.
    * Rationale: Ease of use and maintainability; consumers use abstractions to avoid having to deal with low level stuff. How a member does what it does is superfluous to consumers. Also,
describing what a member does in detail couples the documentation and the code, this makes maintenance a nightmare since documentation cannot indicate that it is out of sync. Moreover, 
a member's body already describes the how of what it does.
    * Enforcement: Manual.
---
#### Params Tag
---
1. Member documentation must include documentation for parameters in *\<param>* tags with name attributes corresponding to parameter identifiers.
    * Rationale: Ease of use; intellisense displays the contents of params tags when entering arguments.
    * Enforcement: SA1611 (**no code fix**), CS1573 (**does not work for interfaces**).
---
2. *\<param>* tag contents must describe the parameter: what it is, its expected state and what it does. They must describe not how it does what it does. E.g *The non-zero integer used as the multiplier*, 
not *Validated to not be 0 then multiplied with quantity x to produce return value y*.
    * Rationale: Ease of use and maintainability.
    * Enforcement: Manual.
---
#### Returns Tag
---
1. Member documentation must include documentation for the return value in a *\<returns>* tag (if there is a return value).
    * Rationale: Ease of use; intellisense does not display the contents of return tags, however, consumers can navigate to members to view the contents of return tags.
    * Enforcement: SA1615.
---
2. \<returns> tag contents must describe the return value, namely what it is. E.g *The default command*.
    * Rationale: Ease of use.
    * Enforcement: Manual.
---
3. If the return type is of type bool, the *\<returns>* tag content must be of the form *true if \<condition>; otherwise, false*.
    * Rationale: Consistency.
    * Enforcement: Manual (**can be automated**).
#### Exception Tag
---
1. Member documentation must include documentation for exceptions in *\<exception>* tags with cref attributes.
    * Rationale: Ease of use; intellisense displays the exceptions.
    * Enforcement: Manual (**can be automated**).
---
2. *\<exception>* tag contents must be of the form *Thrown if \<condition>*.
    * Rationale: Consistentcy.
    * Enforcement: Manual (**can be automated**).
---
#### See Tag
---
1. *\<see>* tags must be used when referring to instances of types or members. When a sentence can refer to an instance of a type or the entity that the type represents, use a
*\<see>* tag. E.g in a *CommandLineApplicationContext* class, use *The command line application's \<see cref="IParser">*, not *The \<see cref="CommandLineApplication>'s parser*:
there is no *CommandLineApplication* instance in a context class, thus the sentence must refer to the business domain entity, the *command line application*. Also, both 
*\<see cref="IParser">* and parser are valid, so the *\<see>* tag must be used.
    * Rationale: Using *\<see>* tags where possible helps with navigating generated docs.
    * Enforcement: Manual.
---
2. Append *s*, *'s* or *s'* to a *\<see>* tag to show pluralism, possession, and plural possession respectively. E.g *\<see cref="Command">s* not *\<see cref="Command"> instances*.
    * Rationale: Concision.
    * Enforcement: Manual.
---
#### Entity Specific Rules
---
1. Class and interface summaries must begin with *Represents*. 
    * Rationale: Consistency; classes and interfaces are code based representations of *things*.
    * Enforcement: Manual (**can be automated**).
---
2. Constructors must begin with *Initializes a new instance of the <see cref="\<class name>" class*.
    * Rationale: Consistency.
    * Enforcement: SA1642.
---
3. Property summaries must begin with *Gets or sets* or *Gets*.
    * Rationale: Makes it immediately obvious whether a property has a setter.
    * Enforcement: SA1623.
---
4. Properties of type bool must begin with *Gets[ or sets] a value indicating*.
    * Rationale: Consistency.
    * Enforcement: Manual (**can be automated**).
---
5. Property value descriptions must be included in summaries. The *\<value>* tag must not be used.
    * Rationale: Intellisense does not display the *\<value>* tag. Consumers need to know what a properties value represents in order to use it.
    * Enforcement: Manual (**can be automated**).
---
6. Method summaries must start with the same verb or verb phrase used for the method identifier.
    * Rationale: Consistency.
    * Enforcement: Manual (**can be automated**).
---
