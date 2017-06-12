# antlr4-webpack-loader

Loads an ANTLR4 grammar file (`.g4`) and compiles it to JavaScript.

```js
import {
  MyGrammarLexer,
  MyGrammarParser,
  MyGrammarListener,
  MyGrammarVisitor
} from './MyGrammar.g4';
```

## Configuration

Add the ANTLR4 JavaScript runtime as a dependency: `npm install --save antlr4`.

Configure `webpack.config.js` by adding `antlr4-webpack-loader`:

```js
module.exports = {
  module: {
    rules: [
      { test: /\.g4/, loader: 'antlr4-webpack-loader' }
    ]
  }
};
```

## Usage

A grammar file named `MyGrammar.g4` with a rule named `myStartRule` can be loaded in used in the following way:

```js
import { InputStream, CommonTokenStream } from 'antlr4/index';
import { MyGrammarLexer, MyGrammarParser, MyGrammarVisitor } from './MyGrammar.g4';

class MyVisitor extends MyGrammarVisitor {

  visitMyStartRule(ctx) { ... }

  ...
}

const input = ...; // Load string content
const lexer = new MyGrammarLexer(new InputStream(input));
const parser = new MyGrammarParser(new CommonTokenStream(lexer));
const result = new MyVisitor().visit(parser.myStartRule());
```
