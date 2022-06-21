#  Hardhat Style Guide

  

This guide is intended to provide coding conventions for writing hardhat tests, specifically for Degis projects. The goal of this guide is consistency within Degis development.

Hardhat allows you to use Truffle to test your smart contracts. It automatically exposes [mocha](https://mochajs.org/) test framework. For more examples, please refer to it.

The preferred assertion library to use is [chai](https://www.chaijs.com/).
The behavior-driven development (BDD) style utilized in Degis development is [expect](https://www.chaijs.com/guide/styles/#expect). It can also be used as a reference.

A Degis Hardhat test is typically written in typescript.



## Table of Content

 
```
code layout/
├── indentation
├── tabs or spaces
├── blank lines
├── maximum line length
├── source file encoding
├── imports
├── order of layout
├── order of scope
├── whitespace in expressions
├── control structures
├── descriptions
└── assertion statements
variable declarations
other recommendations
naming convetions/
├── naming styles
├── names to avoid
├── type names
├── function names
├── function parameter names
├── local and state variable names
├── factories
└── avoiding naming collisions
comments
```

 

##  Code Layout

  

###  Indentation

  

Use 2 spaces per indentation level.

  


###  Tabs or Spaces

  

Spaces are the preferred indentation method.

  

Mixing tabs and spaces should be avoided.

  

###  Blank Lines

  

Surround `describe`, `beforeEach`, `it` and `expect` declarations with one blank line.

 
Depending on functionality and readability, variable declaration might be surrounded with one blank line.
  

Blank lines may be omitted between groups of related one-liners;

```
//
import { getLatestBlockTimestamp, toWei } from "../utils";

describe("Degis Staking", function () {
  let StakingPoolFactory: StakingPoolFactory__factory,
    factory: StakingPoolFactory;
  let DegisToken: DegisToken__factory, degis: DegisToken;
  let MockERC20: MockERC20__factory, poolToken: MockERC20;
  let CoreStakingPool: CoreStakingPool__factory, pool: CoreStakingPool;

  let dev_account: SignerWithAddress,
    testAddress: SignerWithAddress,
    user1: SignerWithAddress;

  it("should be able to check the pool's information", async function () {
    
     const poolInfo = await factory.getPoolData(poolToken.address);
     expect(poolInfo.poolAddress).to.equal(contractAddress);
     expect(poolInfo.poolToken).to.equal(poolToken.address);
     expect(poolInfo.startTimestamp).to.equal(blockTimestamp);
     expect(poolInfo.degisPerSecond).to.equal(toWei("1"));
    }
}
//
```

  

###  Maximum Line Length

  
Keeping lines to a maximum of 79 (or 99) characters helps readers easily parse the code.


###  Source File Encoding

  

UTF-8 or ASCII encoding is preferred.

  

###  Imports

Import statements should always be placed at the top of the file. Multiple named imports and deconstructed imports from a single file might have every import onto its own line at the same indentation level as the import statement.

```
import { SignerWithAddress } from "@nomiclabs/hardhat-ethers/signers";
import { expect } from "chai";
import { formatEther, getContractAddress } from "ethers/lib/utils";
import { ethers } from "hardhat";
import {
  CoreStakingPool,
  CoreStakingPool__factory,
  DegisToken,
  DegisToken__factory,
  MockERC20,
  MockERC20__factory,
  StakingPoolFactory,
  StakingPoolFactory__factory,
} from "../../typechain";
```


##  Order of Layout

Hardhat tests follow a pattern of chained natural language assertions. Those assertions are encapsulated by thier parent assertion:

1. Imports
2. describe
   * beforeEach
   * // test assertions
3. functions

## Order of Scope

Hardhat tests follow a pattern of chained natural language assertions. Those assertions are encapsulated by their parent assertion:

*  describe
   *  nested describe
      *  it
         *  expect
 

###  Whitespace in Expressions

  

Avoid extraneous whitespace in the following situations:

* Immediately inside parenthesis, brackets or braces, except for single line function declarations.
* Immediately before a comma, semicolon.
* More than one space around an assignment or other operator to align with another.
* Don’t include whitespace in the receive and fallback functions.


`const blockTimestamp = await getLatestBlockTimestamp(ethers.provider);`
  

###  Control Structures

  

The braces denoting the body of any component, function, if-statements and loops should:

* open on the same line as the declaration.
* close on their own line at the same indentation level as the beginning of the declaration.
* The opening brace should be preceded by a single space.
```
describe("Factory functions", function () {
    it("should have the correct owner", async function () {
      expect(await factory.owner()).to.equal(dev_account.address);
    });
}
```

For control structures whose body contains a single statement, omitting the braces is ok if the statement is contained on a single line.


For if blocks that have an else or else if clause, the else should be placed on the same line as the if’s closing brace. This is an exception compared to the rules of other block-like structures.
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
  
### Descriptions

 

Keeping `describe`, `it` and `expect` descriptions to the core expected behavior improves readability. Make sure that your assertions follow a natural language pattern.

Keep it in the present tense.

Write all steps from third-person point of view.

`describe` words be Capitalized.
`it` words should be lowercased.
`expect` depends on proper string casing and type.

 * describe("Topic Being Tested")
    * it("should be able to behave this way")
       * expect(statement).to.equal(result)
 

###  Assertion Statements

  

For short asssertions, it is recommended for the opening brace of the function body to be kept on the same line as the assertion body.

  

The closing brace should be at the same indentation level as the assertion statement.

  

The opening brace should be preceded by a single space.


For long statements, it is recommended to drop each parameter and chained assertions onto its own line at the same indentation level as the function body. The closing parenthesis should be placed on its own line and at the same indentation level as the assertion declaration. 

```
await expect(
        factory.createPool(poolToken.address, blockTimestamp, toWei("1"))
      )
        .to.emit(factory, "PoolRegistered")
        .withArgs(
          dev_account.address,
          poolToken.address,
          contractAddress,
          toWei("1")
        );
```


When declaring short functions with a single statement, it is permissible to do it on a single line.
`function shortFunction() { doSomething(); }`
  

These guidelines for function declarations are intended to improve readability. Authors should use their best judgment as this guide does not try to cover all possible permutations.

##  Variable Declarations


Avoid hoisting whenever necessary. Declare all your variables at the top of any scope. For variable reassignment, consider that the body of a `describe` block is executed before `beforeEach` blocks.
  

##  Other Recommendations

  

* Strings should be quoted with double-quotes instead of single-quotes.

* Surround operators with a single space on either side.

* Operators with a higher priority than others can exclude surrounding whitespace in order to denote precedence. This is meant to allow for improved readability for complex statements. You should always use the same amount of whitespace on either side of an operator.

`x = (a+b) * (a-b);`

### principles

Tests must start with a clean state. This means prefer `beforeEach` to `before`. Re-instantiate objects before running each `it` blocks. Create every file required by a test in a `beforeEach`. Reset any side effects done on the test environment after each test.

Tests must be runnable in isolation. Each test must pass if they’re run alone. You can run a single test by using mocha test.js --grep 'test name'.
 

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

  

Never use any of these for single-letter variable names. They are often indistinguishable from the numerals one and zero.

  

###  Type Names

  

Structs should be named using the `CapWords` style. Factories are specificed by a trailing `__Factory`.

e.g:
`StakingPool__Factory`

  

###  Function Names

  

Functions should use `mixedCase` style.



###  Function Parameter Names

  

Function arguments should use `mixedCase` style.

When a parameter name leads to naming collision, prioritize using `_singleLeadingUnderscore` style.

  

###  Local and State Variable Names

  

Local and State Variables should use `mixedCase` style.

  

###  Factories

  

Factories should use `CapWords` style.


### Constant Names

Constans should use `UPPER_CASE_WITH_UNDERSCORES` style.

  
###  Avoiding Naming Collisions



`singleTrailingUnderscore_` and `_singleLeadingUnderscore` conventions are suggested when the desired name collides with that of a built-in or otherwise reserved name.

Private and function parameters should prioritize using `_singleLeadingUnderscore`.

  
##  Comments

Comments are incentivized but not required. Use comments to clarify intent. It can also be used to indicate the required input format or parameter specification. Comments should be placed above what it refers to.
```
// 18 decimals for buyer token
BuyerToken = await ethers.getContractFactory("BuyerToken");

//USDC.e Contract = 0xA7D7079b0FEaD91F3e65f86E8915Cb59c1a4C664
stablecoinAddress = await getContractAddress(contractAddress);
```