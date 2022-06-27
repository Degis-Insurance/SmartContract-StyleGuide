# Javascript Style Guide

This guide is intended to provide coding conventions for writing Javascript files, specifically for Degis projects. The goal of this guide is consistency within Degis development. Vue, Typescript and React are also covered by these conventions.

You can use and configure [ESLint](https://eslint.org/) paired with [prettier](https://prettier.io/) to assist you in better the code quality, making it more legible and more consistent but it might not cover all cases or conventions indicated in this guide. Use your knowledge and common sense to decide on edge cases.

An installation guide for ESLint and Prettier is provided below.

Two configuration files for .eslintrc and .prettierrc will be provided at the end of this guide to assist you. Toggling `formatOnSave` on VSCode or `Beautify On Save` on Atom will help you automatically apply rules when saved.

## Table of Content

```
code layout/
├── indentation
├── tabs or spaces
├── blank lines
├── maximum line length
├── source file encoding
└── imports
order of layout/
├── whitespace in expressions
├── control structures
├── quotation marks
├── semicolons
├── no line continuations
└── trailing commas
syntax/
├── variable declarations
├── function declarations
├── ayncchoronous functions
├── error handling
├── ternary operators
├── constructors
├── import
└── export
naming conventions/
├── naming styles
├── names to avoid
├── class names
├── component names
├── enum names
├── function names
├── function parameter names
├── local and state variable names
├── constant names
└── avoiding naming collisions
Comments
ESlint
```

## Code Layout

### Indentation

Use 2 spaces per indentation level.

### Tabs or Spaces

Spaces are the preferred indentation method.

Mixing tabs and spaces should be avoided.

Toggle Soft Tabs in your Code Editor if a Tabs person.
For VSCode Code -> Preferences -> Settings:
```
"editor.tabSize": 2,
"editor.insertSpaces": true,
"editor.detectIndentation": true
```
### Blank Lines

A single blank line appears:

1. Between consecutive methods in a class or object literal
2. Within method bodies, sparingly create logical groupings of statements. Blank lines at the start or end of a function body are not allowed.
3. Optionally before the first or after the last method in a class or object literal (neither encouraged nor discouraged).

Multiple consecutive blank lines are not encouraged but are permitted.

Blank lines may be omitted between groups of related one-liners;

```
$axios.onError(error => {
    clearTimeout(timeout);
    if (loadingInstance) {
      loadingInstance.close();
    }

    if (!error.response) {
      return;
    }

    const code =
      parseInt(error.response && error.response.status) ||
      parseInt(error.response && error.response.code);

    if (error.response) {
      console.log('error.response: ', error.response.data);
    }
  });
```

### Maximum Line Length

Keeping lines to a maximum of 79 characters helps readers easily parse the code.

### Source File Encoding

UTF-8 encoding is preferred.

### Imports

Import statements should always be placed at the top of the file. Multiple named imports and deconstructed imports from a single file might have every import onto its own line at the same indentation level as the import statement.

```
import Vue from 'vue';
import lodash from 'lodash';
import dayjs from 'dayjs';
import Dinero from 'dinero.js';
import {
  foo,
  bar,
  thesis,
  } from 'techstack.js';

export default ({ app }) => {
  //
}
```

## Order of Layout

JavaScript files are dependent on several decisions and Tech Stack. As a general rule, structure your file in a manner where dependencies are placed above its use. An example:

1. Imports
2. Immediately Invoked Functions
3. Variables Declaration
4. Functions
5. Execution and Context
6. Inits & Event Listeners

### Whitespace in Expressions

Avoid extraneous whitespace in the following situations:

- Immediately inside parenthesis, brackets or braces, except for single line function declarations.
- Immediately before a comma, semicolon.
- More than one space around an assignment or other operator to align with another.
- Don’t include whitespace in the receive and fallback functions.

`const blockTimestamp = await getLatestBlockTimestamp(ethers.provider);`

- Operators with a higher priority than others can exclude surrounding whitespace in order to denote precedence. This is meant to allow for improved readability for complex statements. You should always use the same amount of whitespace on either side of an operator.

`x = (a+b) * (a-b);`

### Control Structures

The braces denoting the body of any component, function, if-statements and loops should:

- open on the same line as the declaration.
- close on their own line at the same indentation level as the beginning of the declaration.
- The opening brace should be preceded by a single space.

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

### Quotation marks

- Strings should be quoted with single-quotes instead of double-quotes.
- File references and classes should be quoted with double-quotes.
- When needed, use single quotes for the outermost layer.

`const z = '<div id="container"></div>'`

- Use template literals \`\` over complex string concatenation, particularly if multiple string literals are involved. Template literals may span multiple lines. If a template literal spans multiple lines, it does not need to follow the indentation of the enclosing block, though it may if the added whitespace does not matter.
-

```
function arithmetic(a, b) {
  return `Here is a table of arithmetic operations:
${a} + ${b} = ${a + b}
${a} - ${b} = ${a - b}
${a} * ${b} = ${a * b}
${a} / ${b} = ${a / b}`;
}
```

### Semicolons

A semicolon is required after the following situations:

- variable declaration
- expression
- return
- throw
- break
- continue
- do-while

### Space

Spaces are not required in the following cases:

- After the property name of the object
- after prefix unary operator
- before the postfix unary operator
- Before function call parentheses
- Whether it is a function declaration or a function expression, do not use a space before '('
- Array after '[' and before ']'
- Object after '{' and before '}'
- operator '(' after and before ')'

Spaces are required in the following situations:

- Before and after binary operators
- Ternary operator '?:' before and after
- before code block '{'
- Before the following keywords: else, while, catch,finally
- After the following keywords: `if`, `else`, `for`, `while`, `do`, `switch`, `case`, `try`, `catch`, `finally`, `with`, `return`, `typeof`
- After the single-line comment '//' (if the single-line comment and the code are in the same line, it is also required before '//'), after the multi-line _ comment '_'
- before the property value of the object
- For loop, leave a space after the semicolon, if there are multiple preconditions, leave a space after the comma
- Whether it is a function declaration or a function expression, there must be a space before '{'
- between the parameters of the function

### No line continuations

Do not use line continuations (that is, ending a line inside a string literal with a backslash) in either ordinary or template string literals. Even though ES5 allows this, it can lead to tricky errors if any trailing whitespace comes after the slash, and is less obvious to readers.

```
const longString = 'This is a very long string that far exceeds the 80 ' +
    'column limit. It does not contain long stretches of spaces since ' +
    'the concatenated strings are cleaner.';
```

### Trailing commas

Include a trailing comma whenever there is a line break between the final element and the closing bracket.

## Syntax

### Variable Declarations

Declare your variables below imports.
Declare all local variables with either const or let. Use const by default, unless a variable needs to be reassigned. The var keyword must not be used.
Avoid hoisting in every circumstance.

### Function Declarations

Function declaration depends on Tech Stack. Make sure you are locating functions following the intended design.
Functions may contain nested function definitions. If it is useful to give the function a name, it should be assigned to a local const.
Arrow functions provide concise function syntax but might have conflicting issues with some technologies like `Vue.js`. Be mindful of those issues.

### Asynchronous Functions

Prioritize using `async/await` to handle Promises. Avoid mixing chained declarations (aka. `.then()`) at all cost.

### Error handling

Use `try/catch` to handle errors. It prevents code to break during runtime and offers users a better experience.
Identify it with a string then log the error:
`console.log('Catched error in degisDEXURL:', error);`

### Ternary Operators

Ternary Operators are a great way to improve readability if used properly. Nested Ternary operators should have the same indentation level. Condition and first expression should be on the same line.

```
 result = (foo == bar)  ? result1 :
          (foo == baz)  ? result2 :
          (foo == qux)  ? result3 :
          (foo == quux) ? result4 :
                          fail_result;
```

### Constructors
Never invoke a constructor in a new statement without using parentheses ().

### Import

Avoid using `require` whenever possible. Prioritize utilizing `import/export`.

### Export

When exporting a named function, either use default exports or named exports applying the keyword to the function declaration.
When exporting a single anonymous function, export using `default` keyword.


## Naming Conventions

Naming conventions are powerful when adopted and used broadly. The use of different conventions can convey significant meta information that would otherwise not be immediately available.
The naming recommendations given here are intended to improve the readability, and thus they are not rules, but rather guidelines to try and help convey the most information through the names of things.
Give as descriptive a name as possible, within reason. Do not worry about saving horizontal space as it is far more important to make your code immediately understandable by a new reader.
Do not use abbreviations that are ambiguous or unfamiliar to readers outside Degis projects, and do not abbreviate by deleting letters within a word.
Identifiers use only ASCII letters and digits, and, in a small number of cases noted below, underscores and very rarely (when required by frameworks like Vue) dollar signs.
Lastly, consistency within a codebase should always supersede any conventions outlined in this document.

### Naming Styles

To avoid confusion, the following names will be used to refer to different naming styles.

- `b` (single lowercase letter)
- `B` (single uppercase letter)
- `lowercase`
- `UPPERCASE`
- `UPPER_CASE_WITH_UNDERSCORES`
- `CapitalizedWords` (or CapWords)
- `mixedCase`

### Names to Avoid

- `l` - Lowercase letter el
- `O` - Uppercase letter oh
- `I` - Uppercase letter eye

Never use any of these for single-letter variable names. They are often indistinguishable from the numerals one and zero.


### Class Names

Classes should use the `CapWords` style.

### Component Names

Components should use the `CapWords` style.

### Enum Names

Enums should use the `CapWords` style.

### Function Names

Functions should use `mixedCase` style.

### Function Parameter Names

Function arguments should use `mixedCase` style.

When a parameter name leads to naming collision, prioritize using `_singleLeadingUnderscore` style.

### Local and State Variable Names

Local and State Variables should use `mixedCase` style.

### Constant Names

Global `const` (also known as symbolic consatnts) should use `UPPER_CASE_WITH_UNDERSCORES` style.
Reference `const` should use `mixedCase` style.
Scoped constants should use `mixedCase` style.

### Avoiding Naming Collisions

`singleTrailingUnderscore_` and `_singleLeadingUnderscore` conventions are suggested when the desired name collides with that of a built-in or otherwise reserved name.

## Comments

Comments are incentivized but not required. Use comments to clarify intent. It can also be used to indicate the required input format or parameter specification.
Comments should be placed above what it refers to.

## ESLint

ESLint is a code formatter with a lot of options and flexibility. It finds and fixes problems in JavaScript code. It requires Node.js and works on Windows, Mac and Linux. Current implementation should _enforce_ the rules mentioned in this guide.

`npm install eslint --save-dev` or `yarn add eslint --dev`


`npm init @eslint/config` or `yarn create @eslint/config`

Accept standard configs. Then, paste the following in .eslintrc.js:

```
module.exports = {
  env: {
    browser: true,
    es2021: true,
    node: true,
    mocha: true,
  },
  extends: [
    "eslint:recommended",
    // Vue "plugin:vue/essential",
    // React "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:prettier/recommended",
    "plugin:node/recommended",
  ],
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: "latest",
    sourceType: "module",
  },
  plugins: [
    // Vue "vue",
    // React "react",
    // Typescript "@typescript-eslint",
    "prettier",
  ],
  rules: {
    indent: ["error", 4],
    "linebreak-style": ["error", "auto"],
    quotes: ["error", "single"],
    semi: ["error", "always"],
    "comma-dangle": ["error", "always-multiline"],
    "node/no-unsupported-features/es-syntax": [
      "error",
      { ignores: ["modules"] },
    ],
    "prettier/prettier": [
      "error",
      {
        endOfLine: "auto",
      },
    ],
    camelcase: "warn",
    // Typescript "@typescript-eslint/camelcase": "warn",
    "prefer-const": ["error", { destructuring: "all" }],
    "no-var": "error",
  },
};
```

Then, uncomment the Tech Stack you are currently working on.

# Prettier

Prettier is an opinionated code formatter with limited configuration options. It is currently optional since ESLint should cover most cases in Degis project development. It might be used in the future.

`npm install --save-dev --save-exact prettier`
`echo {}> .prettierrc.json`

A .prretierrc file example:

```
{
  "singleQuote": true,
  "trailingComma": "all",
  "semi": true,
  "arrowParens": "avoid",
  "proseWrap": "preserve"
}
```