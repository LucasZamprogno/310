# "EBNF"
```
QUERY_STRING ::= DATASET + ', ' + FILTER + '; ' + DISPLAY(+ '; ' + ORDER)? + '.'

DATASET ::= 'in ' + TYPE + ' dataset ' + INPUT
FILTER  ::= 'find all entries' || 'find entries whose ' + CRITERIA) || (CRITERIA + (' and '/' or ') + CRITERIA)
DISPLAY ::= 'show ' + KEY + ((', ' + KEY )? + ' and ' + KEY)? 
ORDER   ::= 'sort ' + ('up ' || 'down ')? + 'by ' + KEY + ((', ' + KEY )? + ' and ' + KEY)?

CRITERIA   ::= M_CRITERIA || S_CRITERIA
M_CRITERIA ::= M_KEY + M_OP + INPUT
S_CRITERIA ::= S_KEY + S_OP + INPUT

INPUT ::= string of one or more characters. Cannot contain RESERVED as a substring
RESERVED ::= KEYWORD || M_OP || S_OP || AGGREGATOR || TYPE
KEYWORD ::= 'in' || 'dataset' || 'find' || 'all' || 'show' || 'and' || 'or' || 'sort' || 'by' || 'entries' || 'grouped' || 'where' || 'is' || 'the' || 'of' || 'whose'

M_OP ::= 'is '(+ 'not ' +)? + ('greater than ' || 'less than ' || 'equal to ') + KEY
S_OP ::= ('includes || 'does not include') || ('begins' || 'does not begin' || 'ends' || 'does not end') + ' with ' + KEY
AGGREGATOR ::= 'MAX' || 'MIN' || 'AVG' || 'SUM'
TYPE ::= 'courses' || 'rooms'

KEY ::= M_KEY || S_KEY
M_KEY ::= 'average' || 'passed' || 'failed' || 'audited' || 'latitude' || 'longitude' || 'seats' 
S_KEY ::= 'department' || 'id' || 'instructor' || 'title' || 'uuid' || 'fullname' || 'shortname' || 'number' || 'name' || 'address' || 'type' || 'furniture' || 'link' || 

// Added up and down to keywords, ORDER
// Assuming no case sensitivity
// Doesn't encode that KEY must match associated dataset
// I would like the Oxford comma for ((', ' + KEY )? + ' and ' + KEY) :P
```
