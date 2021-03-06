Docs
----

- General/FAQ: https://github.com/antlr/antlr4/blob/master/doc/faq/general.md
- Index: https://github.com/antlr/antlr4/blob/master/doc/index.md
- Doc directory: https://github.com/antlr/antlr4/tree/master/doc

Listener

- https://github.com/antlr/antlr4/blob/master/doc/listeners.md
- usage example: Extract Java interface: https://media.pragprog.com/titles/tpantlr2/listener.pdf

Visitor

- https://docs.google.com/presentation/d/1XS_VIdicCQVonPK6AGYkWTp-3VeHfGuD2l8yNMpAfuQ/edit

Book

- The Definitive ANTLR 4 Reference

other example

- https://github.com/bkiers/tiny-language-antlr4

  - two visitor: https://github.com/bkiers/tiny-language-antlr4/blob/master/src/main/java/tl/antlr4/Main.java

Note
----
1. ANTLR4 can use grammer to generate Lexer+Parser, so it can transform Source code into AST(Abstract Syntax Tree).
2. ANTLR4 provide 2 interface to manipulate AST: Listener, Visitor

  - Listener: enter/exit non-terminal node, visit terminal node
  - Visitor: visit terminal and non-terminal node
  - parameter of handler: AST node(non-terminal node or terminal node)
  - we can inheritance ``BaseListener``, and ``BaseVisitor`` to use these interface

3. ANTLR4 basic flow

  - ``InputStream(stdin,file)  --(Lexer)-->  TokenStream  --(Parser)-->  AST + TokenStream``
  - Listener: ``ParseTreeWalker.walk(AST, Listener)``
  - Visitor: ``Visitor.visit(AST)``

4. ANTLR4 dependency

  - ``Grammar File --(ANTLR4)--> Lexer + Parser + Listener + Visitor``

    - e.g. ``Java.g4 --(antlr4 --visitor)--> Java{Lexer,Parser,BaseListener,Listener,BaseVisitor,Visitor}``

5. AST-related structure

  - RuleNode(non-terminal): ``<Rule>Context``, all ``<Rule>Context`` inherit ``ParserRuleContext``
  - TerminalNode
  - TokenStream
  - CharStream

6. AST API

  - Node.getText(): get text of interval nodes, including the node and all children of it. (subtree)

    - TerminalNode and RuleNode(non-terminal) both use this API.
  
  - RuleNode
    
    - <Name in lowerCamel>(): get AST child node <Name>. If there are multiple <Name>, they will be a single ArrayList.
    - getChild(int num): get the <num>th child node of AST.
    - getChildCount(): get the number of AST child node.
    - For more detail, see JavaParser.java generated by ANTLR4.

