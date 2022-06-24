# Introduction

This guide is intended to provide coding conventions for writing Python files, specifically for Degis projects. The goal of this guide is to better the code quality and make it more legible and consistent within Degis development. Use your knowledge and common sense to decide on edge cases.

Much of the structure and recommendations have been taken from Python's [PEP8](https://peps.python.org/pep-0008/) Style Guide. If you need more examples, please reference them.

You can use and configure [PyLint](https://eslint.org/) to assist you in better the code quality, making it more legible and more consistent but it might not cover all cases or conventions indicated in this guide. Use your knowledge and common sense to decide on edge cases.

An installation guide for PyLint is provided below.

A configuration file for .pylintrc will be provided at the end of this guide to assist you.
Toggling `formatOnSave` on VSCode or `Beautify On Save` on Atom will help you automatically apply rules when saved.

## Table of Content

```
code Layout/
├── indentation
├── tabs or spaces
├── maximum line length
├── backslashes
├── binary operators line breaks
├── blank lines
├── source file encoding
├── imports
├── module level dunder names
├── string quotes
├── whitespace in expressions and statements
├── trailing commas
└── other recommendations
naming conventions/
├── naming styles
├── names to avoid
├── file names
├── class names
├── class attribute names
├── "magic" object names
├── type variable names
├── enum names
├── function names
├── function parameter names
├── local and state variable names
├── constant names
├── internal attribute names
├── function and method arguments
└──avoiding naming collisions
programming recommendations/
├── is not operator
├── def statements
├── try/except
└── return statements
comments
pylint
```

## Code Layout

### Indentation

Use 4 spaces per indentation level.

Continuation lines should align wrapped elements either vertically using Python’s implicit line joining inside parentheses, brackets and braces, or using a hanging indent [1]. When using a hanging indent the following should be considered; there should be no arguments on the first line and further indentation should be used to clearly distinguish itself as a continuation line.

```
foo = long_function_name(var_one, var_two,
                         var_three, var_four)
```

```
foo = long_function_name(
  var_one, var_two, // optional "hanging"
  var_three, var_four)
```

```
my_list = [
    1, 2, 3,
    4, 5, 6,
    ]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
    )
```

```
if (this_is_one_thing and
    that_is_another_thing):
    do_something()
```

### Tabs or Spaces

4 spaces are the preferred indentation method.

Tabs or spaces should be used to remain consistent with code that is already indented with tabs.

Python disallows mixing tabs and spaces for indentation.

Toggle Soft Tabs in your Code Editor if a Tabs person.
For VSCode Code -> Preferences -> Settings:
```
"editor.tabSize": 4,
"editor.insertSpaces": true,
"editor.detectIndentation": true
```

### Maximum Line Length

Limit all lines to a maximum of 79 characters.

For flowing long blocks of text with fewer structural restrictions (docstrings or comments), the line length should be limited to 72 characters.

### Backslashes

The preferred way of wrapping long lines is by using Python’s implied line continuation inside parentheses, brackets and braces. Long lines can be broken over multiple lines by wrapping expressions in parentheses. These should be used in preference to using a backslash for line continuation.

Backslashes may still be appropriate at times. For example, long, multiple with-statements could not use implicit continuation before Python 3.10, so backslashes were acceptable for that case:

```
with open('/path/to/some/file/you/want/to/read') as file_1, \
     open('/path/to/some/file/being/written', 'w') as file_2:
    file_2.write(file_1.read())
```

Another such case is with assert statements.

Make sure to indent the continued line appropriately.

### Binary Operators Line Breaks

Improve readability for binary operations by using a structure that indents operators to first operand identation.

```
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)
```

### Blank Lines

Surround top-level function and class definitions with two blank lines.

Method definitions inside a class are surrounded by a single blank line.

Extra blank lines may be used (sparingly) to separate groups of related functions. Blank lines may be omitted between a bunch of related one-liners (e.g. a set of dummy implementations).

Use blank lines in functions, sparingly, to indicate logical sections.

### Source File Encoding

Always use UTF-8, and should not have an encoding declaration.

All identifiers in the Python standard library MUST use ASCII-only identifiers.

### Imports

Imports are always put at the top of the file, just after any module comments and docstrings, and before module globals and constants.

Imports should usually be on separate lines.

If imports have a shared package they might be imported in the same line.

Wildcard imports (from <module> import \*) should be avoided, as they make it unclear which names are present in the namespace, confusing both readers and many automated tools.

```
import os
import sys
from subprocess import Popen, PIPE
```

### Module Level Dunder Names

Module level “dunders” (i.e. names with two leading and two trailing underscores) such as `__all__`, `__author__`, `__version__`, etc. should be placed after the module docstring but before any import statements except from `__future__` imports. Python mandates that future-imports must appear in the module before any other code except docstrings.

```
from __future__ import barry_as_FLUFL

__all__ = ['a', 'b', 'c']
__version__ = '0.1'
__author__ = 'Cardinal Biggles'

import os
import sys
```

### String Quotes

Prioritize using double-quotes instead of single-quotes.

For triple-quoted strings, always use double quote characters to be consistent with the docstring convention in PEP 257.

### Whitespace in Expressions and Statements

Avoid extraneous whitespace in the following situations:

 * Immediately inside parentheses, brackets or braces. However, in a slice the colon acts like a binary operator, and should have equal amounts on either side.
  `spam(ham[1], {eggs: 2})`
  `ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]`
 * Immediately before the open parenthesis that starts the argument list of a function call
 * Immediately before the open parenthesis that starts an indexing or slicing
 * More than one space around an assignment (or other) operator to align it with another

### Trailing Commas

Trailing commas are usually optional, except they are mandatory when making a tuple of one element. For clarity, it is recommended to surround the latter in (technically redundant) parentheses.
When trailing commas are redundant, they are often helpful when a version control system is used, when a list of values, arguments or imported items is expected to be extended over time.

```
FILES = ('setup.cfg',)
CASES = [
    'operator.cfg',
    'exit.ini',
    ]
```
### Other Recommendations

 * Avoid trailing whitespace anywhere. Because it’s usually invisible, it can be confusing: e.g. a backslash followed by a space and a newline does not count as a line continuation marker. Some editors don’t preserve it and many projects (like CPython itself) have pre-commit hooks that reject it.
 * Always surround these binary operators with a single space on either side: assignment (=), augmented assignment (+=, -= etc.), comparisons (==, <, >, !=, <>, <=, >=, in, not in, is, is not), Booleans (and, or, not).
 * If operators with different priorities are used, consider adding whitespace around the operators with the lowest priority(ies). Use your own judgment; however, never use more than one space, and always have the same amount of whitespace on both sides of a binary operator.
 * Function annotations should use the normal rules for colons and always have spaces around the -> arrow if present. (See Function Annotations below for more about function annotations.).
 * When combining an argument annotation with a default value, however, do use spaces around the = sign.
Compound statements (multiple statements on the same line) are generally discouraged.


## Naming Conventions

Naming conventions are powerful when adopted and used broadly. The use of different conventions can convey significant meta information that would otherwise not be immediately available, like conveying privacy intent.

The naming recommendations given here are intended to improve the readability, and thus they are not rules, but rather guidelines to try and help convey the most information through the names of things.

Give as descriptive a name as possible, within reason. Do not worry about saving horizontal space as it is far more important to make your code immediately understandable by a new reader.

Do not use abbreviations that are ambiguous or unfamiliar to readers outside Degis projects, and do not abbreviate by deleting letters within a word.

Lastly, consistency within a codebase should always supersede any conventions outlined in this document.

### Naming Styles

To avoid confusion, the following names will be used to refer to different naming styles.

- `b` (single lowercase letter)
- `B` (single uppercase letter)
- `lowercase`
- `lowercase_with_underscores`
- `UPPERCASE`
- `UPPER_CASE_WITH_UNDERSCORES`
- `CapitalizedWords` (or CapWords)
- `mixedCase`
- `singleTrailingUnderscore_`
- `_singleLeadingUnderscore`
- `__double_leading_underscore`
- `__double_leading_and_trailing_underscore__`
- `_0_ordered_lowercase_with_underscores`

### Names to Avoid

- `l` - Lowercase letter el
- `O` - Uppercase letter oh
- `I` - Uppercase letter eye

Never use any of these for single-letter variable names. They are often indistinguishable from the numerals one and zero.

### File Names

It is encouraged to name Files using the `_0_ordered_lowercase_with_underscores` style. If ordering is undesired, `lowercase_with_underscores` should suffice.

### Class Names

Classes should use the `CapWords` style.
To avoid name clashes with subclasses, use `__double_leading_underscore` to invoke Python’s name mangling rules.

### Class Attribute Names

Class attributes should use the `__double_leading_underscore` style.

### "Magic" Object Names

"Magic" objects or attributes that live in user-controlled namespaces should use `__double_leading_and_trailing_underscore__` style.

### Type Variable Names

Type Variable names should use the `CapWords` style.

### Enum Names

Enums should use the `CapWords` style.

### Function Names

Functions should use `lowercase_with_underscores` style.
`mixedCase` is allowed in some cases to maintain backward compatibility.
Use `_singleLeadingUnderscore` only for non-public methods and instance variables.

### Function Parameter Names

Function arguments should use `lowercase_with_underscores` style.
`mixedCase` is allowed in some cases to maintain backward compatibility.

### Local and State Variable Names

Local and State Variables should use `lowercase_with_underscores` style.
`mixedCase` is allowed in some cases to maintain backward compatibility.

### Constant Names

Global `const` (also known as symbolic consatnts) should use `UPPER_CASE_WITH_UNDERSCORES` style.
Reference `const` should use `lowercase_with_underscores` style.
Scoped constants should use `lowercase_with_underscores` style.

### Internal Attribute Names

Internal attributes should use `_singleLeadingUnderscore` style.

### Function and Method Arguments

Always use self for the first argument to instance methods.
Always use cls for the first argument to class methods.

### Avoiding Naming Collisions

conventions are suggested when the desired name collides with that of a built-in or otherwise reserved name.
You should mainly use `singleTrailingUnderscore_` styles.

## Programming Recommendations

### is not Operator

Use `is not` operator rather than `not ... is`. While both expressions are functionally identical, the former is more readable and preferred.

`if foo is not None:`

### def statements

Use a def statement instead of an assignment statement that binds a lambda expression directly to an identifier.

`def f(x): return 2\*x`

### Try/Except

Minimize the amount of code in a `try/except` block. The larger the body of the try, the more likely that an exception will be raised by a line of code that you didn’t expect to raise an exception. In those cases, the `try/except` block hides a real error.
Use the finally clause to execute code whether or not an exception is raised in the try block. This is often useful for cleanup, i.e., closing a file.
When catching exceptions, mention specific exceptions whenever possible instead of using a bare `except: clause:`

```
try:
    import platform_specific_module
except ImportError:
    platform_specific_module = None
```

### Return Statements

Be consistent in return statements. Either all return statements in a function should return an expression, or none of them should. If any return statement returns an expression, any return statements where no value is returned should explicitly state this as return None, and an explicit return statement should be present at the end of the function (if reachable).

```
def foo(x):
    if x >= 0:
        return math.sqrt(x)
else:
    return None

def bar(x):
    if x < 0:
        return None
    return math.sqrt(x)
```

## Comments

Comments should be complete sentences. The first word should be capitalized, unless it is an identifier that begins with a lower case letter (never alter the case of identifiers!).
Block comments generally consist of one or more paragraphs built out of complete sentences, with each sentence ending in a period.
You should use two spaces after a sentence-ending period in multi- sentence comments, except after the final sentence.
Ensure that your comments are clear and easily understandable to other speakers of the language you are writing in.
Block comments generally apply to some (or all) code that follows them, and are indented to the same level as that code. Each line of a block comment starts with a # and a single space (unless it is indented text inside the comment).
Paragraphs inside a block comment are separated by a line containing a single #.
Use inline comments sparingly.

## PyLint

PyLint is a code formatter with a lot of options and flexibility. It finds and fixes problems in Python code. It requires Node.js and works on Windows, Mac and Linux. Current implementation should _enforce_ the rules mentioned in this guide.

To install, run the following commands:

`pip install pylint`


`pylint --generate-rcfile > .pylintrc`

Then, paste the following in .pylintrc:

```
[MAIN]

analyse-fallback-blocks=no
fail-under=10
ignore=CVS
ignore-patterns=^\.#
jobs=1
limit-inference-results=100
persistent=yes
py-version=3.8
recursive=no
suggestion-mode=yes
unsafe-load-any-extension=yes

[REPORTS]

evaluation=max(0, 0 if fatal else 10.0 - ((float(5 * error + warning + refactor + convention) / statement) * 10))
reports=no
score=yes


[MESSAGES CONTROL]

confidence=HIGH,
           CONTROL_FLOW,
           INFERENCE,
           INFERENCE_FAILURE,
           UNDEFINED

disable=raw-checker-failed,
        bad-inline-option,
        locally-disabled,
        file-ignored,
        suppressed-message,
        useless-suppression,
        deprecated-pragma,
        use-symbolic-message-instead

enable=c-extension-no-member


[BASIC]

argument-naming-style=snake_case
attr-naming-style=snake_case
bad-names=foo,
          bar,
          baz,
          toto,
          tutu,
          tata,
          l,
          O,
          I,

class-attribute-naming-style=any
class-const-naming-style=UPPER_CASE
class-naming-style=PascalCase
const-naming-style=UPPER_CASE
docstring-min-length=-1
function-naming-style=snake_case
good-names=i,
           j,
           k,
           ex,
           Run,
           _

include-naming-hint=yes
inlinevar-naming-style=any
method-naming-style=snake_case
module-naming-style=snake_case
no-docstring-rgx=^_
property-classes=abc.abstractproperty
variable-naming-style=snake_case


[CLASSES]

check-protected-access-in-special-methods=no
defining-attr-methods=__init__,
                      __new__,
                      setUp,
                      __post_init__

exclude-protected=_asdict,
                  _fields,
                  _replace,
                  _source,
                  _make

valid-classmethod-first-arg=cls
valid-metaclass-classmethod-first-arg=cls


[DESIGN]

max-args=7
max-attributes=7
max-bool-expr=5
max-branches=12
max-locals=15
max-parents=7
max-public-methods=20
max-returns=6
max-statements=50
min-public-methods=2


[EXCEPTIONS]

overgeneral-exceptions=BaseException,
                       Exception


[FORMAT]

expected-line-ending-format=
ignore-long-lines=^\s*(# )?<?https?://\S+>?$
indent-after-paren=4
indent-string='    '
max-line-length=80
max-module-lines=1000
single-line-class-stmt=no
single-line-if-stmt=no


[IMPORTS]

allow-wildcard-with-all=yes
known-third-party=enchant


[LOGGING]

logging-format-style=old
logging-modules=logging


[MISCELLANEOUS]

notes=FIXME,
      XXX,
      TODO


[REFACTORING]

max-nested-blocks=7
never-returning-functions=sys.exit,argparse.parse_error


[SIMILARITIES]

ignore-comments=yes
ignore-docstrings=yes
ignore-imports=yesn
ignore-signatures=yes
min-similarity-lines=4


[SPELLING]

max-spelling-suggestions=4
spelling-ignore-comment-directives=fmt: on,fmt: off,noqa:,noqa,nosec,isort:skip,mypy:
spelling-store-unknown-words=no


[STRING]

check-quote-consistency=yes
check-str-concat-over-line-jumps=no


[TYPECHECK]

contextmanager-decorators=contextlib.contextmanager
ignore-none=yes
ignore-on-opaque-inference=yes
ignored-checks-for-mixins=no-member,
                          not-async-context-manager,
                          not-context-manager,
                          attribute-defined-outside-init

ignored-classes=optparse.Values,thread._local,_thread._local,argparse.Namespace
missing-member-hint=yes
missing-member-hint-distance=1
missing-member-max-choices=1
mixin-class-rgx=.*[Mm]ixin


[VARIABLES]
allow-global-unused-variables=no
callbacks=cb_,
          _cb
dummy-variables-rgx=_+$|(_[a-zA-Z0-9_]*[a-zA-Z0-9]+?$)|dummy|^ignored_|^unused_
ignored-argument-names=_.*|^ignored_|^unused_
init-import=no
redefining-builtins-modules=six.moves,past.builtins,future.builtins,builtins,io
```