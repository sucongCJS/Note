# keys & attributes
## primary key:
- unique identifier in a table

## secondary key:
- secondary keys are attributes or a combination of attributes that are used to provide an alternative access to the database

## superkey:
- a set of attributes within a talbe whose values can be used to uniquely identify a tuple.

## candidate key:
- a minimal set of attributes necessary to identify a tuple
- also called a minimal superkey

## non-prime attributes
- an attribute that does not occur in any candidate key

## prime attributes
- an attribute that belongs some candicate key

# normal form
## BCNF
- a 3nf table that does not have multiple overlapping candidate keys is guaranteed to be in BCNF,
- Depending on what its functional dependencies are, a 3NF table with two or more overlapping candidate keys may or may not be in BCNF.

## 4NF
### conditions
- A ->> B, for a single value of A,  more than one value of B exist.  
- - BTW: this is called Multi-Valued Dependency, comparing to the Functional Dependency
- Table should have at-least 3 columns.
- For this table with A, B, C columns, B and C should be independent.


# ER
- __The conceptual model__ is concerned with the real world view and understanding of data.
- __The logical model__ is a generalized formal structure in the rules of information science.
- __The physical model__ specifies how this will be executed in s particular DBMS instance.


references:
- [数据库设计概览](https://www.cnblogs.com/ybwang/archive/2012/03/27/2419573.html)
