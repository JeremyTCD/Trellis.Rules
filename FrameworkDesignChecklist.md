# Framework Design Checklist
## Naming
### Capitalization
- [ ] Local variable identifiers must be in camelCase
- [ ] Private instance variable identifiers must be in camelCase
- [ ] Non local variable or private instance variable identifiers must be in PascalCase
- [ ] For an acronym in a position that should begin with a capital character, if it has more 
than 2 characters, only its first character is capitalized. 
E.g *Html*. If it has 2 characters both must be capitalized, e.g *IO*.
- [ ] For an acronym in a position that should begin with a lowercase character, all its characters should be
in lowercase, e.g *htmlWriter*.
- [ ] Closed-form compound words should be capitalized in the same manner as single words. E.g 
*Lowercase*, not *LowerCase*.
### Grammar
Ease of understanding must be prioritized.
- [ ] Use intuitively understandable combinations of words for identifiers. E.g a type that maps
floats should be named *FloatMapper*, not *MapperFloat*.
- [ ] Favour completeness over brevity. E.g *IsDefault* instead of *Def*.
- [ ] Avoid Hungarian notation.
- [ ] Avoid uncommon acronyms.
- [ ] Avoid abbreviations. E.g *Point* instead of *Pt*
### Names for Specific Entities
#### Namespaces
- [ ] A namespace name must be of the form \<Company>.\<Technology>[.\<Feature>][.\<Subfeature>]. E.g
*JeremyTCD.DotNet.Utils.Console*.  
Note: *\<Company>* is required for uniqueness. 
#### Assemblies
- [ ] The name of an assembly should be the common prefix of all namespaces in the assembly. E.g an
assembly with namespaces *JeremyTCD.DotNet.Utils.Console* and *JeremyTCD.DotNet.Utils.Datastructures*
should be named *JeremyTCD.DotNet.Utils*.  
#### Classes, Interfaces and Structs
- [ ] Class, Interface and Struct identifiers must be nouns or noun phrases since they represent
distinct entities. E.g *Printer*, *PrinterFactory*, *IParser*, not *Print*, *Create* or *IParse*.
- [ ] Prepend Interfaces with *I*. E.g *IParser*.
- [ ] The identifier of the default implementation of an interface should differ from the interface's
identifier by *I*. E.g *IParser* and *Parser*.
- [ ] Consider appending identifiers of derived classes with identifiers of their base classes. E.g 
*OptionAttribute* for a class that extends *System.Attribute*
#### Enums
- [ ] Identifiers of non-flag enums should be singular. E.g *Size*.
- [ ] Identifiers of flag enums should be plural. E.g *Sizes*.
#### Type Members
##### Methods
- [ ] Method identifiers must be verbs or verb phrases. E.g *Add* or *CreatePrinter*.
##### Properties
- [ ] Property identifiers must be nouns, noun phrases or adjectives. E.g *Printer*, *StringBuilder* or
*IsDefault*.
- [ ] Avoid having public methods that correspond to a public property to prevent analysis paralysis. 
E.g if there is a public method *GetPrinter*, there should not be a public property *Printer*. 
- [ ] Collection property identifiers should be plural.
- [ ] Boolean property identifiers should be affirmative to avoid double negation. E.g *IsDefault*, 
not *IsNotDefault*.
- [ ] It is acceptable for a property identifier to be identical to the property's type's identifier.
##### Fields
- [ ] Private field identifies must be prepended with an _.
- [ ] Field identifiers must be nouns, noun phrases or adjectives. E.g *_printer*, *_stringBuilder* or
*_isDefault*.
##### Resources
- [ ] Since resouces are properties, all requirements for properties apply.
- [ ] Strings must have the format \<what its used for (noun)>_\<description>. E.g *OptionName_Help* or
*ArgumentException_IllegalCharacters*.