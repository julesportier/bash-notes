# Introduction ([manual 1](https://www.gnu.org/software/bash/manual/bash.html#Introduction))

- A shell is basically **a macro processor that executes commands**.
- A Unix shell is both a **command interpreter** and a **programming language**.


# Definitions ([manual 2](https://www.gnu.org/software/bash/manual/bash.html#Definitions))

- **POSIX**: A family of open system standards based on Unix. Bash is primarily concerned with the Shell and Utilities portion of the POSIX 1003.1 standard.
- **blank**: A space or tab character.
- **builtin**: A command that is implemented internally by the shell itself, rather than by an executable program somewhere in the file system.
- **control operator**: A token that performs a control function. It is a newline or one of the following: `||`, `&&`, `&`, `;`, `;;`, `;&`, `;;&`, `|`, `|&`, `(`, or `)`.
- **exit status**: The value returned by a command to its caller. The value is restricted to eight bits, so the maximum value is 255.
- **field**: A unit of text that is the result of one of the shell expansions. After expansion, when executing a command, the resulting fields are used as the command name and arguments.
- **filename**: A string of characters used to identify a file.
- **job**: A set of processes comprising a pipeline, and any processes descended from it, that are all in the same process group.
- **job control**: A mechanism by which users can selectively stop (suspend) and restart (resume) execution of processes.
- **metacharacter**: A character that, when unquoted, separates words. A metacharacter is a space, tab, newline, or one of the following characters: `|`, `&`, `;`, `(`, `)`, `<`, or `>`.
- **name**: A word consisting solely of letters, numbers, and underscores, and beginning with a letter or underscore. Names are used as shell variable and function names. Also referred to as an identifier.
- **operator**: A control operator or a redirection operator. See Redirections, for a list of redirection operators. Operators contain at least one unquoted metacharacter.
- **process group**: A collection of related processes each having the same process group ID.
- **process group ID**: A unique identifier that represents a process group during its lifetime.
- **reserved word**: A word that has a special meaning to the shell. Most reserved words introduce shell flow control constructs, such as for and while.
- **return status**: A synonym for exit status.
- **signal**: A mechanism by which a process may be notified by the kernel of an event occurring in the system.
- **special builtin**: A shell builtin command that has been classified as special by the POSIX standard.
- **token**: A sequence of characters considered a single unit by the shell. It is either a word or an operator.
- **word**: A sequence of characters treated as a unit by the shell. Words may not include unquoted metacharacters.


# Basic Shell Features ([manual 3](https://www.gnu.org/software/bash/manual/bash.html#Basic-Shell-Features))

## Shell Syntax ([manual 3.1](https://www.gnu.org/software/bash/manual/bash.html#Shell-Syntax))

Describes in details how the shell handle the input that it's fed:

### Shell Operation ([manual 3.1.1](https://www.gnu.org/software/bash/manual/bash.html#Shell-Operation))

The general steps to parse and execute the input:
1. Read input
2. Break it into words and operators tokens
3. Parse the tokens into simple and compound commands
4. Perform expansions
5. Perform and remove redirections
6. Execute commands
7. Optionnaly wait for command to complete and collect exit status

### Quoting ([manual 3.1.2](https://www.gnu.org/software/bash/manual/bash.html#Quoting))

Quoting rules.
- `\` Litteral value of succeding character.
- `''` Litteral value of enclosed chars.
- `""` Only expands `$`, `` ` ` ``, (`!` outside POSIX mode). `*` and `@` have a special meaning.
- `$''` Only expands ANSI C escape sequences (e.g. `\n`).

### Comments ([manual 3.1.3](https://www.gnu.org/software/bash/manual/bash.html#Comments))

Lines beggining by `#` are ignored.

## Shell Commands ([manual 3.2](https://www.gnu.org/software/bash/manual/bash.html#Shell-Commands))

### Reserved Words ([manual 3.2.1](https://www.gnu.org/software/bash/manual/bash.html#Reserved-Words))

Words used to begin and end compound commands:
`if` `then` `elif` `else` `fi` `time`
`for` `in` `until` `while` `do` `done`
`case` `esac` `coproc` `select` `function`
`{` `}` `[[` `]]` `!`

### Pipelines ([manual 3.2.3](https://www.gnu.org/software/bash/manual/bash.html#Pipelines))

Sequence of commands separated by `|` or `&|` (== `2>&1 |`), each one executed in a subshell.
This connection is performed before any redirection.
By default the exit status is the one of the last command in the pipeline.

### List of Commands ([manual 3.2.4](https://www.gnu.org/software/bash/manual/bash.html#Lists))

Sequence of one or more pipelines separated by:
- Lower precendence
    - `;` (sequential execution), equivalent to newline
    - `&` (asynchronous execution), create background processes
- Higher precedence
    - `&&` (logical and)
    - `||` (logical or)

### Compound Commands ([manual 3.2.5](https://www.gnu.org/software/bash/manual/bash.html#Compound-Commands))

They are the shell programming language construct.
Each of them begins with a reserved word or operator and end with a corresponding one.
Any redirection associated apply to all commands within that compound command (unless overridden).

#### Looping Constructs [manual 3.2.5.1](https://www.gnu.org/software/bash/manual/bash.html#Looping-Constructs)

- `until` while test commands exit status != 0
- `while` while test commands exit status == 0
- `for` iterate a list (can be the result of an expansion, an array...)

#### Conditionals Constructs [manual 3.2.5.2](https://www.gnu.org/software/bash/manual/bash.html#Conditional-Constructs)

- `if`
- `case` to have multiple patterns (cases)
- `select` useful to generate menus
- `((...))` arithmetic expression, expands like in double quotes (don't expands double quotes inside of it)
- `[[...]]` enclose conditional expression, performing most of the expansions inside of it, (complex behavior, see manual).

Expressions may be combined using the following operators (in order of precedence):
`(exp)`, `! exp`, `exp1 && exp2`, `exp1 || exp2`

#### Grouping Commands [manual 3.2.5.3](https://www.gnu.org/software/bash/manual/bash.html#Command-Grouping)

- `( list )` executes the list of commands in a subshell
- `{ list; }` executes the list of commands in the current shell (there is some subtelties, see manual)

### Coprocesses [manual 3.2.6](https://www.gnu.org/software/bash/manual/bash.html#Coprocesses)

### Gnu Parallel [manual 3.2.7](https://www.gnu.org/software/bash/manual/bash.html#GNU-Parallel)

## Shell Functions [manual 3.3](https://www.gnu.org/software/bash/manual/bash.html#Shell-Functions)

## Shell Parameters [manual 3.4](https://www.gnu.org/software/bash/manual/bash.html#Shell-Parameters)


