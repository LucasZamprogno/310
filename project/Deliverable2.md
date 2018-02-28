### EBNF

```
QUERY ::='{'BODY ', ' OPTIONS (', ' TRANSFORMATIONS)? '}'

BODY ::= 'WHERE:{'  (FILTER)? '}'
OPTIONS ::= 'OPTIONS:{' COLUMNS ', ' (SORT)?'}'
TRANSFORMATIONS ::= 'TRANSFORMATIONS: {' GROUP ', ' APPLY '}'

FILTER ::= (LOGICCOMPARISON | MCOMPARISON | SCOMPARISON | NEGATION)

LOGICCOMPARISON ::= LOGIC ':[{' FILTER ('}, {' FILTER )* '}]'  
MCOMPARISON ::= MCOMPARATOR ':{' key ':' number '}'  
SCOMPARISON ::= 'IS:{' key ':' [*]? inputstring [*]? '}'  // inputstring may have option * characters as wildcards
NEGATION ::= 'NOT :{' FILTER '}'

LOGIC ::= 'AND' | 'OR' 
MCOMPARATOR ::= 'LT' | 'GT' | 'EQ' 

COLUMNS ::= 'COLUMNS:[' ((key|applystring) ',')* (key|applystring) ']' 
SORT ::= 'ORDER: ' ('{ dir:'  DIRECTION ', keys: [ ' ORDERKEY (',' ORDERKEY)* ']}') | ORDERKEY 
DIRECTION ::= 'UP' | 'DOWN'  
ORDERKEY ::= key | applystring

GROUP ::= 'GROUP: [' (key ',')* key ']'                                                          
APPLY ::= 'APPLY: [' (APPLYKEY (', ' APPLYKEY )* )? ']'  
APPLYKEY ::= '{' applystring ': {' APPLYTOKEN ':' key '}}'
APPLYTOKEN ::= 'MAX' | 'MIN' | 'AVG' | 'COUNT' | 'SUM'                           

key ::= string '_' string
inputstring ::= [^*]* // zero or more of any character except asterisk.
applystring ::= [^_]+ // one or more of any character except underscore.
```
