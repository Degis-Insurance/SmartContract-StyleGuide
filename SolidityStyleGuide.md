
#  Solidity Style Guide

  

This guide is intended to provide coding conventions for writing Solidity code, specifically for Degis projects. The goal of this guide is consistency within Degis development.

  

Much of the structure and recommendations has been taken from [Solidity's style guide](https://docs.soliditylang.org/en/v0.8.13/style-guide.html). For more examples, please refer to it.

# Table of Content

```
code layout/
├── indentation
├── tabs or spaces
├── blank lines
├── maximum line length
├── source file encoding
├── imports
├── order of functions
├── whitespace in expressions
├── control structures
└── function declaration
mappings
variable declarations
other recommendations
order of layout
├── order of functions
└── template
naming convetions/
├── naming styles
├── names to avoid
├── contracts and library names
├── struct names
├── event names
├── function names
├── function parameter names
├── local and state variable names
├── constants
├── modifier names
├── enums
└── avoiding naming collisions
NatSpec/comments
└── tags
```

##  Code Layout

  

###  Indentation

  

Use 4 spaces per indentation level.

  


###  Tabs or Spaces

  

Spaces are the preferred indentation method.

  

Mixing tabs and spaces should be avoided.

  

###  Blank Lines

  

Surround top level declarations in Solidity source with two blank lines.

  

Within a contract surround function declarations with a single blank line.

  

Blank lines may be omitted between groups of related one-liners (such as stub functions for an abstract contract);

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

abstract contract I {
    function c() public virtual pure;
    function d() public virtual pure;
}


contract A is I {

    function c() public virtual pure {
        // ...
    }
    function d() public virtual pure {
        // ...
    }
}


contract B {
    // ...
}
```

  

###  Maximum Line Length

  

Keeping lines to a maximum of 79 (or 99) characters helps readers easily parse the code.

  

Wrapped lines should conform to the following guidelines.

1. The first parameter should not be attached to the opening parenthesis.
2. One, and only one, indent should be used.
3. Each parameter should fall on its own line.
4. The terminating element, );, should be placed on the final line by itself.

```
thisFunctionCallIsReallyLong(
    longArgument1,
    longArgument2,
    longArgument3
);
``` 

###  Source File Encoding

  

UTF-8 or ASCII encoding is preferred.

  

###  Imports

Import statements should always be placed at the top of the file.

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

import "./Owned.sol";

contract A {
    // ...
}


contract B is Owned {
    // ...
}
```

##  Order of Layout

  

Layout contract elements in the following order:

1. Pragma statements
2. Import statements
3. Interfaces
4. Libraries
5. Contracts

  

Inside each contract, library or interface, use the following order:

1. Type declarations
2. State variables
3. Events
4. Errors
5. Constructor
6. Modifiers
7. Functions

  


###  Order of Functions

  

Ordering helps readers identify which functions they can call.

  

Functions should be grouped according to their functionality beneath its correspondent header comment with the following names:

* receive (if exists)
* fallback (if exists)
* view
* set
* main (external & public)
* internal (internal, private)

include `pure` functions at the end of each function group.

### Template

Include the following template to assist on ordering all contract components.

```
// SPDX-License-Identifier: GPL-3.0

/*
 //======================================================================\\
 //======================================================================\\
  *******         **********     ***********     *****     ***********
  *      *        *              *                 *       *
  *        *      *              *                 *       *
  *         *     *              *                 *       *
  *         *     *              *                 *       *
  *         *     **********     *       *****     *       ***********
  *         *     *              *         *       *                 *
  *         *     *              *         *       *                 *
  *        *      *              *         *       *                 *
  *      *        *              *         *       *                 *
  *******         **********     ***********     *****     ***********
 \\======================================================================//
 \\======================================================================//
*/

pragma solidity ^0.8.13;

contract A {
    // ---------------------------------------------------------------------------------------- //
    // ************************************* Constants **************************************** //
    // ---------------------------------------------------------------------------------------- //
    / ...

    // ---------------------------------------------------------------------------------------- //
    // ************************************* Variables **************************************** //
    // ---------------------------------------------------------------------------------------- //
    / ...

    // ---------------------------------------------------------------------------------------- //
    // *************************************** Events ***************************************** //
    // ---------------------------------------------------------------------------------------- //
    / ...

    // ---------------------------------------------------------------------------------------- //
    // *************************************** Errors ***************************************** //
    // ---------------------------------------------------------------------------------------- //
    / ...

    // ---------------------------------------------------------------------------------------- //
    // ************************************* Constructor ************************************** //
    // ---------------------------------------------------------------------------------------- //

    constructor() {
        // ...
    }

    receive() external payable {
        // ...
    }

    fallback() external {
        // ...
    }

    // ---------------------------------------------------------------------------------------- //
    // ************************************** Modifiers *************************************** //
    // ---------------------------------------------------------------------------------------- //
    // ..

    // ---------------------------------------------------------------------------------------- //
    // *********************************** View Functions ************************************* //
    // ---------------------------------------------------------------------------------------- //
    // ...

    // ---------------------------------------------------------------------------------------- //
    // ************************************* Set Functions ************************************ //
    // ---------------------------------------------------------------------------------------- //
    // ...

    // ---------------------------------------------------------------------------------------- //
    // ************************************ Main Functions ************************************ //
    // ---------------------------------------------------------------------------------------- //
    // ...

    // ---------------------------------------------------------------------------------------- //
    // ********************************** Internal Functions ********************************** //
    // ---------------------------------------------------------------------------------------- //
    // ...

    // ---------------------------------------------------------------------------------------- //
    // *********************************** Pure Functions ************************************* //
    // ---------------------------------------------------------------------------------------- //
    // ...
}
```

###  Whitespace in Expressions

  

Avoid extraneous whitespace in the following situations:

* Immediately inside parenthesis, brackets or braces, with the exception of single line function declarations.
* Immediately before a comma, semicolon.
* More than one space around an assignment or other operator to align with another.
* Don’t include a whitespace in the receive and fallback functions.
`mint(position[1], Coin({name: "degis"}));`
  

###  Control Structures

  

The braces denoting the body of a contract, library, functions and structs should:

* open on the same line as the declaration
* close on their own line at the same indentation level as the beginning of the declaration.
* The opening brace should be preceded by a single space.
```
contract Coin {
    struct Bank {
        address owner;
        uint balance;
    }
}
```
  

The same recommendations apply to the control structures if, else, while, and for.

  

Additionally there should be a single space between the control structures if, while, and for and the parenthetic block representing the conditional, as well as a single space between the conditional parenthetic block and the opening brace.

  

For control structures whose body contains a single statement, omitting the braces is ok if the statement is contained on a single line.

  

For if blocks which have an else or else if clause, the else should be placed on the same line as the if’s closing brace. This is an exception compared to the rules of other block-like structures.
```
if (x < 3) {
    x += 1;
} else if (x > 7) {
    x -= 1;
} else {
    x = 5;
}

if (x < 3)
    x += 1;
else
    x -= 1;
```
  

###  Function Declaration

  

For short function declarations, it is recommended for the opening brace of the function body to be kept on the same line as the function declaration.

  

The closing brace should be at the same indentation level as the function declaration.

  

The opening brace should be preceded by a single space.

  

The modifier order for a function should be:

1. Visibility
2. Mutability
3. Virtual
4. Override
5. Custom modifiers

  
```
function increment(uint x) public pure onlyOwner returns (uint) {
    return x + 1;
}
```

For long function declarations, it is recommended to drop each parameter onto its own line at the same indentation level as the function body. The closing parenthesis and opening bracket should be placed on their own line as well at the same indentation level as the function declaration.

  

If a long function declaration has modifiers, then each modifier should be dropped to its own line.

  

Multiline output parameters and return statements should follow the same style recommended for wrapping long lines found in the `Maximum Line Length` section.

```
function thisFunctionNameIsReallyLong(
    address a,
    address b,
    address c
)
    public
    returns (
        address someAddressName,
        uint256 LongArgument,
        uint256 Argument
    )
{
    doSomething()

    return (
        veryLongReturnArg1,
        veryLongReturnArg2,
        veryLongReturnArg3
    );
}
```
  

For constructor functions on inherited contracts whose bases require arguments, it is recommended to drop the base constructors onto new lines in the same manner as modifiers if the function declaration is long or hard to read.
```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
// Base contracts just to make this compile
contract B {
    constructor(uint) {
    }
}


contract C {
    constructor(uint, uint) {
    }
}


contract D {
    constructor(uint) {
    }
}


contract A is B, C, D {
    uint x;

    constructor(uint param1, uint param2, uint param3, uint param4, uint param5)
        B(param1)
        C(param2, param3)
        D(param4)
    {
        // do something with param5
        x = param5;
    }
}
```
  

When declaring short functions with a single statement, it is permissible to do it on a single line.
`function shortFunction() public { doSomething(); }`
  

These guidelines for function declarations are intended to improve readability. Authors should use their best judgment as this guide does not try to cover all possible permutations for function declarations.

  

##  Mappings

  

In variable declarations, do not separate the keyword `mapping` from its type by a space. Do not separate any nested `mapping` keyword from its type by whitespace.

`mapping(uint => uint) map;`

  

##  Variable Declarations

  

Declarations of array variables should not have a space between the type and the brackets.

`uint[] x;`

  

##  Other Recommendations

  

* Strings should be quoted with double-quotes instead of single-quotes.

* Surround operators with a single space on either side.

* Operators with a higher priority than others can exclude surrounding whitespace in order to denote precedence. This is meant to allow for improved readability for complex statements. You should always use the same amount of whitespace on either side of an operator.

`x = (a+b) * (a-b);`

 

##  Naming Conventions

  

Naming conventions are powerful when adopted and used broadly. The use of different conventions can convey significant meta information that would otherwise not be immediately available.

  

The naming recommendations given here are intended to improve the readability, and thus they are not rules, but rather guidelines to try and help convey the most information through the names of things.

  

Lastly, consistency within a codebase should always supersede any conventions outlined in this document.

  

###  Naming Styles

  

To avoid confusion, the following names will be used to refer to different naming styles.

  

* `b` (single lowercase letter)
* `B` (single uppercase letter)
* `lowercase`
* `UPPERCASE`
* `UPPER_CASE_WITH_UNDERSCORES`
* `CapitalizedWords` (or CapWords)
* `mixedCase`

  

###  Names to Avoid

  

* `l` - Lowercase letter el
* `O` - Uppercase letter oh
* `I` - Uppercase letter eye

  

Never use any of these for single letter variable names. They are often indistinguishable from the numerals one and zero.

  

###  Contract and Library Names

  

* Contracts and libraries should be named using the `CapWords` style.
* Contract and library names should also match their filenames.
* If a contract file includes multiple contracts and/or libraries, then the filename should match the core contract. This is not recommended however if it can be avoided.

  

###  Struct Names

  

Structs should be named using the `CapWords` style.

  

###  Event Names

  

Events should be named using the `CapWords` style.

  

###  Function Names

  

Functions should use `mixedCase` style.

  

###  Private Function Names

  

Private Functions should use `_singleLeadingUnderscore` style.

  

###  Function Parameter Names

  

Function arguments should use `mixedCase` style.

When writing library functions that operate on a custom struct, the struct should be the first argument and should always be named `self`.

When a parameter name leads to naming collision, prioritize using `_singleLeadingUnderscore` style.

  

###  Local and State Variable Names

  

Local and State Variables should use `mixedCase` style.

  

###  Constants

  

Constants should be use `UPPER_CASE_WITH_UNDERSCORES` style.

  

###  Modifier Names

  

Modifiers should use `mixedCase` style.

  

###  Enums

  

Enums, in the style of simple type declarations, should be named using the `CapWords` style.

  

###  Avoiding Naming Collisions



`singleTrailingUnderscore_` and `_singleLeadingUnderscore` conventions are suggested when the desired name collides with that of a built-in or otherwise reserved name.

Private and function parameters should prioritize using `_singleLeadingUnderscore`.

  
##  NatSpec/Comments

  

Solidity contracts can also contain NatSpec comments. They are written with a triple slash `///` or a double asterisk block `/** ... */` and they should be used directly above function declarations or statements.

```
/**
 * @title Degis Income Sharing Contract
 * @notice This contract will receive part of the income from Degis products
 *         And the income will be shared by DEG holders (in the form of veDEG)
 *
 *         It is designed to be an ever-lasting reward
 *
 *         At first the reward is USDC.e and later may be transferred to Shield
 *         To enter the income sharing vault, you need to lock some veDEG
 *             - When your veDEG is locked, it can not be withdrawed
 *
 *         The reward is distributed per second like a farming pool
 *         The income will come from (to be updated)
 *             - IncomeMaker: Collect swap fee in naughty price pool
 *             - PolicyCore: Collect deposit/redeem fee in policy core
 */
```

  

###  Tags

It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI).

All tags are optional. The following table explains the purpose of each NatSpec tag and where it may be used.
|Tag|Description|Context|
|--|--|--|
|@title|A title that should describe the contract/interface|contract, library, interface|
|@author | The name of the author | contract, library, interface|
| @notice | Explain to an end user what this does | contract, library, interface, function, public state variable, event |
| @dev | Explain to a developer any extra details | contract, library, interface, function, state variable, event |
| @param | Documents a parameter | function, event |
| @return | Documents the return variables of a contract’s function | function, public state variable |
| @inheritdoc | Copies all missing tags from the base function (must be followed by the contract name) | function, public state variable |
| @custom:... | Custom tag, semantics is application-defined | everywhere |

If no tags are used then the Solidity compiler will interpret a `///` or `/**` comment in the same way as if it were tagged with `@notice`.

If your function contains multiple params or returns multiple values, then use multiple @param or @return statements.