# Hbnb console

![airbnb_img](https://i.imgur.com/symULZt.png)

[MVP web static](https://kateincoding.github.io/AirBnB_clone/)

The AirBnB clone project starts now until… the end of the first year. The goal of the project is to deploy on your server a simple copy of the AirBnB website.
After 4 months, you will have a complete web application composed by:

* A command interpreter to manipulate data without a visual interface, like in a Shell (perfect for development and debugging)
* A website (the front-end) that shows the final product to everybody: static and dynamic
* A database or files that store data (data = objects)
* An API that provides a communication interface between the front-end and your data (retrieve, create, delete, update them)

![steps](https://i.imgur.com/9WkM9nn.png)

And the final data diagram looks like this:

![data_diagram](https://i.imgur.com/I7VURNR.jpg)

# First step and GOAl of this repository: Write a command interpreter to manage your AirBnB objects.

This is the first step towards building the first full web application: the AirBnB clone. This first step is very important because we will use what we build during this project with all other following projects: HTML/CSS templating, database storage, API, front-end integration…

## What’s a command interpreter?

Do you remember the Shell? It’s exactly the same but limited to a specific use-case. In our case, we want to be able to manage the objects of our project:

* Create a new object (ex: a new User or a new Place)
* Retrieve an object from a file, a database etc…
* Do operations on objects (count, compute stats, etc…)
* Update attributes of an object
* Destroy an object

## Resources
Read or watch:

* cmd module
* packages concept page
* uuid module
* datetime
* unittest module
* args/kwargs
* Python test cheatsheet

## Learning Objectives
* How to create a Python package
* How to create a command interpreter in Python using the cmd module
* What is Unit testing and how to implement it in a large project
* How to serialize and deserialize a Class
* How to write and read a JSON file
* How to manage datetime
* What is an UUID
* What is *args and how to use it
* What is **kwargs and how to use it
* How to handle named arguments in a function

## Execution

The hbnb command interpreter should work like this in interactive mode:

```
$ ./console.py
(hbnb) help

Documented commands (type help <topic>):
========================================
EOF  help  quit

(hbnb) 
(hbnb) 
(hbnb) quit
$
```

But also in non-interactive mode: (like the Shell project in C):

```
$ echo "help" | ./console.py
(hbnb)

Documented commands (type help <topic>):
========================================
EOF  help  quit
(hbnb) 
$
$ cat test_help
help
$
$ cat test_help | ./console.py
(hbnb)

Documented commands (type help <topic>):
========================================
EOF  help  quit
(hbnb) 
$
```

All tests should also pass in non-interactive mode: ``` $ echo "python3 -m unittest discover tests" | bash ```

## Airbnb files structure

##|File|Description
---|---|---
0|[console.py](./console.py)|command interpreter to manage your AirBnB objects: Create a new object (ex: a new User or a new Place) ; Retrieve an; object from a file, a database etc… ; Do operations on objects (count, compute stats, etc…); Update attributes of an object; Destroy an object
1|[models](./models)|directory of all the classes
2|[tests](./tests)|directory of console test and class tests

## 0.Console and how to executes

you can run it writting ```./console.py``` in your terminal and you will enter to the command interpreter like you see in this example, after it you can use the commands allowed for the terminal.

```
guillaume@ubuntu:~/AirBnB$ ./console.py
(hbnb) help

Documented commands (type help <topic>):
========================================
EOF  help  quit

(hbnb) 
(hbnb) help quit
Quit command to exit the program

(hbnb) 
(hbnb) 
(hbnb) quit 
guillaume@ubuntu:~/AirBnB$ 
```

##|Commands|how to use it in the command interpreter|Instance form|Description
---|---|---|---|---
0.0|quit|```quit```||Exit the program
0.1|EOF|```EOF```||Exit the program
0.2|empty line|``` ```||not do nothing
0.3|create|```create <class name>```|| create an instance of the class
0.4|show|```show <class name> <id number>```|```<class name>.show(<id>)```|Prints the string representation of an instance based on the class name and id
0.5|destroy|```destroy <class name> <id number>```|```<class name>.destroy(<id>)```|Deletes an instance based on the class name and id (save the change into the JSON file)
0.6|all|```all``` or ```all <class name>```|```<class name>.all()```|Prints all string representation of all instances based or not on the class name
0.7|update|```update <class name> <id number> <attribute to update> "<new value of attribute>"```|simple form:```<class name>.update(<id>, <attribute name>, <attribute value>)``` update more than 1 attribute(using dictionaries): ```<class name>.update(<id>, <dictionary representation>)```|Updates an instance based on the class name and id by adding or updating attribute (save the change into the JSON file). If there are more commands, the command interpreter will only count the first attribute with its value
0.8|count|```count <class name>```|```<class name>.count()```|retrieve the number of instances of a class

##|Allowed classes
---|---
a|BaseModel|```BaseModel```
b|User|```User```
c|Place|```Place```
d|State|```State```
e|City|```City```
f|Amenity|```Amenity```
g|Review|```Review```
h|User|```User```

#### Examples:

* help:

```
(hbnb) help

Documented commands (type help <topic>):
========================================
EOF  help  quit

```

* quit and EOF: quits

```
(hbnb) quit 
vagrant@ubuntu:~/AirBnB$ 
```

```
(hbnb) quit 
vagrant@ubuntu:~/AirBnB$ 
```

* create:

```
(hbnb) create BaseModel
2dd6ef5c-467c-4f82-9521-a772ea7d84e9
(hbnb) create User
35dd5991-c54f-4e33-a4c4-2be5219cc15e
```

* all:

```
(hbnb) all BaseModel
["[BaseModel] (49faff9a-6318-451f-87b6-910505c55907) {'created_at': datetime.datetime(2017, 10, 2, 3, 10, 25, 903293), 'id': '49faff9a-6318-451f-87b6-910505c55907', 'updated_at': datetime.datetime(2017, 10, 2, 3, 10, 25, 903300)}"]
```

* show:

```
(hbnb) show BaseModel 49faff9a-6318-451f-87b6-910505c55907
[BaseModel] (49faff9a-6318-451f-87b6-910505c55907) {'created_at': datetime.datetime(2017, 10, 2, 3, 10, 25, 903293), 'id': '49faff9a-6318-451f-87b6-910505c55907', 'updated_at': datetime.datetime(2017, 10, 2, 3, 10, 25, 903300)}
```

* destroy:

```
(hbnb) destroy
** class name missing **
```

* update:

```
(hbnb) show BaseModel 49faff9a-6318-451f-87b6-910505c55907
[BaseModel] (49faff9a-6318-451f-87b6-910505c55907) {'created_at': datetime.datetime(2017, 10, 2, 3, 10, 25, 903293), 'id': '49faff9a-6318-451f-87b6-910505c55907', 'updated_at': datetime.datetime(2017, 10, 2, 3, 10, 25, 903300)}
(hbnb) update BaseModel 49faff9a-6318-451f-87b6-910505c55907 first_name "Betty"
(hbnb) show BaseModel 49faff9a-6318-451f-87b6-910505c55907
[BaseModel] (49faff9a-6318-451f-87b6-910505c55907) {'first_name': 'Betty', 'id': '49faff9a-6318-451f-87b6-910505c55907', 'created_at': datetime.datetime(2017, 10, 2, 3, 10, 25, 903293), 'updated_at': datetime.datetime(2017, 10, 2, 3, 11, 3, 49401)}
```

* all or all BaseModel:
```
(hbnb) create User
35dd5991-c54f-4e33-a4c4-2be5219cc15e
(hbnb) create BaseModel
2c181221-b41f-47f9-bf2a-9e7bc53126a1
(hbnb) all BaseModel
["[BaseModel] (2c181221-b41f-47f9-bf2a-9e7bc53126a1) {'id': '2c181221-b41f-47f9-bf2a-9e7bc53126a1', 'created_at': datetime.datetime(2021, 7, 1, 4, 46, 34, 306736), 'updated_at': datetime.datetime(2021, 7, 1, 4, 46, 34, 306804)}", "[User] (35dd5991-c54f-4e33-a4c4-2be5219cc15e) {'id': '35dd5991-c54f-4e33-a4c4-2be5219cc15e', 'created_at': datetime.datetime(2021, 7, 1, 4, 46, 0, 151113), 'updated_at': datetime.datetime(2021, 7, 1, 4, 46, 0, 151209)}"]
(hbnb) all
["[BaseModel] (2c181221-b41f-47f9-bf2a-9e7bc53126a1) {'id': '2c181221-b41f-47f9-bf2a-9e7bc53126a1', 'created_at': datetime.datetime(2021, 7, 1, 4, 46, 34, 306736), 'updated_at': datetime.datetime(2021, 7, 1, 4, 46, 34, 306804)}", "[User] (35dd5991-c54f-4e33-a4c4-2be5219cc15e) {'id': '35dd5991-c54f-4e33-a4c4-2be5219cc15e', 'created_at': datetime.datetime(2021, 7, 1, 4, 46, 0, 151113), 'updated_at': datetime.datetime(2021, 7, 1, 4, 46, 0, 151209)}"]
(hbnb) all User
["[User] (35dd5991-c54f-4e33-a4c4-2be5219cc15e) {'id': '35dd5991-c54f-4e33-a4c4-2be5219cc15e', 'created_at': datetime.datetime(2021, 7, 1, 4, 46, 0, 151113), 'updated_at': datetime.datetime(2021, 7, 1, 4, 46, 0, 151209)}"]
(hbnb) 
```

#### Instance mode:

* `<class name>.all() `:

```
hbnb) User.all()
["[User] (35dd5991-c54f-4e33-a4c4-2be5219cc15e) {'id': '35dd5991-c54f-4e33-a4c4-2be5219cc15e', 'created_at': datetime.datetime(2021, 7, 1, 4, 46, 0, 151113), 'updated_at': datetime.datetime(2021, 7, 1, 4, 46, 0, 151209)}", "[User] (03be30e8-d686-4b4f-bdb0-66180bb76c62) {'id': '03be30e8-d686-4b4f-bdb0-66180bb76c62', 'created_at': datetime.datetime(2021, 7, 1, 4, 48, 2, 274519), 'updated_at': datetime.datetime(2021, 7, 1, 4, 48, 2, 274584)}"]
```

* ```<class name>.count()```:

```
(hbnb) User.count()
2
```

* ```<class name>.show(<id>)```:

```
(hbnb) User.show("35dd5991-c54f-4e33-a4c4-2be5219cc15e")
[User] (35dd5991-c54f-4e33-a4c4-2be5219cc15e) {'id': '35dd5991-c54f-4e33-a4c4-2be5219cc15e', 'created_at': datetime.datetime(2021, 7, 1, 4, 46, 0, 151113), 'updated_at': datetime.datetime(2021, 7, 1, 4, 46, 0, 151209)}
(hbnb) 
```

* ```<class name>.destroy(<id>)```:

```
(hbnb) User.count()
2
(hbnb) User.destroy("35dd5991-c54f-4e33-a4c4-2be5219cc15e")
(hbnb) User.count()
1
(hbnb) 
```

* update

```
(hbnb) User.show("03be30e8-d686-4b4f-bdb0-66180bb76c62")[User] (03be30e8-d686-4b4f-bdb0-66180bb76c62) {'id': '03be30e8-d686-4b4f-bdb0-66180bb76c62', 'created_at': datetime.datetime(2021, 7, 1, 4, 48, 2, 274519), 'updated_at': datetime.datetime(2021, 7, 1, 4, 48, 2, 274584)}
(hbnb) User.update("03be30e8-d686-4b4f-bdb0-66180bb76c62", "first_name", "John")
(hbnb) User.show("03be30e8-d686-4b4f-bdb0-66180bb76c62")[User] (03be30e8-d686-4b4f-bdb0-66180bb76c62) {'updated_at': datetime.datetime(2021, 7, 1, 4, 53, 12, 110537), 'id': '03be30e8-d686-4b4f-bdb0-66180bb76c62', 'first_name': '"John"', 'created_at': datetime.datetime(2021, 7, 1, 4, 48, 2, 274519)}
```

More than one command:

```
(hbnb) User.show("03be30e8-d686-4b4f-bdb0-66180bb76c62")[User] (03be30e8-d686-4b4f-bdb0-66180bb76c62) {'updated_at': datetime.datetime(2021, 7, 1, 4, 53, 12, 110537), 'id': '03be30e8-d686-4b4f-bdb0-66180bb76c62', 'first_name': '"John"', 'created_at': datetime.datetime(2021, 7, 1, 4, 48, 2, 274519)}
(hbnb) User.update("03be30e8-d686-4b4f-bdb0-66180bb76c62", {'first_name': "Goku", "age": 89})
(hbnb) User.show("03be30e8-d686-4b4f-bdb0-66180bb76c62")[User] (03be30e8-d686-4b4f-bdb0-66180bb76c62) {'age': '"89"', 'updated_at': datetime.datetime(2021, 7, 1, 4, 54, 21, 791081), 'id': '03be30e8-d686-4b4f-bdb0-66180bb76c62', 'first_name': '"Goku"', 'created_at': datetime.datetime(2021, 7, 1, 4, 48, 2, 274519)}
```


## 1.Models file Structure

##|File|Description|Recommendations
---|---|---|---
1.0|[engine](./models/engine)|directory of Store first object|The first way you will see here is to save these objects to a file with dictionaries: ```<class 'BaseModel'> -> to_dict() -> <class 'dict'> -> <class 'BaseModel'>```
1.1|[__init__.py](./models/engine/__init__.py)|initialization code for the package|files are required to make Python treat the directories as containing packages; this is done to prevent directories with a common name
1.2|[amenity.py](./models/engine/amenity.py)|Amenity class| Inherits from BaseModel and contains specific public attributes
1.3|[base_model.py](./models/engine/base_model.py)| Base Model class|  Defines all common attributes/methods for other classes sach as id, datetime
1.4|[city.py](./models/engine/city.py)|City Class| Inherits from BaseModel and contains specific public attributes
1.5|[place.py](./models/engine/place.py)|Place Class| Inherits from BaseModel and contains specific public attributes
1.6|[review.py](./models/engine/review.py)|Review Class| Inherits from BaseModel and contains specific public attributes
1.7|[state.py](./models/engine/state.py)|State Class| Inherits from BaseModel and contains specific public attributes
1.8|[user.py](./models/engine/user.py)|User Class| Inherits from BaseModel and contains specific public attributes

### 1.0.Engine structure

Every time that the program is launched, we will save these objects to a file:
In this project, we converted the dictionary representation to a JSON string. JSON is a standard representation of a data structure. With this format, humans can read and all programming languages have a JSON reader and writer.

The flow of serialization-deserialization is:
```
<class 'BaseModel'> -> to_dict() -> <class 'dict'> -> JSON dump -> <class 'str'> -> FILE -> <class 'str'> -> JSON load -> <class 'dict'> -> <class 'BaseModel'>
```

##|File|Description|Recommendations
---|---|---|---
1.0.0|[__init__.py](./models/engine/__init__.py)|initialization code for the package|files are required to make Python treat the directories as containing packages; this is done to prevent directories with a common name
1.0.1|[file_storage.py](./models/engine/file_storage.py)||

## 2.Tests file Structure and how to compile

All files, classes, functions must be tested with unit tests
```
guillaume@ubuntu:~/AirBnB$ python3 -m unittest discover tests
...................................................................................
...................................................................................
.......................
----------------------------------------------------------------------
Ran 189 tests in 13.135s

OK
guillaume@ubuntu:~/AirBnB$
```

Unit tests must also pass in non-interactive mode:

```
guillaume@ubuntu:~/AirBnB$ echo "python3 -m unittest discover tests" | bash
...................................................................................
...................................................................................
.......................
----------------------------------------------------------------------
Ran 189 tests in 13.135s

OK
guillaume@ubuntu:~/AirBnB$
```

##|File|Description
---|---|---
2.0|[test_models](./tests/test_models)|Test of the models class
2.1|[__init__.py](./tests/__init__.py)|initialization code for the package: files are required to make Python treat the directories as containing packages; this is done to prevent directories with a common name
2.2|[test_console.py](./tests/test_console.py)|Test of the console

### 2.0.Test_models structure

##|File|Description
---|---|---
2.0.0|[test_engine](./tests/test_models/test_engine)|Directory where the project tests all the tests for the storage of the program
2.0.1|[__init__.py](./tests/test_models/__init__.py)|initialization code for the package: files are required to make Python treat the directories as containing packages; this is done to prevent directories with a common name
2.0.2|[test_amenity.py](./tests/test_models/test_amenity.py)|Testing Amenity class- Comproving expectect outputs and documentation
2.0.3|[test_base_model.py](./tests/test_models/test_base_model.py)|Testing BaseModel- Comproving expectect outputs and documentation
2.0.4|[test_city.py](./tests/test_models/test_city.py)|Test City Class - Comproving expectect outputs and documentation
2.0.5|[test_place.py](./tests/test_models/test_place.py)|Test place - Comproving expectect outputs and documentation
2.0.6|[test_review.py](./tests/test_models/test_review.py)|Test Review - Comproving expectect outputs and documentation
2.0.7|[test_state.py](./tests/test_models/test_state.py)|Test state - Comproving expectect outputs and documentation
2.0.8|[test_user.py](./tests/test_models/test_user.py)|Test User - Comproving expectect outputs and documentation

#### 2.0.0.Test_engine structure

##|File|Description
---|---|---
2.0.0.0|[__init__.py](./tests/test_models/test_engine/__init__.py)|initialization code for the package: files are required to make Python treat the directories as containing packages; this is done to prevent directories with a common name
2.0.0.1|[test_file_storage.py](./tests/test_models/test_engine/test_file_storage.py)|Test if the process and the allocation is correct(ouput and process)

## Authors:
* Joshua Claudio Enrico |   <img alt="GitHub" width="26px" src="https://raw.githubusercontent.com/github/explore/78df643247d429f6cc873026c0622819ad797942/topics/github/github.png" /> [GitHub](https://github.com/yoyogold-a11) | [Medium](https://joshuaclaudioenrico.medium.com/)
* Katherine Soto | <img alt="GitHub" width="26px" src="https://raw.githubusercontent.com/github/explore/78df643247d429f6cc873026c0622819ad797942/topics/github/github.png" />[GitHub](https://github.com/kateincoding) | [Medium](https://kateincoding.medium.com/)
