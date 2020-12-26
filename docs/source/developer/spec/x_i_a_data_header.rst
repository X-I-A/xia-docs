X-I-A Data Header Protocol
==========================

Introduction
------------
Specification Number: XIA-001

Scope
-----
The protocol describes standard data header specification of Xeed -> Insight -> Agent flow.

key: source_id
--------------
Source Table Name
    * Format: <level_1>.<level_2>.<level_3>.<level_4>. Examples
        * Database use case: level 1, 2, 3, 4 could be system id, database name, schema name and table name
        * Email use case: level 1, 2, 3, 4 could be username('.' escaped), domain name('.' escaped), subject name, attachment name

key: topic_id
-------------
Topic Name
  * Format: Any


key: table_id
-------------
  * Description: Target Table Name
  * Same format as source_id



