

# Lexical Parser & Syntax Analyzer
This repository contains a lexical parser and syntax analyzer for a fictional programming language called "Rat18."

In its current implementation, the parser takes a file containing Rat18 code as input and outputs a token-by-token analysis of the code. This analysis includes each token's lexical classification and corresponding grammar rule(s). 

The syntax analyser uses a Recursive Descent method to analyse tokens.

This was the final project for Cal State Fullerton's CSPC323 ("Compilers and Languages") course, Spring 2019.

### How to run
```bash
	python3 parser.py <input file> <output file>
```
###
## Rat18 Grammar Rules
```xml
<Statement> -> <If-statement> | <While-loop> | <Declaration> | <Assignment>
<Declaration> -> <Data-Type> <Assignment>
<Assignment> -> <Identifier> = <Expression>;
<Data-Type> -> int | boolean | float
 
<If-statement> -> if <conditional> then <Statement> <Else>
<Else> -> else <Statement> | epsilon

<Conditional> -> <Expression> <Conditional-Operator> <Expression>
<Conditional-Operator> -> "=" | "<" | ">"
 
<While-loop> -> while <conditional> <statement> whileend
 
<Expression> -> <Term> <Expression-Prime>
<Expression-Prime> -> + <Term> <Expression-Prime> | - <Term> <Expression-Prime> | epsilon
<Term> -> <Factor> -> <Term-Prime>
<Term-Prime> -> * <Factor> <Term-Prime> | / <Factor> <Term-Prime> | epislon
<Factor> -> (<Expression>) | <Identifier> | <Integer> | <Float> | <Boolean>

<Identifer> -> (Aa-Zz)(Aa-Zz0-9$)*
<Integer> -> (0-9)+
<Float> -> (0-9)+.(0-9)+
<Boolean> -> true | True | false | False
```

## Example
#### Input
```
int x=4;
float y=1.5;
 
while y=1.5
    if x=3 then 
        y=y+1;
whileend
```
###
###
#### Output
```xml
Lexeme: int  Token: KEYWORD
<Statement> -> <Declaration>
<Declaration> -> <Data-Type> <Assignment>
Lexeme: x  Token: IDENTIFIER
<Assignment> -> <Identifier> = <Expression>;
Lexeme: =  Token: OPERATOR
<Expression> -> <Term> <Expression-Prime>
<Term> -> <Factor> <Term-Prime>
Lexeme: 4  Token: INTEGER
<Factor> -> <Integer>
<Term-Prime> -> epsilon
<Expression-Prime> -> epsilon
Lexeme: ;  Token: SEPERATOR
Lexeme: float  Token: KEYWORD
<Statement> -> <Declaration>
<Declaration> -> <Data-Type> <Assignment>
Lexeme: y  Token: IDENTIFIER
<Assignment> -> <Identifier> = <Expression>;
Lexeme: =  Token: OPERATOR
<Expression> -> <Term> <Expression-Prime>
<Term> -> <Factor> <Term-Prime>
Lexeme: 1.5  Token: REAL
<Factor> -> <Float>
<Term-Prime> -> epsilon
<Expression-Prime> -> epsilon
Lexeme: ;  Token: SEPERATOR
Lexeme: while  Token: KEYWORD
<Statement> -> <While-Loop>
<While-Loop> -> while <Conditional> <Statement> whileend
<Conditional> -> <Expression> <Conditional-Operator> <Expression>
<Expression> -> <Term> <Expression-Prime>
<Term> -> <Factor> <Term-Prime>
Lexeme: y  Token: IDENTIFIER
<Factor> -> <Identifier>
<Term-Prime> -> epsilon
<Expression-Prime> -> epsilon
Lexeme: =  Token: OPERATOR
<Expression> -> <Term> <Expression-Prime>
<Term> -> <Factor> <Term-Prime>
Lexeme: 1.5  Token: REAL
<Factor> -> <Float>
<Term-Prime> -> epsilon
<Expression-Prime> -> epsilon
Lexeme: if  Token: KEYWORD
<Statement> -> <If-Statement>
<If-Statement> -> if <Conditional> then <Statement> <Else>
<Conditional> -> <Expression> <Conditional-Operator> <Expression>
<Expression> -> <Term> <Expression-Prime>
<Term> -> <Factor> <Term-Prime>
Lexeme: x  Token: IDENTIFIER
<Factor> -> <Identifier>
<Term-Prime> -> epsilon
<Expression-Prime> -> epsilon
Lexeme: =  Token: OPERATOR
<Expression> -> <Term> <Expression-Prime>
<Term> -> <Factor> <Term-Prime>
Lexeme: 3  Token: INTEGER
<Factor> -> <Integer>
<Term-Prime> -> epsilon
<Expression-Prime> -> epsilon
Lexeme: then  Token: KEYWORD
Lexeme: y  Token: IDENTIFIER
<Statement> -> <Assignment>
<Assignment> -> <Identifier> = <Expression>;
Lexeme: =  Token: OPERATOR
<Expression> -> <Term> <Expression-Prime>
<Term> -> <Factor> <Term-Prime>
Lexeme: y  Token: IDENTIFIER
<Factor> -> <Identifier>
<Term-Prime> -> epsilon
Lexeme: +  Token: OPERATOR
<Expression-Prime> -> + <Term> <Expression-Prime>
<Term> -> <Factor> <Term-Prime>
Lexeme: 1  Token: INTEGER
<Factor> -> <Integer>
<Term-Prime> -> epsilon
<Expression-Prime> -> epsilon
Lexeme: ;  Token: SEPERATOR
<Else> -> epsilon
Error: While loop missing closing "whileend".
Lexeme: $  Token: END_OF_FILE

```

> 
> Written with [StackEdit](https://stackedit.io/).

