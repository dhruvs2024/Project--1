# Project--1(In-Memory Database)
### My Experience While Working on the Project

While doing this project, I had to study topics like linked lists, file I/O operations, dynamic memory allocation, structs and typedef. and one of the most troubling problem throughout this was the linked lists as it was completely new to me.  While writing the code the main problem i faced was the gets() one as it randomly gave segmentation faults(it you enter more than memory allotted to it, it takes the input but shows segmentation fault as so space is there to store it) so I rather used scanf and used "%8s" which only takes the first 8 characters of the index and 2nd was none other than linked lists as it was very new concept to me(had many logical confusions) then i slowly solved them as I continued through the code. and it was a nice experience doing my first project.

### How the project works.

set command adds the record to the DBMS with key and the value.<br>
get function gets the value associated with that particular key.<br>
Delete function deletes the record associated with that particular key.<br>
Exists checks whether the record exists with such key.<br>
Save function saves the data which was temporarily stored in volatile memory(RAM) in a file(Takes the name of file in which data is to be stored).<br>
Load function extracts the data from a file and then stores it into the volatile memory of the computer(RAM).<br>
