# Golang Rules Engine  [![Build Status][ci-img]][ci] [![codecov](https://codecov.io/gh/nikunjy/rules/branch/master/graph/badge.svg)](https://codecov.io/gh/nikunjy/rules)
Rules engine written in golang with the help of antlr.

This package will be very helpful in situations where you have a generic rule and want to verify if your values (specified using `map[string]interface{}`) satisfy the rule. 


Here are some examples:

```
  type obj map[string]interface{}
  
  parser.Evaluate("x eq 1", obj{"x": 1})
  parser.Evaluate("x == 1", obj{"x": 1})
  parser.Evaluate("x lt 1", obj{"x": 1})
  parser.Evaluate("x < 1", obj{"x": 1})
  parser.Evaluate("x gt 1", obj{"x": 1})
  
  parser.Evaluate("x.a == 1 and x.b.c <= 2", obj{
    "x": obj{
       "a": 1,
       "b": obj{
          "c": 2,
       },
    },
  })
  

  parser.Evaluate("y == 4 and (x > 1)", obj{"x": 1})

  parser.Evaluate("y == 4 and (x IN [1,2,3])", obj{"x": 1})

  parser.Evaluate("y == 4 and (x eq 1.2.3)", obj{"x": "1.2.3"})
  
```

## Operations
All the operations can be written capitalized or lowercase (ex: `eq` or `EQ` can be used)

Logical Operations supported are `AND OR`

Compare Expression and their definitions (a|b means you can use either one of the two a or b):
```
eq|==: equals to 
ne|!=: not equals to
lt|<: less than 
gt|>: greater than
le|<=: less than equal to
ge|>=: greater than equal to 
co: contains 
sw: starts with 
ew: ends with
in: in a list
pr: present
not: not of a logical expression
```

## How to use it 
Use your dependency manager to import `github.com/nikunjy/rules/parser`. This will let you parse a rule and keep the parsed representation around. 
Alternatively, you can also use `github.com/nikunjy/rules` directly to call the root `Evaluate(string, map[string]interface{})` method. 

I would recommend importing `github.com/nikunjy/rules/parser` 

[ci-img]: https://api.travis-ci.org/nikunjy/rules.svg?branch=master
[ci]: https://travis-ci.org/nikunjy/rules
