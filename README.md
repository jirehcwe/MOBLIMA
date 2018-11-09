# MOBLIMA Project for Object Oriented Design Programming Module

This is a Java project and an introduction into the world of OO programming as a 2nd year computer science student.
This is a console based movie booking app for both administrators and users to view, book and review movies.

### Design Considerations
The 4 Object-oriented programming design (OODP) principles (Inheritance, Abstraction, Encapsulation and Polymorphism) and SOLID principles are used to design our code. 

### Approach
We started with the flow of the programme (What the customer sees, what the Admin sees and the functions). By identifying the “nouns” in the flow of programme, we are able to identify the different classes required. We then move on to identify the different relationships (has-a, whole/part etc.) that links the different classes. Concurrently, we made sure that the links between the classes do not form a network. High cohesion and low coupling are continuously ensured. After drafting the UML Class and UML Sequence diagrams, we applied SOLID principles to further refine the code and checked that the 4 OODP principles have been applied. Lastly, we went through all the code and inserted relevant exception handlings. 

### Assumptions
There will be future plans to modify/expand the code
There is only one admin/user account 
The showtime will be within this year
Age of child: <12 years old
Age of Elderly: >65 years old


# UML Diagrams drawn up for this project

## Main Diagram
![Main UML Diagram](https://github.com/jirehcwe/MOBLIMA/blob/master/UML%20Class%20Diagram%201.jpg "Main UML Diagram")

## Cineplex, Cinema, CinemaShow, Movies and MovieReview modules
![Cinema Submodule](https://github.com/jirehcwe/MOBLIMA/blob/master/UML%20Class%20Diagram%205.png "Cineplex, Cinema, CinemaShow, Movies and MovieReview modules")

## Ticket Modules and subclasses
![Ticket Submodule](https://github.com/jirehcwe/MOBLIMA/blob/master/UML%20Class%20Diagram%204.png "Ticket and subclasses")

## Databases
![Database Submodule](https://github.com/jirehcwe/MOBLIMA/blob/master/UML%20Class%20Diagram%202.png "Databases")

## Menu (Frontfacing and Administrative) Modules
![Menu Submodule](https://github.com/jirehcwe/MOBLIMA/blob/master/UML%20Class%20Diagram%203.png "Menu (Frontfacing and Administrative) Modules")

## OODP Principles
### 1. Inheritance:
In our code, inheritance leads to extensibility, where subclasses MovieNormal, MovieBlockbuster, Movie3D extends from the parent Movie class through the use of is-a relationship. The subclasses override some methods in the Ticket class (such as the getDiscount method) to create more meaningful implementation that is specific to the subclasses (by including their respective ticket discounts based on their movie type). Other methods in the parent class (Movie) such as printAverageRating are common methods used by all the subclasses. By sharing common code amongst several subclasses, it minimizes the amount of duplicate code in our application, which in turn results in better organisation of code with smaller and simpler compilation units. Furthermore, adopting inheritance in our code increases its reusability where the Movie class (containing public methods that are general in purpose) can be used for other purposes without having to rewrite the same code again. 

### 2. Encapsulation:
We achieve encapsulation by hiding certain details in our code that we feel are unnecessary for other classes to know through the use of accessibility modifiers (public, private etc ). Most attributes in the classes created are declared as private. This allows only the class itself to read and alter the value of these attributes (through get/set methods), while other classes do not have access to these attributes. For example, in the Cinema class, attributes such as classOfCinema and cinemaID are declared as private and cannot be directly accessed by other classes such as CustomerModule class. This demonstrates information-hiding since it is not important for CustomerModule to know the details of implementation of cinemaID. This controlled access of information prevents unwanted changes to the data in our code as other classes that do not depend on these private attributes are unable to change or access such data. 

### 3. Abstraction:
We make use of abstract class to make our code more loosely coupled. Movie class is an abstract class since it cannot be instantiated on its own. The subclasses Movie3D, MovieBlockbuster and MovieNormal created override the getDiscount method in the abstract Movie class where each getDiscount method returns their respective discount rates based on their own movie type. The use of abstraction in our code therefore allows sibling classes to be grouped according to similar functionalities. It also provides compile-time safety as it ensures that any classes that extend Movie class will provide the bare minimum functionality to work. Movie class remains as a representation of the subclasses, with unwanted detail (the different discount rates) omitted. 

### 4. Polymorphism: 
We achieve polymorphism by enabling the change of behaviour of our application in run time based on the object on which the invocation happens. For example, all classes that inherits from Ticket class has a calculateTicketPrice function. Each subclasses interprets calculateTicketPrice differently since each subclasses has its own discount. Therefore if there is a need to add more tickets type in the future, one can then code the calculateTicketPrice of that subclass independently without modifying other classes. 

## SOLID Principles

### Single-responsibility Principle:
Multiple classes are created such that each class has only one responsibility. The major classes are: Cineplex, Cinema, Movie, Customer Module, Admin Module and the respective Databases. We grouped the codes based on its purpose and linking each code to necessary classes instead of bunching all of them in the “Main” class. Even for similar functions, we further categorise these codes in different class to maintain the single-responsibility principle (Ticket, TicketDatabase, TicketDiscount). By doing so, we further break down the classes to more specific functions. We did this with the idea of maintenance and extensibility in mind. For any future cases, there will be minimal instances of having to change multiple classes due to the high cohesion. 

### Open-closed principle:
Ticket parent is closed for modification but it is open for extension (AdultTicket, ChildTicket, ElderlyTicket). Each of these class overrides the function calculateTicketPrice. The open-closed principle makes it easier for future extension where there can be a class with a different way of calculateTicketPrice. 

### Liskov Substitution Principle:
In many of our sub-classes we ensure that it does not require more parameters and returns sufficient results such that the sub-classes can be substitutable for its parent class without the calling class knowing it. For example, the getMovieDiscount method in the subclasses (Movie3D, MovieBlockbuster, MovieNormal) over-rides that of the parent class (Movie class) and can be substituted for the parent class’ getMovieDiscount without changing its funcionality as the respective subclasses will still calculate their respective discount values through the getMovieDiscount method. 

### Interface Segregation Principle:
Small interfaces are implemented in our code instead of “fat” interface. This ensures that other classes will be able to choose the interfaces they need instead of being forced to implement interfaces they don’t use. For example, the interface “Database” has one main function that fetches saved data from dat files and writes them into respective ArrayLists in all databases.

### Dependency Injection Principle:
High level modules such as CustomerModule and AdminModule class do not directly write into the databases’ files. They merely call the respective database to fetch or edit the database file. All the work will then be done within the data base classes. For example, to add a review of a particular movie, CustomerModule calls the addReview function in MovieDatabase. The addReview function in MovieDatabase will take care of the process of adding the review. The CustomerModule does not need to know how the addReview function is coded. The higher level modules (AdminModule and CustomerModule) are not dependent on lower level  modules (the Database classes), therefore removing the hard-code dependencies and making the whole application more loosely coupled.
