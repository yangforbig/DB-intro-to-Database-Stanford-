# DB intro to Database Stanford
*Study note for the course [Introduction to Database from Stanford](https://lagunita.stanford.edu/courses/Engineering/db/2014_1/about)*
*Last updated Jun 7 2016*

##Introduction 

**Charateristics of Database**

(1) Massive,  terabytes

(2) Persistent,

(3) Safe

(4) Multi-user, concrurrency control

(5) Convenient, 

(6) Efficient

(7) Reliable 

**Key concepts**

 - data model
 set of records(relational database), XML, graph, JASN
 
 - schema(types) versus data
 schema: structure of data
 - Data definition language (DTD)
 - Data manipulation or query language(DML)
 querying and modifying 
 
**Key people** 

- DBMS implementer
 Builds system

- Database designer
 establish the schema
 
- Database application developer
  programs that operate on database
  
- database administrator 
  Loads data, keep running smoothly
  

**Relational database**
  
  - The relation model
  
  a set of named relations( or tables)
  
  Each relation has a set of named attributes ( or columns)
  
  Each tuple (or row) has value for each attribute
  
  Each attribute has a type (or domain)
  
  Schema: stuctural description of relation
  
  instance: actual content at given point in time
  
  NULL: undefined or unknown
  
  key: attribute whose value is unique in each tuple or set of attributes whose combined values are unique 
  - Create relation:
  ```
  CREATE TABLE STUDENT (ID, NAME, GPA, PICTURE)
  ```
  
  - Querying Relational Database
  
  (1) relational Algrebra
  
  (2) SQL
  

**XML data**
  
  XML: extensible markup language
  
- standard for data representation and exchange

- Document format similar to HTML

  Tags describe content instead of formatting 
  
- Steaming format

 Well-Formed XML

- Tagged elements

- Attributes

- Text


**Difference between Relational data structure with XML data**


|                  | Relational                        | XML              |
 ----------------- | ---------------------------- | ------------------
| Structure | Tables          | Hierarchical|
| Schema           | Fixed in advance           | Flexible, "self-describing" |
| Queries           |Simple, nice, long|Less so |
| Ordering           | No| implied |
|Implementation       |Native|add-on |
---------------|---------------

1. DTDs, IDs, and IDREFs

"Valid" XML
Adheres to basic structural requirements
 Also adheres to contents-specific specification
 Document Type Descripor(DTD)
 XMLSchema(XSD)

                     
```

 
 XML document --> Validing XML Parser--> Parsed XML
                        |
                        V
                  Not well-formed 
```

**DTD**: 

- Grammar-like language for specifying elements, attributes, nesting, ordering  
- Also special attribute types ID and IDREF(s)

Positive: programs can assume struture. CSS/XSL 
Negative: flexibility, ease of change



XML scheme:
- extensive language
- Like DTDs, can specify elements, attributes, nesting, ordering, occurences
- Also data types, keys, typed(pointer)
- XSD is written in XML

**Notice**:

in DTD all attributes are treated as strings

in XSD the type of attributes can be specified 

in XSD reference key can be set

in XSD the occurences can be specified (minOccurs, maxOccurs) default is 1

ID is globally uniquely identified


Well-formed XML must follow these rules (along with others):

>(1) There must be exactly one top level element.

>(2) All opening tags must be closed.

>(3) All elements are properly nested i.e., there are no interleaved elements.

>(4) Attribute values must be enclosed in single or double quotes.

The correct choices (i.e., the erroneous DTD snippets) are based on two rules:

>(1) A #REQUIRED attribute must appear in every element.

>(2) An attribute can have types CDATA, ID, or IDREF(S), but not #PCDATA.

**JASON**

An alternative model for the semi-structured data

JSON --> JavaScript Object Notation

- standard for "serializing" data objects, usually in files
- Human-readable, useful for data interchange

Basic constructs

(reursive)
- Basic values:
  number, string, boolean, none
- Objects{}
  sets of label-value pairs
- arrays[]
  lists of values
 
|                  | Relational                        | JSON             |
 ----------------- | ---------------------------- | ------------------
| Structure | Tables          | Sets, Arrays(nested)|
| Schema           | Fixed in advance           | self-describing |
| Queries           |Simple, nice, long|programmactically munupulated |
| Ordering           | None| Array |
|Implementation       |Native|coupled with PLS, NOSQL systems |

**JASN Schema: mechanism for enforcing certain constraints beyond simple syntatic correctness**

JASO allows to have additional attributes that are described in JASN.



##SQL

- DDL
create table
drop table

- DML
select
insert
delete
update
- Other Commands
indexes, constraints, views, triggers, transactions, authorization, 

```
Demo: simple college admission database

college(cName, state, enrollment)

student(sID, sName, GPA, sizeHS)

Apply(sID, cName, major, decision)
```

**Subqueies in where clause**

*as: change the attribute name* 
```

select s1.sID, s1.sName, s1.GPA, s2.sID, s2.sName, s2.GPA

from student s1, student s2

where s1.GPA = s2.GPA and s1.sID <> s2.sID

```

**Union, intercet, except**

Union in sql by default eliminates duplicates in its results

subquery can eliminate duplicates
```
#Students who have applied CS major did not apply the EE major

select sID, sName

from Student

where sID in (select sID from Apply where major = 'CS')

and sID not in (select sID from Apply where major != 'EE')

#find the largest or smallest(Without using MAX, MIN)

select sName, GPA

from Student C1

where not exists( select * from student C2
                  where C2.GPA > C1.GPA)


select sName, GPA

from Student 

where GPA >= all (select GPA from student);


select cName

from college S1

where not enrolloment < any (select enrollment from college S2
                             where S2.cName <> S1.cName)
                              
                              
not .. = .. is not equal to <>

```
**any, one or more**

	   It turns out we can always write a query that would use any or all by using the exists operator or not exists instead

**Subqueies in From and Select**

```
select sID, sName, GPA, GPA * (sizeHS/1000.0) as scaleGPA

from student

where abs(GPA * (sizeHS/1000.0) - GPA > 1.0;

select *
from ( sID, sName, GPA, GPA * (sizeHS / 1000.0) as scaleGPA
from student) G
where abs(scaleGPA - GPA) > 1.0;

```

**Aggregation Function **

min,max,sum,avg,count

```
select count(distinct sID)
from Apply
where cName = 'Cornel';

having clause only used in the conjuectino with aggregation 
```

**NULL**

count(distinct ..) will omit the null rows

**Data Modification Statements**

- insert new data(2 methods)
```
1. insert into table 
   values(A1, A2, A3,..,An)
   
2. Insert into table 
   select-statement 
   
```
```
#insert the students who did not apply any college with CMU in CS major

insert into apply
select sID, "Carnegie Mellon", "CS", NULL
from student
where sIN not in (select sID from apply)
```

- Delete exisiting data
```
Delete from table 
where condition 
```
```
# delete colleges with no cs applicants

Delete from college
where cName not in (select cName from Apply where major = 'CS')

```
- updating existing data
```
update table 
set att = expression
where condition
```
```
update Apply 
set decision = 'Y', major = 'economics'
where cName = 'Carneige'

update Student 
set GPA = (select max(GPA) from student)
    sizeHZ = (select min(GPA) from student);

```

**Join Operator**
inner join on condition 
natrual join 
inner join using attribute 
outer join(right, left, full)

```
#Join three tables

select Apply.sID, sName, GPA, Apply.cName enrollment
from (Apply join Student on Apply.sID = Student.sID) join College
on Apply.cName = College.cName

Natural Join automatically equating colomns and then eliminate duplicates. 
Or use Using clause(software engineering standpoint)

comutativity     (A op B) = (B op A)
associativity   (A op B) op C = A op (B op C)
```

##SQL With Statement 

With Recursive 
	R1 as (query-1)
	R2 as (query-2)
	...
<query involving R (and other tables)>


With Recursive 

	R As ( base query
			Union
		   recursive query)
<query involving R (and other tables)>


example 1: find the ancestors of Mary

| parent | child |
---------|--------
|Alice|Carol|
|Bob|Carol|
|Carol|Dave|
|Carol|George|
|Dave|Mary|
|Eve|Mary|
|Mary|Frank|

```
with recursive 
	Ancestor(a, d) as (select parent as a, child as d from ParentOf
					   Union
					   select Ancestor.a, ParentOf.child as d
					   from Ancestor, ParentOf
					   where Ancestor.d = ParentOf.parent)
select a from Ancestor where d = "Mary";

```

example 2: total salary cost of project

--employee--

| id | salary |
---------|--------
|123|100|
|234|90|
|345|80|
|456|70|
|567|60|

--manager--

| mid | eid |
---------|--------
|123|234|
|234|345|
|234|456|
|345|567|

--project--

| mid | mgrID |
------|------
|X|123|
|Y|234|
|Z|456|


Query:
```
with recursive
	Xemps(ID) as (select mgrID as ID from project where name = 'X'
				  union
				  select eid as ID
				  from manager, Xemps
				  where mid = ID)
select sum(salary)
from employee
where id in (select id from Xemps);
```

example 3: find the cheapest way to get B from A

--Flight--

|origin|dest|airline|cost|
-------|----|-------|-----
|A|ORD|United|200|
|ORD|B|American|100|
|A|PHX|Southwest|25|
|PHX|LAS|Southwest|30|
|LAS|CMH|Frontier|60|
|CMH|B|Frontier|60|
|A|B|JetBlue|195|

Query:

```
with recursive
	FromA(dest, total) as
		(select dest, cost as total from flight where orig = 'A'
		 union
		 select flight.dest, total + cost
		 from flight, FromA
		 where flight.orig = FromA.dest)
select * from FromA where dest = 'B';
```

```
with recursive
	ToB(orig, total) as
		(select orig, cost from Flight where dest = 'B'
		union
		select flight.orig, cost+total
		from Flight, ToB
		where Flight.dest = ToB.orig
select * from ToB;
```

What if the there is an infinite loop in the relation, use LIMIT clause or define a flag

**Nonlinear Recursive**

Nonlinear Recursive converge faster(running time log(n)) but hard to implement.
Nonlinear Recursive is not supported in current SQL and Posgres


		









				  
				















