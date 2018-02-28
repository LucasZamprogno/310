# "EBNF"
```
QUERY  ::= QUERY_NORMAL || QUERY_AGGREGATE

FILTER ::= 'find all entries' || 'find entries whose ' + (CRITERIA || (CRITERIA + ((' and ' || ' or ') + CRITERIA)*)

QUERY_NORMAL ::= DATASET + ', ' + FILTER + '; ' + DISPLAY(+ '; ' + ORDER)? + '.'
DATASET      ::= 'in ' + TYPE + ' dataset ' + INPUT
DISPLAY      ::= 'show ' + KEY (+ MORE_KEYS)?
ORDER        ::= 'sort ' + ('up ' || 'down ')? + 'by ' + KEY (+ MORE_KEYS)?

QUERY_AGGREGATE ::= DATASET_GROUPED + ', ' + FILTER + '; ' + DISPLAY_GROUPED(+ '; ' + ORDER_GROUPED)? + '.'
DATASET_GROUPED ::= DATASET + ' grouped by ' + KEY (+ MORE_KEYS)?
DISPLAY_GROUPED ::= 'show ' + KEY_C (+ MORE_KEYS_C)? + (', ' + AGGREGATION)?  
ORDER_GROUPED   ::= 'sort ' + (('up ' || 'down ') +)? 'by ' + KEY_C (+ MORE_KEYS_C)?
AGGREGATION     ::= 'where ' + AGG_DEF (+ MORE_DEFS)*

AGG_DEF    ::= INPUT + ' is the ' + AGGREGATOR + ' of ' + KEY
MORE_RULES ::= ((', ' + AGG_DEF +)* ' and ' + AGG_DEF)
AGGREGATOR ::= 'MAX' || 'MIN' || 'AVG' || 'SUM'

CRITERIA   ::= M_CRITERIA || S_CRITERIA
M_CRITERIA ::= M_KEY + M_OP + INPUT
S_CRITERIA ::= S_KEY + S_OP + INPUT

INPUT    ::= string of one or more characters. Cannot contain RESERVED as a substring
RESERVED ::= KEYWORD || M_OP || S_OP || AGGREGATOR || TYPE
KEYWORD  ::= 'in' || 'dataset' || 'find' || 'all' || 'show' || 'and' || 'or' || 'sort' || 'by' || 'entries' || 'grouped' || 'where' || 'is' || 'the' || 'of' || 'whose'
M_OP     ::= 'is ' + ('not ' +)? ('greater than ' || 'less than ' || 'equal to ') + KEY
S_OP     ::= (('includes ' || 'does not include ') || ('begins' || 'does not begin' || 'ends' || 'does not end') + ' with ')) + KEY
TYPE     ::= 'courses' || 'rooms'

KEY   ::= M_KEY || S_KEY
KEY_C ::= KEY || INPUT
MORE_KEYS   ::= ((', ' + KEY +)* ' and ' + KEY)
MORE_KEYS_C ::= ((', ' + KEY_C +)* ' and ' + KEY_C) 
M_KEY ::= 'average' || 'passed' || 'failed' || 'audited' || 'latitude' || 'longitude' || 'seats' 
S_KEY ::= 'department' || 'id' || 'instructor' || 'title' || 'uuid' || 'full name' || 'short name' || 'number' || 'name' || 'address' || 'type' || 'furniture' || 'link' || 

// '_C' is for 'custom'
// Using + for concatenation
// * is 0 or more
// Added past tense to pass, fail, audit (personal opinion: sounds better in natural language)
// Added 'up' and 'down' to KEYWORD and ORDER to match D2 (not present in examples I saw)
// Added 'or' KETWORD and FILTER to match old spec (not present in examples I saw)
// Assuming no case sensitivity
// Doesn't encode that KEY must match associated dataset (courses/rooms)
// Doesn't encode that KEY_C in DISPLAY_GROUPED must be specified by INPUT in AGGREGATION
// I would like the Oxford comma for ((', ' + KEY )? + ' and ' + KEY) even though it's not in the examples :P
// Changing to D1 only entails removaling aggregation sections, KEY_C, and MORE_KEYS_C, removingrooms keys from M_KEY and S_KEY, modifying ORDER
```
