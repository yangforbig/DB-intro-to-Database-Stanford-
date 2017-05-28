# DB-intro-to-Database-Stanford
Study note for the course Introduction to Database from Stanford


1. Introduction 

Charateristics of Database

(1) Massive,  terabytes

(2) Persistent,

(3) Safe, 

(4) Multi-user, concrurrency control

(5) Convenient, 

(6) Efficient

(7) Reliable 

Key concepts 

 - data model
 set of records(relational database), XML, graph, JASN
 
 - schema(types) versus data
 schema: structure of data
 
 - Data definition language (DTD
 
 
 - Data manipulation or query language(DML)
 querying and modifying 

Key people 

- DBMS implementer
 Builds system

- Database designer
 establish the schema
 
 - Database application developer
  progroms that operate on database
  
 - database administrator 
  Loads data, keep running smoothly
  
  
  2. Relational database
  (1) The relation model
  
  a set of named relations( or tables)
  
  Each relation has a set of named attributes ( or columns)
  
  Each tuple (or row) has value for each attribute
  
  Each attribute has a type (or domain)
  
  Schema: stuctural description of relation
  
  instance: actual content at given point in time
  
  NULL: undefined or unknown
  
  key: attribute whose value is unique in each tuple or set of attributes whose combined values are unique 
  
  Create relation:
  
  CREATE TABLE STUDENT (ID, NAME, GPA, PICTURE)
  
  (2) Querying Relational Database
  
  - relational Algrebra
  
  - SQL
  
  3. XML data
  
  XML: extensible markup language
  
- standard for data representation and exchange

- Document format similar to HTML

  Tags describe content instead of formatting 
  
- Steaming format

1. Well-Formed XML

- Tagged elements

- Attributes

- Text

|                  | Relational                        | XML              |
 ----------------- | ---------------------------- | ------------------
| Structure | Tables          | Hierarchical|
| Schema           | Fixed in advance           | Flexible, "self-describing" |
| Queries           |Simple, nice, long|Less so |
| Ordering           | No| implied |
|Implementation       |Native|add-on |

2. DTDs, IDs, and IDREFs

"Valid" XML
Adheres to basic structural requirements
 Also adheres to contents-specific specification
 Document Type Descripor(DTD)
 XMLSchema(XSD)
 
 XML document --->  XML Parser----> Parsed XML
                        |
                     Not well-formed 
                    
                      DTD or XSD
 
 XML document --->  Validing XML Parser----> Parsed XML
                        |
                     Not well-formed 


**DTD**: 

- Grammar-like language for specifying elements, attributes, nesting, ordering  
- Also special attribute types ID and IDREF(s)

Positive: programs can assume struture
CSS/XSL ,
Negative: flexibility, ease of change

ID is globally uniquely identified

XML scheme:
- extensive language
- Like DTDs, can specify elements, attributes, nesting, ordering, occurences
- Also data types, keys, typed(pointer)
- XSD is written in XML

in DTD all attributes are treated as strings

in XSD the type of attributes can be specified 

in XSD reference key can be set

in XSD the occurences can be specified (minOccurs, maxOccurs) default is 1

XML QUIZ: 

Well-formed XML must follow these rules (along with others):

(1) There must be exactly one top level element.

(2) All opening tags must be closed.

(3) All elements are properly nested i.e., there are no interleaved elements.

(4) Attribute values must be enclosed in single or double quotes.

The correct choices (i.e., the erroneous DTD snippets) are based on two rules:

(1) A #REQUIRED attribute must appear in every element.

(2) An attribute can have types CDATA, ID, or IDREF(S), but not #PCDATA.

JASON

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

JASN Schema: mechanism for enforcing certain constraints beyond simple syntatic correctness

JASO allows to have additional attributes that are described in JASN.



SQL

-DDL
create table
drop table

-DML
select
insert
delete
update

- Other Commands
indexes, constraints, views, triggers, transactions, authorization, 

as: change the attribute name 

select s1.sID, s1.sName, s1.GPA, s2.sID, s2.sName, s2.GPA
from student s1, student s2
where s1.GPA = s2.GPA and s1.sID <> s2.sID

Union, intercet, except
Union in sql by default eliminates duplicates in its results

subquery can eliminate duplicates

select sID, sName
from Student
where sID in (select sID from Apply where major = 'CS')
and sID not in (select sID from Apply where major != 'EE')

find the largest or smallest 
select sName, GPA
from Student C!
where not exists( select * from student C2
                  where C2.GPA > C!.GPA
                  
select sName, GPA
from Student 
where GPA >= all (select GPA from student);

select cName
from college S1
where not enrolloment < any (select enrollment from college S2
                              where S2.cName <> S1.cName
                              
not .. = .. is not equal to <>

any, one or more 
It turns out we can always write a query that would use any or all by using the exists operator or not exists instead




Basic 











