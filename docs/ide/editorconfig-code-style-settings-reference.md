---
title: ".NET coding convention settings For EditorConfig in Visual Studio | Microsoft Docs"
ms.date: 02/28/2018
ms.topic: "article"
dev_langs:
  - "CSharp"
  - "VB"
helpviewer_keywords:
  - "coding conventions [EditorConfig]"
  - "EditorConfig coding conventions"
  - "language conventions [EditorConfig]"
  - "formatting conventions [EditorConfig]"
author: "kuhlenh"
ms.author: "kaseyu"
manager: ghogen
ms.technology: vs-ide-general
ms.workload:
  - "dotnet"
  - "dotnetcore"
---
# .NET coding convention settings for EditorConfig

In Visual Studio 2017, you can define and maintain consistent code style in your codebase with the use of an [EditorConfig](../ide/create-portable-custom-editor-options.md) file. EditorConfig includes several core formatting properties, such as `indent_style` and `indent_size`. In Visual Studio, .NET coding conventions settings can also be configured using an EditorConfig file. EditorConfig files allow you to enable or disable individual .NET coding conventions, and to configure the degree to which you want the convention enforced via a severity level. To learn more about how to use EditorConfig to enforce consistency in your codebase, read [Create portable custom editor options](../ide/create-portable-custom-editor-options.md). You can also look at the [.NET Compiler Platform's .editorconfig file](https://github.com/dotnet/roslyn/blob/master/.editorconfig) as an example.

There are three supported .NET coding convention categories:

- [Language Conventions](#language-conventions)

   Rules pertaining to the C# or Visual Basic language. For example, you can specify rules around using `var` or explicit types when defining variables, or preferring expression-bodied members.

- [Formatting Conventions](#formatting-conventions)

   Rules regarding the layout and structure of your code in order to make it easier to read. For example, you can specify rules around Allman braces, or preferring spaces in control blocks.

- [Naming Conventions](../ide/editorconfig-naming-conventions.md)

   Rules regarding the naming of code elements. For example, you can specify that `async` methods must end in "Async".

## Language conventions

Rules for language conventions have the following format:

`options_name = false|true : none|suggestion|warning|error`

For each language convention rule, you must specify either **true** (prefer this style) or **false** (do not prefer this style), and a **severity**. The severity specifies the level of enforcement for that style.

The following table lists the possible severity values and their effects:

Severity | Effect
:------- | ------
none or silent | Do not show anything to the user when this rule is violated. Code generation features will generate code in this style, however.
suggestion | When this style rule is violated, show it to the user as a suggestion. Suggestions appear as three grey dots under the first two characters.
warning | When this style rule is violated, show a compiler warning.
error | When this style rule is violated, show a compiler error.

The following list shows the allowable language convention rules:

- .NET Code Style Settings
    - ["This." and "Me." qualifiers](#this_and_me)
        - dotnet\_style\_qualification\_for_field
        - dotnet\_style\_qualification\_for_property
        - dotnet\_style\_qualification\_for_method
        - dotnet\_style\_qualification\_for_event
    - [Language keywords instead of framework type names for type references](#language_keywords)
        - dotnet\_style\_predefined\_type\_for\_locals\_parameters_members
        - dotnet\_style\_predefined\_type\_for\_member_access
    - [Modifier preferences](#normalize_modifiers)
        - dotnet\_style\_require\_accessibility_modifiers
        - csharp\_preferred\_modifier_order
        - visual\_basic\_preferred\_modifier_order
    - [Expression-level preferences](#expression_level)
        - dotnet\_style\_object_initializer
        - dotnet\_style\_collection_initializer
        - dotnet\_style\_explicit\_tuple_names
        - dotnet\_style\_coalesce_expression
        - dotnet\_style\_null_propagation
        - dotnet\_prefer\_inferred\_tuple_names
        - dotnet\_prefer\_inferred\_anonymous\_type\_member_names
- C# Code Style Settings
    - [Implicit and explicit types](#var)
        - csharp\_style\_var\_for\_built\_in_types
        - csharp\_style\_var\_when\_type\_is_apparent
        - csharp\_style\_var_elsewhere
    - [Expression-bodied members](#expression_bodied_members)
        - csharp\_style\_expression\_bodied_methods
        - csharp\_style\_expression\_bodied_constructors
        - csharp\_style\_expression\_bodied_operators
        - csharp\_style\_expression\_bodied_properties
        - csharp\_style\_expression\_bodied_indexers
        - csharp\_style\_expression\_bodied_accessors
    - [Pattern matching](#pattern_matching)
        - csharp\_style\_pattern\_matching\_over\_is\_with\_cast_check
        - csharp\_style\_pattern\_matching\_over\_as\_with\_null_check
    - [Inlined variable declarations](#inlined_variable_declarations)
        - csharp\_style\_inlined\_variable_declaration
    - [Expression-level preferences](#expression_level_csharp)
        - csharp\_prefer\_simple\_default_expression
        - csharp\_style\_deconstructed\_variable_declaration
        - csharp\_style\_pattern\_local\_over\_anonymous_function
    - ["Null" checking preferences](#null_checking)
        - csharp\_style\_throw_expression
        - csharp\_style\_conditional\_delegate_call
    - [Code block preferences](#code_block)
        - csharp\_prefer_braces

### .NET code style settings

The style rules in this section are applicable to both C# and Visual Basic. To see code examples in your preferred programming language, choose it in the drop-down **Language** menu at the top-right corner of your browser window.

#### <a name="this_and_me">"This." and "Me." qualifiers</a>

This style rule (rule IDs IDE0003 and IDE0009) can be applied to fields, properties, methods or events. A value of **true** means prefer the code symbol to be prefaced with `this.` in C# or `Me.` in Visual Basic. A value of **false** means prefer the code element _not_ to be prefaced with `this.` or `Me.`.

The following table shows the rule names, applicable programming languages, and default values:

| Rule Name | Applicable languages | Visual Studio default value |
| ----------- | -------------------- | ----------------------|
| dotnet_style_qualification_for_field | C# and Visual Basic | false:none |
| dotnet_style_qualification_for_property | C# and Visual Basic | false:none |
| dotnet_style_qualification_for_method | C# and Visual Basic | false:none |
| dotnet_style_qualification_for_event | C# and Visual Basic | false:none |

**dotnet\_style\_qualification\_for_field**

- When this rule is set to **true**, prefer fields to be prefaced with `this.` in C# or `Me.` in Visual Basic.
- When this rule is set to **false**, prefer fields _not_ to be prefaced with `this.` or `Me.`.

Code examples:

```csharp
// dotnet_style_qualification_for_field = true
this.capacity = 0;

// dotnet_style_qualification_for_field = false
capacity = 0;
```

```vb
' dotnet_style_qualification_for_field = true
Me.capacity = 0

' dotnet_style_qualification_for_field = false
capacity = 0
```

**dotnet\_style\_qualification\_for_property**

- When this rule is set to **true**, prefer properties to be prefaced with `this.` in C# or `Me.` in Visual Basic.
- When this rule is set to **false**, prefer properties _not_ to be prefaced with `this.` or `Me.`.

Code examples:

```csharp
// dotnet_style_qualification_for_property = true
this.ID = 0;

// dotnet_style_qualification_for_property = false
ID = 0;
```

```vb
' dotnet_style_qualification_for_property = true
Me.ID = 0

' dotnet_style_qualification_for_property = false
ID = 0
```

**dotnet\_style\_qualification\_for_method**

- When this rule is set to **true**, prefer methods to be prefaced with `this.` in C# or `Me.` in Visual Basic.
- When this rule is set to **false**, prefer methods _not_ to be prefaced with `this.` or `Me.`.

Code examples:

```csharp
// dotnet_style_qualification_for_method = true
this.Display();

// dotnet_style_qualification_for_method = false
Display();
```

```vb
' dotnet_style_qualification_for_method = true
Me.Display()

' dotnet_style_qualification_for_method = false
Display()
```

**dotnet\_style\_qualification\_for_event**

- When this rule is set to **true**, prefer events to be prefaced with `this.` in C# or `Me.` in Visual Basic.
- When this rule is set to **false**, prefer events _not_ to be prefaced with `this.` or `Me.`.

Code examples:

```csharp
// dotnet_style_qualification_for_event = true
this.Elapsed += Handler;

// dotnet_style_qualification_for_event = false
Elapsed += Handler;
```

```vb
' dotnet_style_qualification_for_event = true
AddHandler Me.Elapsed, AddressOf Handler

' dotnet_style_qualification_for_event = false
AddHandler Elapsed, AddressOf Handler
```

These rules could appear in an .editorconfig file as follows:

```EditorConfig
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_qualification_for_field = false:suggestion
dotnet_style_qualification_for_property = false:suggestion
dotnet_style_qualification_for_method = false:suggestion
dotnet_style_qualification_for_event = false:suggestion
```

#### <a name="language_keywords">Language keywords instead of framework type names for type references</a>

This style rule can be applied to local variables, method parameters, and class members, or as a separate rule to type member access expressions. A value of **true** means prefer the language keyword (e.g. `int` or `Integer`) instead of the type name (e.g. `Int32`) for types that have a keyword to represent them. A value of **false** means prefer the type name instead of the language keyword.

The following table shows the rule names, rules IDs, applicable programming languages, and default values:

| Rule Name | Rule ID | Applicable Languages | Visual Studio Default |
| --------- | ------- | -------------------- | ----------------------|
| dotnet_style_predefined_type_for_locals_parameters_members | IDE0012 and IDE0014 | C# and Visual Basic | true:none |
| dotnet_style_predefined_type_for_member_access | IDE0013 and IDE0015 | C# and Visual Basic | true:none |

**dotnet\_style\_predefined\_type\_for\_locals\_parameters_members**

- When this rule is set to **true**, prefer the language keyword for local variables, method parameters, and class members, instead of the type name, for types that have a keyword to represent them.
- When this rule is set to **false**, prefer the type name for local variables, method parameters, and class members, instead of the language keyword.

Code examples:

```csharp
// dotnet_style_predefined_type_for_locals_parameters_members = true
private int _member;

// dotnet_style_predefined_type_for_locals_parameters_members = false
private Int32 _member;
```

```vb
' dotnet_style_predefined_type_for_locals_parameters_members = true
Private _member As Integer

' dotnet_style_predefined_type_for_locals_parameters_members = false
Private _member As Int32
```

**dotnet\_style\_predefined\_type\_for\_member_access**

- When this rule is set to **true**, prefer the language keyword for member access expressions, instead of the type name, for types that have a keyword to represent them.
- When this rule is set to **false**, prefer the type name for member access expressions, instead of the language keyword.

Code examples:

```csharp
// dotnet_style_predefined_type_for_member_access = true
var local = int.MaxValue;

// dotnet_style_predefined_type_for_member_access = false
var local = Int32.MaxValue;
```

```vb
' dotnet_style_predefined_type_for_member_access = true
Dim local = Integer.MaxValue

' dotnet_style_predefined_type_for_member_access = false
Dim local = Int32.MaxValue
```

These rules could appear in an .editorconfig file as follows:

```EditorConfig
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_predefined_type_for_locals_parameters_members = true:suggestion
dotnet_style_predefined_type_for_member_access = true:suggestion
```

#### <a name="normalize_modifiers">Modifier preferences</a>

The style rules in this section concern modifier preferences, including requiring accessibility modifiers and specifying the desired modifier sort order.

The following table shows the rule names, rule IDs, applicable programming languages, default values, and first supported version of Visual Studio:

| Rule Name | Rule ID | Applicable Languages | Visual Studio Default | Visual Studio 2017 Version |
| --------- | ------- | -------------------- | ----------------------| ----------------  |
| dotnet_style_require_accessibility_modifiers | IDE0040 | C# and Visual Basic | for_non_interface_members:none | 15.5 |
| csharp_preferred_modifier_order | IDE0036 | C# | public, private, protected, internal, static, extern, new, virtual, abstract, sealed, override, readonly, unsafe, volatile, async:none | 15.5 |
| visual_basic_preferred_modifier_order | IDE0036 | Visual Basic | Partial, Default, Private, Protected, Public, Friend, NotOverridable, Overridable, MustOverride, Overloads, Overrides, MustInherit, NotInheritable, Static, Shared, Shadows, ReadOnly, WriteOnly, Dim, Const,WithEvents, Widening, Narrowing, Custom, Async:none | 15.5 |

**dotnet\_style\_require\_accessibility_modifiers**

This rule does not accept a **true** or **false** value; instead it accepts a value from the following table:

| Value | Description |
| ----- |:----------- |
| always | Prefer accessibility modifiers to be specified |
| for\_non\_interface_members | Prefer accessibility modifiers to be declared except for public interface members. This will currently not differ from **always** and will act as future proofing for if C# adds default interface methods. |
| never | Do not prefer accessibility modifiers to be specified |

Code examples:

```csharp
// dotnet_style_require_accessibility_modifiers = always
// dotnet_style_require_accessibility_modifiers = for_non_interface_members
class MyClass
{
    private const string thisFieldIsConst= "constant";
}

// dotnet_style_require_accessibility_modifiers = never
class MyClass
{
    const string thisFieldIsConst= "constant";
}
```

**csharp_preferred_modifier_order**

- When this rule is set to a list of modifiers, prefer the specified ordering.
- When this rule is omitted from the file, do not prefer a modifier order.

Code examples:

```csharp
// csharp_preferred_modifier_order = public,private,protected,internal,static,extern,new,virtual,abstract,sealed,override,readonly,unsafe,volatile,async
class MyClass
{
    private static readonly int _daysInYear = 365;
}
```

**visual_basic_preferred_modifier_order**

- When this rule is set to a list of modifiers, prefer the specified ordering.
- When this rule is omitted from the file, do not prefer a modifier order.

Code examples:

```vb
' visual_basic_preferred_modifier_order = Partial,Default,Private,Protected,Public,Friend,NotOverridable,Overridable,MustOverride,Overloads,Overrides,MustInherit,NotInheritable,Static,Shared,Shadows,ReadOnly,WriteOnly,Dim,Const,WithEvents,Widening,Narrowing,Custom,Async
Public Class MyClass
    Private Shared ReadOnly daysInYear As Int = 365
End Class
```

These rules could appear in an .editorconfig file as follows:

```EditorConfig
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_require_accessibility_modifiers = always:suggestion

# CSharp code style settings:
[*.cs]
csharp_preferred_modifier_order = public,private,protected,internal,static,extern,new,virtual,abstract,sealed,override,readonly,unsafe,volatile,async:suggestion

# Visual Basic code style settings:
[*.vb]
visual_basic_preferred_modifier_order = Partial,Default,Private,Protected,Public,Friend,NotOverridable,Overridable,MustOverride,Overloads,Overrides,MustInherit,NotInheritable,Static,Shared,Shadows,ReadOnly,WriteOnly,Dim,Const,WithEvents,Widening,Narrowing,Custom,Async:suggestion
```

#### <a name="expression_level">Expression-level preferences</a>

The style rules in this section concern expression-level preferences, including the use of object initializers, collection initializers, explicit tuple names, null coalescing expressions versus ternary operators, and the null-conditional operator.

The following table shows the rule names, rule IDs, applicable programming languages, default values, and first supported version of Visual Studio:

| Rule Name | Rule ID | Applicable Languages | Visual Studio Default | Visual Studio 2017 Version |
| --------- | ------- | -------------------- | ----------------------| ---- |
| dotnet_style_object_initializer | IDE0017 | C# and Visual Basic | true:suggestion | First release |
| dotnet_style_collection_initializer | IDE0028 | C# and Visual Basic | true:suggestion | First release |
| dotnet_style_explicit_tuple_names | IDE0033 | C# 7.0+ and Visual Basic 15+ | true:suggestion | First release |
| dotnet_style_coalesce_expression | IDE0029 | C# and Visual Basic | true:suggestion | First release |
| dotnet_style_null_propagation | IDE0031 | C# 6.0+ and Visual Basic 14+ | true:suggestion | First release |
| dotnet_prefer_inferred_tuple_names | IDE0037 | C# 7.1+ and Visual Basic 15+ | true:suggestion | 15.6 |
| dotnet_prefer_inferred_anonymous_type_member_names | IDE0037 | C# and Visual Basic | true:suggestion | 15.6 |

**dotnet\_style\_object_initializer**

- When this rule is set to **true**, prefer objects to be initialized using object initializers when possible.
- When this rule is set to **false**, prefer objects to *not* be initialized using object initializers.

Code examples:

```csharp
// dotnet_style_object_initializer = true
var c = new Customer() { Age = 21 };

// dotnet_style_object_initializer = false
var c = new Customer();
c.Age = 21;
```

```vb
' dotnet_style_object_initializer = true
Dim c = New Customer() With {.Age = 21}

' dotnet_style_object_initializer = false
Dim c = New Customer()
c.Age = 21
```

**dotnet\_style\_collection_initializer**

- When this rule is set to **true**, prefer collections to be initialized using collection initializers when possible.
- When this rule is set to **false**, prefer collections to *not* be initialized using collection initializers.

Code examples:

```csharp
// dotnet_style_collection_initializer = true
var list = new List<int> { 1, 2, 3 };

// dotnet_style_collection_initializer = false
var list = new List<int>();
list.Add(1);
list.Add(2);
list.Add(3);
```

```vb
' dotnet_style_collection_initializer = true
Dim list = New List(Of Integer) From {1, 2, 3}

' dotnet_style_collection_initializer = false
Dim list = New List(Of Integer)
list.Add(1)
list.Add(2)
list.Add(3)
```

**dotnet\_style\_explicit\_tuple_names**

- When this rule is set to **true**, prefer tuple names to ItemX properties.
- When this rule is set to **false**, prefer ItemX properties to tuple names.

Code examples:

```csharp
// dotnet_style_explicit_tuple_names = true
(string name, int age) customer = GetCustomer();
var name = customer.name;

// dotnet_style_explicit_tuple_names = false
(string name, int age) customer = GetCustomer();
var name = customer.Item1;
```

```vb
 ' dotnet_style_explicit_tuple_names = true
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.name

' dotnet_style_explicit_tuple_names = false
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.Item1
```

**dotnet\_style\_coalesce_expression**

- When this rule is set to **true**, prefer null coalescing expressions to ternary operator checking.
- When this rule is set to **false**, prefer ternary operator checking to null coalescing expressions.

Code examples:

```csharp
// dotnet_style_coalesce_expression = true
var v = x ?? y;

// dotnet_style_coalesce_expression = false
var v = x != null ? x : y; // or
var v = x == null ? y : x;
```

```vb
' dotnet_style_coalesce_expression = true
Dim v = If(x, y)

' dotnet_style_coalesce_expression = false
Dim v = If(x Is Nothing, y, x) ' or
Dim v = If(x IsNot Nothing, x, y)
```

**dotnet\_style\_null_propagation**

- When this rule is set to **true**, prefer to use null-conditional operator when possible.
- When this rule is set to **false**, prefer to use ternary null checking where possible.

Code examples:

```csharp
// dotnet_style_null_propagation = true
var v = o?.ToString();

// dotnet_style_null_propagation = false
var v = o == null ? null : o.ToString(); // or
var v = o != null ? o.String() : null;
```

```vb
' dotnet_style_null_propagation = true
Dim v = o?.ToString()

' dotnet_style_null_propagation = false
Dim v = If(o Is Nothing, Nothing, o.ToString()) ' or
Dim v = If(o IsNot Nothing, o.ToString(), Nothing)
```

**dotnet\_prefer\_inferred\_tuple_names**

- When this rule is set to **true**, prefer inferred tuple element names.
- When this rule is set to **false**, prefer explicit tuple element names.

Code examples:

```csharp
// dotnet_style_prefer_inferred_tuple_names = true
var tuple = (age, name);

// dotnet_style_prefer_inferred_tuple_names = false
var tuple = (age: age, name: name);
```

**dotnet\_style\_prefer\_inferred\_anonymous\_type\_member_names**

- When this rule is set to **true**, prefer inferred anonymous type member names.
- When this rule is set to **false**, prefer explicit anonymous type member names.

Code examples:

```csharp
// dotnet_style_prefer_inferred_anonymous_type_member_names = true
var anon = new { age, name };

// dotnet_style_prefer_inferred_anonymous_type_member_names = false
var anon = new { age = age, name = name };

```

These rules could appear in an .editorconfig file as follows:

```EditorConfig
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_object_initializer = true:suggestion
dotnet_style_collection_initializer = true:suggestion
dotnet_style_explicit_tuple_names = true:suggestion
dotnet_style_coalesce_expression = true:suggestion
dotnet_style_null_propagation = true:suggestion
dotnet_style_prefer_inferred_tuple_names = true:suggestion
dotnet_style_prefer_inferred_anonymous_type_member_names = true:suggestion
```

### C# code style settings

The style rules in this section are applicable to C# only.

#### <a name="var">Implicit and explicit types</a>

The style rules in this section (rule IDs IDE0007 and IDE0008) concern the use of the [var](/dotnet/csharp/language-reference/keywords/var) keyword versus an explicit type in a variable declaration. This rule can be applied separately to built-in types, when the type is apparent, and elsewhere.

The following table shows the rule names, applicable programming languages, and default values:

| Rule Name | Applicable Languages | Visual Studio Default |
| ----------- | -------------------- | ----------------------|
| csharp_style_var_for_built_in_types | C# | true:none |
| csharp_style_var_when_type_is_apparent | C# | true:none |
| csharp_style_var_elsewhere | C# | true:none |

**csharp\_style\_var\_for\_built\_in_types**

- When this rule is set to **true**, prefer `var` is used to declare variables with built-in system types such as `int`.
- When this rule is set to **false**, prefer explicit type over `var` to declare variables with built-in system types such as `int`.

Code examples:

```csharp
// csharp_style_var_for_built_in_types = true
var x = 5;

// csharp_style_var_for_built_in_types = false
int x = 5;
```

**csharp\_style\_var\_when\_type\_is_apparent**

- When this rule is set to **true**, prefer `var` when the type is already mentioned on the right-hand side of a declaration expression.
- When this rule is set to **false**, prefer explicit type over `var` when the type is already mentioned on the right-hand side of a declaration expression.

Code examples:

```csharp
// csharp_style_var_when_type_is_apparent = true
var obj = new Customer();

// csharp_style_var_when_type_is_apparent = false
Customer obj = new Customer();
```

**csharp\_style\_var_elsewhere**

- When this rule is set to **true**, prefer `var` over explicit type in all cases, unless overridden by another code style rule.
- When this rule is set to **false**, prefer explicit type over `var` in all cases, unless overridden by another code style rule.

Code examples:

```csharp
// csharp_style_var_elsewhere = true
var f = this.Init();

// csharp_style_var_elsewhere = false
bool f = this.Init();
```

Example .editorconfig file:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_style_var_for_built_in_types = true:suggestion
csharp_style_var_when_type_is_apparent = true:suggestion
csharp_style_var_elsewhere = true:suggestion
```

#### <a name="expression_bodied_members">Expression-bodied members</a>

The style rules in this section concern the use of [expression-bodied members](/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members) when the logic consists of a single expression. This rule can be applied to methods, constructors, operators, properties, indexers, and accessors.

The following table shows the rule names, rule IDs, applicable language versions, default values, and first supported version of Visual Studio:

| Rule Name | Rule ID | Applicable Languages | Visual Studio Default | Visual Studio 2017 Version |
| --------- | ------- | -------------------- | ----------------------| ----------------  |
| csharp_style_expression_bodied_methods | IDE0022 | C# 6.0+ | false:none | 15.3 |
| csharp_style_expression_bodied_constructors | IDE0021 | C# 7.0+ | false:none | 15.3 |
| csharp_style_expression_bodied_operators | IDE0023 and IDE0024 | C# 7.0+ | false:none | 15.3 |
| csharp_style_expression_bodied_properties | IDE0025 | C# 7.0+ | true:none | 15.3 |
| csharp_style_expression_bodied_indexers | IDE0026 | C# 7.0+ | true:none | 15.3 |
| csharp_style_expression_bodied_accessors | IDE0027 | C# 7.0+ | true:none | 15.3 |

**csharp\_style\_expression\_bodied_methods**

This rule accepts values from the following table:

| Value | Description |
| ----- |:----------- |
| true | Prefer expression-bodied members for methods |
| when_on_single_line | Prefer expression-bodied members for methods when they will be a single line |
| false | Prefer block bodies for methods |

Code examples:

```csharp
// csharp_style_expression_bodied_methods = true
public int GetAge() => this.Age;

// csharp_style_expression_bodied_methods = false
public int GetAge() { return this.Age; }
```

**csharp\_style\_expression\_bodied_constructors**

This rule accepts values from the following table:

| Value | Description |
| ----- |:----------- |
| true | Prefer expression-bodied members for constructors |
| when_on_single_line | Prefer expression-bodied members for constructors when they will be a single line |
| false | Prefer block bodies for constructors |

Code examples:

```csharp
// csharp_style_expression_bodied_constructors = true
public Customer(int age) => Age = age;

// csharp_style_expression_bodied_constructors = false
public Customer(int age) { Age = age; }
```

**csharp\_style\_expression\_bodied_operators**

This rule accepts values from the following table:

| Value | Description |
| ----- |:----------- |
| true | Prefer expression-bodied members for operators |
| when_on_single_line | Prefer expression-bodied members for operators when they will be a single line |
| false | Prefer block bodies for operators |

Code examples:

```csharp
// csharp_style_expression_bodied_operators = true
public static ComplexNumber operator + (ComplexNumber c1, ComplexNumber c2)
    => new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary);

// csharp_style_expression_bodied_operators = false
public static ComplexNumber operator + (ComplexNumber c1, ComplexNumber c2)
{ return new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary); }
```

**csharp\_style\_expression\_bodied_properties**

This rule accepts values from the following table:

| Value | Description |
| ----- |:----------- |
| true | Prefer expression-bodied members for properties |
| when_on_single_line | Prefer expression-bodied members for properties when they will be a single line |
| false | Prefer block bodies for properties |

Code examples:

```csharp
// csharp_style_expression_bodied_properties = true
public int Age => _age;

// csharp_style_expression_bodied_properties = false
public int Age { get { return _age; }}
```

**csharp\_style\_expression\_bodied_indexers**

This rule accepts values from the following table:

| Value | Description |
| ----- |:----------- |
| true | Prefer expression-bodied members for indexers |
| when_on_single_line | Prefer expression-bodied members for indexers when they will be a single line |
| false | Prefer block bodies for indexers |

Code examples:

```csharp
// csharp_style_expression_bodied_indexers = true
public T this[int i] => _value[i];

// csharp_style_expression_bodied_indexers = false
public T this[int i] { get { return _values[i]; } }
```

**csharp\_style\_expression\_bodied_accessors**

This rule accepts values from the following table:

| Value | Description |
| ----- |:----------- |
| true | Prefer expression-bodied members for accessors |
| when_on_single_line | Prefer expression-bodied members for accessors when they will be a single line |
| false | Prefer block bodies for accessors |

Code examples:

```csharp
// csharp_style_expression_bodied_accessors = true
public int Age { get => _age; set => _age = value; }

// csharp_style_expression_bodied_accessors = false
public int Age { get { return _age; } set { _age = value; } }
```

Example .editorconfig file:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_style_expression_bodied_methods = false:none
csharp_style_expression_bodied_constructors = false:none
csharp_style_expression_bodied_operators = false:none
csharp_style_expression_bodied_properties = true:suggestion
csharp_style_expression_bodied_indexers = true:suggestion
csharp_style_expression_bodied_accessors = true:suggestion
```

#### <a name="pattern_matching">Pattern matching</a>

The style rules in this section concern the use of [pattern matching](/dotnet/csharp/pattern-matching) in C#.

The following table shows the rule names, rule IDs, applicable language versions, and default values:

| Rule Name | Rule ID | Applicable Languages | Visual Studio Default |
| --------- | ------- | -------------------- | ----------------------|
| csharp_style_pattern_matching_over_is_with_cast_check | IDE0020 | C# 7.0+ | true:suggestion |
| csharp_style_pattern_matching_over_as_with_null_check | IDE0019 | C# 7.0+ | true:suggestion |

**csharp\_style\_pattern\_matching\_over\_is\_with\_cast_check**

- When this rule is set to **true**, prefer pattern matching instead of `is` expressions with type casts.
- When this rule is set to **false**, prefer `is` expressions with type casts instead of pattern matching.

Code examples:

```csharp
// csharp_style_pattern_matching_over_is_with_cast_check = true
if (o is int i) {...}

// csharp_style_pattern_matching_over_is_with_cast_check = false
if (o is int) {var i = (int)o; ... }
```

**csharp\_style\_pattern\_matching\_over\_as\_with\_null_check**

- When this rule is set to **true**, prefer pattern matching instead of `as` expressions with null checks to determine if something is of a particular type.
- When this rule is set to **false**, prefer `as` expressions with null checks instead of pattern matching to determine if something is of a particular type.

Code examples:

```csharp
// csharp_style_pattern_matching_over_as_with_null_check = true
if (o is string s) {...}

// csharp_style_pattern_matching_over_as_with_null_check = false
var s = o as string;
if (s != null) {...}
```

Example .editorconfig file:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_style_pattern_matching_over_is_with_cast_check = true:suggestion
csharp_style_pattern_matching_over_as_with_null_check = true:suggestion
```

#### <a name="inlined_variable_declarations">Inlined variable declarations</a>

This style rule concerns whether `out` variables are declared inline or not. Starting in C# 7, you can [declare an out variable in the argument list of a method call](/dotnet/csharp/language-reference/keywords/out-parameter-modifier#calling-a-method-with-an-out-argument), rather than in a separate variable declaration.

The following table shows the rule name, rule ID, applicable language versions, and default values:

| Rule Name | Rule ID | Applicable Languages | Visual Studio Default |
| --------- | -------- | -------------------- | ----------------------|
| csharp_style_inlined_variable_declaration | IDE0018 | C# 7.0+ | true:suggestion |

**csharp\_style\_inlined\_variable_declaration**

- When this rule is set to **true**, prefer `out` variables to be declared inline in the argument list of a method call when possible.
- When this rule is set to **false**, prefer `out` variables to be declared before the method call.

Code examples:

```csharp
// csharp_style_inlined_variable_declaration = true
if (int.TryParse(value, out int i) {...}

// csharp_style_inlined_variable_declaration = false
int i;
if (int.TryParse(value, out i) {...}
```

Example .editorconfig file:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_style_inlined_variable_declaration = true:suggestion
```

#### <a name="expression_level_csharp">Expression-level preferences</a>

The style rules in this section concern expression-level preferences, including the use of [default expressions](/dotnet/csharp/programming-guide/statements-expressions-operators/default-value-expressions#default-literal-and-type-inference), deconstructed variables, and local functions over anonymous functions.

The following table shows the rule name, rule ID, applicable language versions, default values, and first supported version of Visual Studio:

| Rule Name | Rule ID | Applicable Languages | Visual Studio Default | Visual Studio 2017 Version |
| --------- | ------- | -------------------- | ----------------------| ----------------  |
| csharp_prefer_simple_default_expression | IDE0034 | C# 7.1+ | true:suggestion | 15.3 |
| csharp_style_deconstructed_variable_declaration | IDE0042 | C# 7.0+ | true:suggestion | 15.5 |
| csharp_style_pattern_local_over_anonymous_function | IDE0039 | C# 7.0+ | true:suggestion | 15.5 |

**csharp\_prefer\_simple\_default_expression**

This style rule concerns using the [`default` literal for default value expressions](/dotnet/csharp/programming-guide/statements-expressions-operators/default-value-expressions#default-literal-and-type-inference) when the compiler can infer the type of the expression.

- When this rule is set to **true**, prefer `default` over `default(T)`.
- When this rule is set to **false**, prefer `default(T)` over `default`.

Code examples:

```csharp
// csharp_prefer_simple_default_expression = true
void DoWork(CancellationToken cancellationToken = default) { ... }

// csharp_prefer_simple_default_expression = false
void DoWork(CancellationToken cancellationToken = default(CancellationToken)) { ... }
```

**csharp\_style\_deconstructed\_variable_declaration**

- When this rule is set to **true**, prefer deconstructed variable declaration.
- When this rule is set to **false**, do not prefer deconstruction in variable declarations.

Code examples:

```csharp
// csharp_style_deconstructed_variable_declaration = true
var (name, age) = GetPersonTuple();
Console.WriteLine($"{name} {age}");

(int x, int y) = GetPointTuple();
Console.WriteLine($"{x} {y}");

// csharp_style_deconstructed_variable_declaration = false
var person = GetPersonTuple();
Console.WriteLine($"{person.name} {person.age}");

(int x, int y) point = GetPointTuple();
Console.WriteLine($"{point.x} {point.y}");
```

**csharp\_style\_pattern\_local\_over\_anonymous_function**

- When this rule is set to **true**, prefer local functions over anonymous functions.
- When this rule is set to **false**, prefer anonymous functions over local functions.

Code examples:

```csharp
// csharp_style_pattern_local_over_anonymous_function = true
int fibonacci(int n)
{
    return n <= 1 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}

// csharp_style_pattern_local_over_anonymous_function = false
Func<int, int> fibonacci = null;
fibonacci = (int n) =>
{
    return n <= 1 ? 1 : fibonacci(n - 1) + fibonacci(n - 2);
};
```

Example .editorconfig file:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_prefer_simple_default_expression = true:suggestion
csharp_style_deconstructed_variable_declaration = true:suggestion
csharp_style_pattern_local_over_anonymous_function = true:suggestion
```

#### <a name="null_checking">"Null" checking preferences</a>

These style rules concern the syntax around `null` checking, including using `throw` expressions or `throw` statements, and whether to perform a null check or use the conditional coalescing operator (`?.`) when invoking a [lambda expression](/dotnet/csharp/lambda-expressions).

The following table shows the rule names, rule IDs, applicable language versions, and default values:

| Rule Name | Rule ID | Applicable Languages | Visual Studio Default |
| --------- | ------- | -------------------- | ----------------------|
| csharp_style_throw_expression | IDE0016 | C# 7.0+ | true:suggestion |
| csharp_style_conditional_delegate_call | IDE0041 | C# 6.0+ | true:suggestion |

**csharp\_style\_throw_expression**

- When this rule is set to **true**, prefer to use `throw` expressions instead of `throw` statements.
- When this rule is set to **false**, prefer to use `throw` statements instead of `throw` expressions.

Code examples:

```csharp
// csharp_style_throw_expression = true
this.s = s ?? throw new ArgumentNullException(nameof(s));

// csharp_style_throw_expression = false
if (s == null) { throw new ArgumentNullException(nameof(s)); }
this.s = s;
```

**csharp\_style\_conditional\_delegate_call**

- When this rule is set to **true**, prefer to use the conditional coalescing operator (`?.`) when invoking a lambda expression, instead of performing a null check.
- When this rule is set to **false**, prefer to perform a null check before invoking a lambda expression, instead of using the conditional coalescing operator (`?.`).

Code examples:

```csharp
// csharp_style_conditional_delegate_call = true
func?.Invoke(args);

// csharp_style_conditional_delegate_call = false
if (func != null) { func(args); }
```

Example .editorconfig file:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_style_throw_expression = true:suggestion
csharp_style_conditional_delegate_call = false:suggestion
```

#### <a name="code_block">Code block preferences</a>

This style rule concerns the use of curly braces `{ }` to surround code blocks.

The following table shows the rule name, rule ID, applicable language versions, default values, and first supported version of Visual Studio:

| Rule Name | Rule ID | Applicable Languages | Visual Studio Default | Visual Studio 2017 Version |
| --------- | ------- | -------------------- | ----------------------| ----------------  |
| csharp_prefer_braces | IDE0011 | C# | true:none | 15.3 |

**csharp\_prefer\_braces**

- When this rule is set to **true**, prefer curly braces even for one line of code.
- When this rule is set to **false**, prefer no curly braces if allowed.

Code examples:

```csharp
// csharp_prefer_braces = true
if (test) { this.Display(); }

// csharp_prefer_braces = false
if (test) this.Display();
```

Example .editorconfig file:

```EditorConfig
# CSharp code style settings:
[*.cs]
csharp_prefer_braces = true:none
```

## Formatting conventions

Most of the rules for formatting conventions have the following format:

`rule_name = false|true`

You specify either **true** (prefer this style) or **false** (do not prefer this style). You do not specify a severity. For a few rules, instead of true or false, you specify other values to describe when and where to apply the rule.

The following list shows the formatting convention rules available in Visual Studio:

- .NET Formatting Settings
    - [Organize Usings](#usings)
        - dotnet_sort_system_directives_first
- C# Formatting Settings
    - [Newline Options](#newline)
        - csharp_new_line_before_open_brace
        - csharp_new_line_before_else
        - csharp_new_line_before_catch
        - csharp_new_line_before_finally
        - csharp_new_line_before_members_in_object_initializers
        - csharp_new_line_before_members_in_anonymous_types
        - csharp_new_line_between_query_expression_clauses
    - [Indentation Options](#indent)
        - csharp_indent_case_contents
        - csharp_indent_switch_labels
        - csharp_indent_labels
    - [Spacing Options](#spacing)
        - csharp_space_after_cast
        - csharp_space_after_keywords_in_control_flow_statements
        - csharp_space_between_method_declaration_parameter_list_parentheses
        - csharp_space_between_method_call_parameter_list_parentheses
        - csharp_space_between_parentheses
    - [Wrapping Options](#wrapping)
        - csharp_preserve_single_line_statements
        - csharp_preserve_single_line_blocks

### .NET formatting settings

The formatting rules in this section are applicable to C# and Visual Basic.

#### <a name="usings">Organize usings</a>

This formatting rule concerns the placement of System.* using directives with respect to other using directives.

The following table shows the rule name, applicable languages, default value, and first supported version of Visual Studio:

| Rule Name | Applicable Languages | Visual Studio Default | Visual Studio 2017 Version |
| ----------- | -------------------- | ----------------------| ----------------  |
| dotnet_sort_system_directives_first |  C# and Visual Basic | true | 15.3  |

**dotnet\_sort\_system\_directives_first**

- When this rule is set to **true**, sort System.* using directives alphabetically, and place them before other usings.
- When this rule is set to **false**, do not place System.* using directives before other using directives.

Code examples:

```csharp
// dotnet_sort_system_directives_first = true
using System.Collections.Generic;
using System.Threading.Tasks;
using Octokit;

// dotnet_sort_system_directives_first = false
using System.Collections.Generic;
using Octokit;
using System.Threading.Tasks;
```

Example .editorconfig file:

```EditorConfig
# .NET formatting settings:
[*.{cs,vb}]
dotnet_sort_system_directives_first = true
```

### C# formatting settings

The formatting rules in this section apply only to C# code.

#### <a name="newline">Newline Options</a>

These formatting rules concern the use of new lines to format code.

The following table shows the "new line" rule names, applicable languages, default values, and first supported version of Visual Studio:

| Rule Name | Applicable Languages | Visual Studio Default | Visual Studio 2017 Version |
| ----------- | -------------------- | ----------------------| ----------------  |
| csharp_new_line_before_open_brace |  C# | all | 15.3  |
| csharp_new_line_before_else |  C# | true | 15.3  |
| csharp_new_line_before_catch |  C# | true | 15.3  |
| csharp_new_line_before_finally |  C# | true | 15.3  |
| csharp_new_line_before_members_in_object_initializers |  C# | true | 15.3  |
| csharp_new_line_before_members_in_anonymous_types |  C# | true | 15.3  |
| csharp_new_line_between_query_expression_clauses |  C# | true | 15.3  |

**csharp\_new\_line\_before\_open_brace**

This rule concerns whether an open brace `{` should be placed on the same line as the preceding code, or on a new line. For this rule, you do not specify **true** or **false**. Instead you specify **all**, **none**, or one or more code elements such as **methods** or **properties**, to define when this rule should be applied. The complete list of allowable values is shown in the following table:

| Value | Description
| ------------- |:-------------|
| accessors, anonymous_methods, anonymous_types, control_blocks, events, indexers, lambdas, local_functions, methods, object_collection, properties, types.<br>(For multiple kinds, separate with ','). | Require braces to be on a new line for the specified code elements (also known as "Allman" style) |
| all | Require braces to be on a new line for all expressions ("Allman" style) |
| none | Require braces to be on the same line for all expressions ("K&R") |

Code examples:

```csharp
// csharp_new_line_before_open_brace = all
void MyMethod()
{
    if (...)
    {
        ...
    }
}

// csharp_new_line_before_open_brace = none
void MyMethod() {
    if (...) {
        ...
    }
}
```

**csharp\_new\_line\_before_else**

- When this rule is set to **true**, place `else` statements on a new line.
- When this rule is set to **false**, place `else` statements on the same line.

Code examples:

```csharp
// csharp_new_line_before_else = true
if (...) {
    ...
}
else {
    ...
}

// csharp_new_line_before_else = false
if (...) {
    ...
} else {
    ...
}
```

**csharp\_new\_line\_before_catch**

- When this rule is set to **true**, place `catch` statements on a new line.
- When this rule is set to **false**, place `catch` statements on the same line.

Code examples:

```csharp
// csharp_new_line_before_catch = true
try {
    ...
}
catch (Exception e) {
    ...
}

// csharp_new_line_before_catch = false
try {
    ...
} catch (Exception e) {
    ...
}
```

**csharp\_new\_line\_before_finally**

- When this rule is set to **true**, require `finally` statements to be on a new line after the closing brace.
- When this rule is set to **false**, require `finally` statements to be on the same line as the closing brace.

Code examples:

```csharp
// csharp_new_line_before_finally = true
try {
    ...
}
catch (Exception e) {
    ...
}
finally {
    ...
}

// csharp_new_line_before_finally = false
try {
    ...
} catch (Exception e) {
    ...
} finally {
    ...
}
```

**csharp\_new\_line\_before\_members\_in\_object_initializers**

- When this rule is set to **true**, require members of object intiializers to be on separate lines.
- When this rule is set to **false**, require members of object initializers to be on the same line.

Code examples:

```csharp
// csharp_new_line_before_members_in_object_initializers = true
var z = new B()
{
    A = 3,
    B = 4
}

// csharp_new_line_before_members_in_object_initializers = false
var z = new B()
{
    A = 3, B = 4
}
```

**csharp\_new\_line\_before\_members\_in\_anonymous_types**

- When this rule is set to **true**, require members of anonymous types to be on separate lines.
- When this rule is set to **false**, require members of anonymous types to be on the same line.

Code examples:

```csharp
// csharp_new_line_before_members_in_anonymous_types = true
var z = new
{
    A = 3,
    B = 4
}

// csharp_new_line_before_members_in_anonymous_types = false
var z = new
{
    A = 3, B = 4
}
```

**csharp_new_line_between_query_expression_clauses**

- When this rule is set to **true**, require elements of query expression clauses to be on separate lines.
- When this rule is set to **false**, require elements of query expression clauses to be on the same line.

Code examples:

```csharp
// csharp_new_line_between_query_expression_clauses = true
var q = from a in e
        from b in e
        select a * b;

// csharp_new_line_between_query_expression_clauses = false
var q = from a in e from b in e
        select a * b;
```

Example .editorconfig file:

```EditorConfig
# CSharp formatting settings:
[*.cs]
csharp_new_line_before_open_brace = methods, properties, control_blocks, types
csharp_new_line_before_else = true
csharp_new_line_before_catch = true
csharp_new_line_before_finally = true
csharp_new_line_before_members_in_object_initializers = true
csharp_new_line_before_members_in_anonymous_types = true
csharp_new_line_between_query_expression_clauses = true
```

#### <a name="indent">Indentation options</a>

These formatting rules concern the use of indentation to format code.

The following table shows the rule names, applicable languages, default values, and first supported version of Visual Studio:

| Rule Name | Applicable Languages | Visual Studio Default | Visual Studio 2017 Version |
| ----------- | -------------------- | ----------------------| ----------------  |
| csharp_indent_case_contents |  C# | true | 15.3  |
| csharp_indent_switch_labels |  C# | true | 15.3  |
| csharp_indent_labels |  C# | no_change | 15.3  |

**csharp\_indent\_case_contents**

- When this rule is set to **true**, indent `switch` case contents.
- When this rule is set to **false**, do not indent `switch` case contents.

Code examples:

```csharp
// csharp_indent_case_contents = true
switch(c) {
    case Color.Red:
        Console.WriteLine("The color is red");
        break;
    case Color.Blue:
        Console.WriteLine("The color is blue");
        break;
    default:
        Console.WriteLine("The color is unknown.");
        break;
}

// csharp_indent_case_contents = false
switch(c) {
    case Color.Red:
    Console.WriteLine("The color is red");
    break;
    case Color.Blue:
    Console.WriteLine("The color is blue");
    break;
    default:
    Console.WriteLine("The color is unknown.");
    break;
}
```

**csharp\_indent\_switch_labels**

- When this rule is set to **true**, indent `switch` labels.
- When this rule is set to **false**, do not indent `switch` labels.

Code examples:

```csharp
// csharp_indent_switch_labels = true
switch(c) {
    case Color.Red:
        Console.WriteLine("The color is red");
        break;
    case Color.Blue:
        Console.WriteLine("The color is blue");
        break;
    default:
        Console.WriteLine("The color is unknown.");
        break;
}

// csharp_indent_switch_labels = false
switch(c) {
case Color.Red:
    Console.WriteLine("The color is red");
    break;
case Color.Blue:
    Console.WriteLine("The color is blue");
    break;
default:
    Console.WriteLine("The color is unknown.");
    break;
}
```

**csharp\_indent_labels**

This rule does not accept a **true** or **false** value; instead it accepts a value from the following table:

| Value | Description |
| ----- |:----------- |
| flush_left | Labels are placed at the leftmost column |
| one_less_than_current | Labels are placed at one less indent to the current context |
| no_change | Labels are placed at the same indent as the current context |

Code examples:

```csharp
// csharp_indent_labels= flush_left
class C
{
    private string MyMethod(...)
    {
        if (...) {
            goto error;
        }
error:
        throw new Exception(...);
    }
}

// csharp_indent_labels = one_less_than_current
class C
{
    private string MyMethod(...)
    {
        if (...) {
            goto error;
        }
    error:
        throw new Exception(...);
    }
}

// csharp_indent_labels= no_change
class C
{
    private string MyMethod(...)
    {
        if (...) {
            goto error;
        }
        error:
        throw new Exception(...);
    }
}
```

Example .editorconfig file:

```EditorConfig
# CSharp formatting settings:
[*.cs]
csharp_indent_case_contents = true
csharp_indent_switch_labels = true
csharp_indent_labels = flush_left
```

#### <a name="spacing">Spacing Options</a>

These formatting rules concern the use of space characters to format code.

The following table shows the rule names, applicable languages, default values, and first supported version of Visual Studio:

| Rule Name | Applicable Languages | Visual Studio Default | Visual Studio 2017 Version |
| ----------- | -------------------- | ----------------------| ----------------  |
| csharp_space_after_cast |  C# | false | 15.3  |
| csharp_space_after_keywords_in_control_flow_statements |  C# | true | 15.3  |
| csharp_space_between_method_declaration_parameter_list_parentheses |  C# | false | 15.3  |
| csharp_space_between_method_call_parameter_list_parentheses |  C# | false | 15.3  |
| csharp_space_between_parentheses |  C# | false | 15.3  |

**csharp\_space\_after_cast**

- When this rule is set to **true**, require a space between a cast and the value.
- When this rule is set to **false**, require _no_ space between the cast and the value.

Code examples:

```csharp
// csharp_space_after_cast = true
int y = (int) x;

// csharp_space_after_cast = false
int y = (int)x;
```

**csharp_space_after_keywords_in_control_flow_statements**

- When this rule is set to **true**, require a space after a keyword in a control flow statement such as a `for` loop.
- When this rule is set to **false**, require _no_ space after a keyword in a control flow statement such as a `for` loop.

Code examples:

```csharp
// csharp_space_after_keywords_in_control_flow_statements = true
for (int i;i<x;i++) { ... }

// csharp_space_after_keywords_in_control_flow_statements = false
for(int i;i<x;i++) { ... }
```

**csharp_space_between_method_declaration_parameter_list_parentheses**

- When this rule is set to **true**, place a space character after the opening parenthesis and before the closing parenthesis of a method declaration parameter list.
- When this rule is set to **false**, do not place space characters after the opening parenthesis and before the closing parenthesis of a  method declaration parameter list.

Code examples:

```csharp
// csharp_space_between_method_declaration_parameter_list_parentheses = true
void Bark( int x ) { ... }

// csharp_space_between_method_declaration_parameter_list_parentheses = false
void Bark(int x) { ... }
```

**csharp_space_between_method_call_parameter_list_parentheses**

- When this rule is set to **true**, place a space character after the opening parenthesis and before the closing parenthesis of a method call.
- When this rule is set to **false**, do not place space characters after the opening parenthesis and before the closing parenthesis of a method call.

Code examples:

```csharp
// csharp_space_between_method_call_parameter_list_parentheses = true
MyMethod( argument );

// csharp_space_between_method_call_parameter_list_parentheses = false
MyMethod(argument);
```

**csharp_space_between_parentheses**

This rule does not accept a **true** or **false** value; instead it accepts a value from the following table:

| Value | Description |
| ----- |:------------|
| control_flow_statements | Place space between parentheses of control flow statements |
| expressions | Place space between parentheses of expressions |
| type_casts | Place space between parentheses in type casts |

Code examples:

```csharp
// csharp_space_between_parentheses = control_flow_statements
for( int i;i<x;i++ ) { ... }

// csharp_space_between_parentheses = expressions
var z = ( x * y ) - ( ( y - x ) * 3);

// csharp_space_between_parentheses = type_casts
int y = ( int )x;
```

Example .editorconfig file:

```EditorConfig
# CSharp formatting settings:
[*.cs]
csharp_space_after_cast = true
csharp_space_after_keywords_in_control_flow_statements = true
csharp_space_between_method_declaration_parameter_list_parentheses = true
csharp_space_between_method_call_parameter_list_parentheses = true
csharp_space_between_parentheses = control_flow_statements, type_casts
```

#### <a name="wrapping">Wrapping options</a>

These formatting rules concern the use of single lines versus separate lines for statements and code blocks.

The following table shows the rule names, applicable languages, default values, and first supported version of Visual Studio:

| Rule Name | Applicable Languages | Visual Studio Default | Visual Studio 2017 Version |
| ----------- | -------------------- | ----------------------| ----------------  |
| csharp_preserve_single_line_statements |  C# | true | 15.3  |
| csharp_preserve_single_line_blocks |  C# | true | 15.3  |

**csharp_preserve_single_line_statements**

- When this rule is set to **true**, leave statements and member declarations on the same line.
- When this rule is set to **false**, leave statements and member declarations on different lines.

Code examples:

```csharp
//csharp_preserve_single_line_statements = true
int i = 0; string name = "John";

//csharp_preserve_single_line_statements = false
int i = 0;
string name = "John";
```

**csharp_preserve_single_line_blocks**

- When this rule is set to **true**, leave code block on single line.
- When this rule is set to **false**, leave code block on separate lines.

Code examples:

```csharp
//csharp_preserve_single_line_blocks = true
public int Foo { get; set; }

//csharp_preserve_single_line_blocks = false
public int MyProperty
{
    get; set;
}
```

Example .editorconfig file:

```EditorConfig
# CSharp formatting settings:
[*.cs]
csharp_preserve_single_line_statements = true
csharp_preserve_single_line_blocks = true
```

## See also

- [Quick Actions](../ide/quick-actions.md)
- [.NET naming conventions for EditorConfig](../ide/editorconfig-naming-conventions.md)
- [Create portable custom editor options](../ide/create-portable-custom-editor-options.md)
- [.NET Compiler Platform's .editorconfig file](https://github.com/dotnet/roslyn/blob/master/.editorconfig)
