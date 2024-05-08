This is a project to implement a parser and GUI using Python, organized using object-oriented programming principles.

# Context Free Grammar
line → expression exit_command

line → line expression exit_command

line → exit_command

line → line exit_command

line → UserIn VAR '=' expression exit_command

line → Print expression exit_command

-------------------------------------------------------------------------------------------------------------------

expression → term

expression → term '+' expression

expression → term '-' expression

expression → term UserIn

expression → VAR

-------------------------------------------------------------------------------------------------------------------

term → factor

term → factor '*' term

term → factor '/' term

term → factor UserIn

term → VAR

-------------------------------------------------------------------------------------------------------------------

factor → primary

factor → primary '^' factor

factor → primary UserIn

factor → VAR

-------------------------------------------------------------------------------------------------------------------

primary → number

primary → '(' expression ')'

-------------------------------------------------------------------------------------------------------------------

exit_command → EXIT

-------------------------------------------------------------------------------------------------------------------

# Description

Line:

An expression followed by an exit command
A line followed by an expression and an exit command
An exit command
A line followed by an exit command
User input stored in a variable followed by an expression
Print statements takes an expression and displays the result
Expression:

A term
A term followed by '+' and another expression
A term followed by '-' and another expression
A term followed by user input
A variable
Term:

A factor
A factor multiplied by another term
A factor divided by another term
A factor followed by user input
A variable
Factor:

A primary expression
A primary expression raised to the power of another factor
A primary expression followed by user input
A variable
Primary:

A number
An expression enclosed in parentheses
Exit Command:

The exit command "EXIT"


# Python Tokenizer Documentation
This document describes the implementation of a lexical analyzer (tokenizer) in Python, designed to convert a string input into a list of tokens based on specified patterns. The tokenizer handles whitespace, comments, and various syntactic elements of a simplified programming language.

# Token Types
Each token type corresponds to a specific pattern in the input language. The tokenizer identifies the following token types:

Whitespace: Ignored and not included in the output token list.

Single-line Comments: Start with // and extend to the end of the line. These are ignored.

Multi-line Comments: Enclosed between /* and */. These are ignored.

Operators: Include +, -, *, /, ^, and %. Each operator is recognized distinctly.

Assignment: Recognized by the = symbol.

Delimiters: Includes the ; character, used to denote the end of a statement.

User Input: Prefixed with User In:.

Print Command: Recognized by the Print: prefix.

Variables: Identifiers that start with a letter or underscore, followed by any combination of letters, digits, and underscores.

Numbers: Decimal numbers, which may include an integer part followed by a fractional part.

Parentheses: Left ( and right ) parentheses are used for grouping expressions.

# Function Description
tokenize(input_string)

Parameters:
input_string (str): A string containing the source code to be tokenized.

Returns:
List of tuples: Each tuple contains two elements:
Token Type (str): A string label describing the type of token.
Token Value (str): The exact string from the input that matches the token type.

Behavior:
The function iterates over the input string, matching patterns in the order they are specified. When a pattern matches, the function:
If the token type is not None (i.e., not whitespace or a comment), appends a tuple to the result list containing the token type and the matched string.
Advances the position in the input string past the end of the matched token.
If no patterns match the current beginning of the string, a ValueError is raised indicating an invalid token.

![image](https://github.com/HasaanNoor/Compiler-Design-Project/assets/122407889/b1161167-a04b-4185-a5f6-a6a92081af3c)

![image](https://github.com/HasaanNoor/Compiler-Design-Project/assets/122407889/9d781855-73f6-4d41-9b3e-ce0024f19b1b)

# Error Handling

If an unrecognized sequence is encountered in the input string, a ValueError is raised with a message indicating the problematic part of the input.


# Python Expression Parser

# Node Classes

# Node

Description: Base class for all nodes in the AST. This class is abstract and serves as a foundation for specific types of nodes that represent parts of an expression.

Methods:
None explicitly defined; serves as a superclass for type hierarchy and common behaviors.

# Expression(Node)
Description: Represents a binary expression, which includes an operator and two operand expressions.

Attributes:

left: The left-hand operand (Node).
operator: The operator (str) as a string symbol.
right: The right-hand operand (Node), optional if the operator is not present.

Methods:
__str__(): Returns a string representation of the expression, which recursively includes the string representations of the operands and the operator.

# Number(Node)
Description: Represents a numeric literal in an expression.

Attributes:
value: The numeric value (str) of the number.

Methods:
__str__(): Returns the string representation of the number.

# Variable(Node)

Description: Represents a variable identifier in an expression.

Attributes:
identifier: The name (str) of the variable.

Methods:
__str__(): Returns the identifier of the variable as its string representation.

# Parser Class

# Parser

Description: Handles parsing of a list of tokens into an AST based on a simplified set of grammar rules for arithmetic expressions.

Attributes:
tokens: A list of tuples where each tuple represents a token in the form (token_type, token_value).
current: The current position (int) in the token list that the parser is processing.

Methods:
eat(token_type): Consumes the current token if it matches the expected token_type, otherwise raises an exception.
parse(): Starts the parsing process and returns the root of the AST.
expression(): Parses expressions involving addition and subtraction.
term(): Parses expressions involving multiplication and division.
factor(): Handles parsing of numbers, variables, and nested expressions.

Error Handling:
Throws exceptions with messages indicating mismatches between expected and actual tokens, facilitating debugging of syntax errors.
Parsing Process
The parser operates by recursive descent, translating a flat list of tokens into a nested tree structure that reflects the precedence and associativity of arithmetic operators. The parsing methods (expression, term, and factor) represent different levels of precedence in the grammar.



