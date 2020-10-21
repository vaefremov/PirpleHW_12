# Pirple Homework Assignment #12: Object Oriented Programming

Available on  [GitHub](https://github.com/vaefremov/PirpleHW_12)

---

# General principles

The object-oriented programming (OOP) paradigm is centered around the following three concepts: encapsulation,
inheritance and polymorphism. Basically, their meaning is as follows:

* Encapsulation means that we can hide all the implementation detail inside an object. The internal
state of an object (data) can be accessed only using a set of methods (or, in some langualges like SmallTalk,
by sending _messages_) to objects

* Inheritance expresses is-a relationship between objects. Using inheritance it is possible to
extend the behavior of a base class by re-implementing some methods in an inherited object
 while keeping some code and data of the base class intact

 * Polymorphism, basically, means that we can use inherited objects in place of base objects. 
 That allows us to formulate algorithms in terms of base objects, and then apply it to the 
 inherited objects.

---

 # Example application

As an example of application that can benefit from application of the OOP paradigm we can think of 
a REST server that keeps some large-volume data (e.g. geophysical data related to seismic exploration).
The purpose of this server is to draw some graphics including the data. User (that may be a web or
a desktop application of some sort) may use methods (messages) of the server to draw a picture and
transfer it back to the user side, avoiding transferring large volumes of data to perform drawing on the 
user side. That is, we have kind of graphical editor on the server side, capable of creating pictures
comprised of graphical objects of a number of classes (lines, text elements, points, rectangles,
slices of data) that can be drawn on a canvas. The canvas can be rendered into a picture using some
format (vector, like SVG, or pixel like PNG), the picture can be downloaded to user application and 
displayed.

In terms of implementing the drawing operations, the following user stories can be implemented:

* User creates a new picture. The picture ID is returned.
* User draws a number of graphical elements by providing a set of commands (messages). Each command
specifies type of object to be drawn, its coordinates on the canvas, (possibly) data object that
is represented by the object (e.g. slice of massive data object). The ID of the created object is returned
for every command.
* User requests rendering the picture in some particular format and downloads the resulting picture.

---

# Main classes

The implementation of the application may use the following classes (types of objects):

* Canvas
* Shape - basic object representing anything that can be drawn on the canvas
* Point
* Line
* Rectangle
* Text
* DataSlice - object inheriting from Rectangle, represents picture of a given data slice

---

# Pseudo-code

    class Canvas {
        private List<Shape> elements;
        public draw(Shape s) {
            for el in elements:
            el.draw(this);
        }
    };


    class Shape {
        private [int x, int y] coordinates;
        public draw(Canvas c){
            // Implementation of drawing a point on canvas
        } 
    };

    class Point inherit Shape;

    class Line inherit Shape;

    class Rectangle inherit Shape {
        private [int x, int y] lowerRightPoint;
        public draw(Canvas c);
    }

    class Text {
        private String text;
        constructor Text(String t); // Assigns text to the argument
        public draw(Canvas c);
    }

    class DataSlice inherits Rectangle {
        private SliceParameters sliceParams;
        constructor DataSlice(DataObjectID dataID, SliceParameters p);
        public draw(Canvas c);
    }

