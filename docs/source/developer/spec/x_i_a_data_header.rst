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
    * When the value is empty, source_id takes the value of table_id

key: topic_id
-------------
Topic Name
    * Format: Any


key: table_id
-------------
Target Table Name
    * Same format as source_id
    * When the value is empty, source_id takes the value of table_id

key: start_seq
--------------
Data history id.
    * Format: length 20 string with python time format '%Y%m%d%H%M%S%f'
    * If two data header with the same source_id + start_seq means the same data source.
    * Not presents in the case of Strong Data Consistency data fields

key: age
--------
Data sequence within a single history ID
    * Format: Integer
    * If age is equal to 1 means the data body contains table header information
    * age > 2 only presents in the case of Strong Data Consistency

key: end_age
------------
End of age of the message (when not set, end_age is considered equal to age)

key: aged
---------
True = Strong Data Consistency / False = Weak Data Consistency

key: data_store
---------------
Data store type
    * `body`: means the data is in the data body.
    * Other value needs a Storer Module to read the data

key: data_encode
----------------
Data encode type
    * `gzip` : gzipped byte array
    * `b64g` : base64-encoded gzipped char array
    * `flat` : plein-text
    * `blob` : binary data
    * Other value needs a Decoder Module to decoder the data (**Xeed service ONLY**).

key: data_format
----------------
Data format
    * `record` : json - list of dictionary
    * Other value needs a Formatter Module to format the data (**Xeed service ONLY**).

key: data_spec
--------------
Data specification
    * `x-i-a` : x-i-a data specification
    * Other value needs a Translator Module to translate the data (**Xeed service ONLY**).

Definition: Strong Data Consistency
-----------------------------------
Data sequence is defined by age field. A consistency data history couldn't has an age gap

Definition: Weak Data Consistency
---------------------------------
Data sequence is defined by start_seq field. Data update sequence is not very important. Typical use cases:
    * Append only dataset
    * Data has already a field to control the sequence
