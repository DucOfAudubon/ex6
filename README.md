# Exercise 6 - Abstract classes and interfaces

## Learning Goals

This exercise targets the understanding of the following subjects:
* To design and use abstract classes (13.2).
* To specify common behavior for objects using interfaces (13.5).
* To define interfaces and define classes that implement interfaces (13.5).
* To define a natural order using the Comparable interface (13.6).
* To make objects cloneable using the Cloneable interface (13.7).
* To explore the similarities and differences among concrete classes, abstract classes, and interfaces (13.8).
* To design classes that follow the class-design guidelines (13.10).

## Description

In this exercise, we will implement a simple Paint program which paints to screen. The user can create simple panels and add several shapes to them. The shapes can be manipulated. You can create panels and add to them other panels and shapes. Then, you can ask a panel to print to screen a specific line.

## Example

The following code:

```
public static void main(String[] args) {
    Painter p = new Painter();
    try {
      p.init();
      p.printToScreen();
    } catch (NodeOverflow no) {
      System.err.println("Elements overflow from painter");
    }
 }

private void init() throws NodeOverflow {
    pane = new Panel(20,30);
    Panel pane2 = new Panel(10,20);
    pane.add(new TShape(3,5));
    pane2.add(new TShape(8,7));
    pane2.add(new LShape(5,3));
    pane.add(pane2);
}
```

Should print to screen

```
------------------------------
|***** --------------------  |
|  *   |******* *         |  |
|  *   |   *    *         |  |
|      |   *    *         |  |
|      |   *    *         |  |
|      |   *    ***       |  |
|      |   *              |  |
|      |   *              |  |
|      |   *              |  |
|      --------------------  |
|                            |
|                            |
|                            |
|                            |
|                            |
|                            |
|                            |
|                            |
------------------------------
```

## Instructions

* Create a package `aup.cs.paint` and a class `Painter` containing a main method which calls an `init` and `printToScreen` methods on a `Painter` instance. The `Painter` should also contain one `Panel`  datafield.
* The classes we need are `Node`, `Panel`, `Shape`, `TShape`, `LShape` and `IShape`.  We also need an exception `NodeOverflow`.
* `Panel` has dimensions (`height` and `width`) as well as an `ArrayList` for holding objects of type `Node` (`Shape`s or `Panel`s).
* All `Shape`s inherit from `Shape` and have `height` and `width`
* A node has a method `printLine(int line)` which prints to screen 1 line of the node (panel or shape)
* The `Painter.printToScreen` should iterate over the `height` of its `Panel` and print each line of it on a new line using the `printLine` method.
* The `Panel` should implement the `printLine` method to print borders `|` on the sides and `-` on the top and bottom (see example) as well as use the `printLine` methods of the nodes it contains. There should be space between each two elements.
* The shapes are printed using the `*` symbol (see example).
* What is the inheritance structure which makes most sense here? Implement the full hierarchy while making sure to use concrete and abstract classes correctly.
* `Panel`s also have an `add` method which adds new `Node`s to the panel. It should throw a `NodeOverflow` exception when the total width of the contained nodes plus the borders and spaces exceeds the width of the panel.
* The `TShape` shape creates a `T` of the specified width and height. Its constructor should throw a `ShapeIllegalArgumentException` if the width argument is smaller than 3 or is not odd or if the height is smaller than 2. Use meaningful exception messages.
* The `LShape` shape creates an `L` of the specified width and height. Its constructor should throw a `ShapeIllegalArgumentException` if the width argument is smaller than 2 or if the height is smaller than 2. Use meaningful exception messages.
* The `IShape` shape creates a `I` of the specified width and height. Its constructor should throw a `ShapeIllegalArgumentException` if the width argument is smaller than 3 or is not odd or if the height is smaller than 2. Use meaningful exception messages.
* Rememebr to not repeat code! For example, implement in `Node` protected methods for printing the different symbols and spaces and call these methods in the different nodes when printing them (i.e. `System.out.print` should be called only in these protected methods).
* Add a `sort` functionality to panels which will sort its (`Comparable`) nodes as following: if a `Shape` is compared to another `Shape`, or a `Panel` to another `Panel`, the one with a smaller height will be placed first.  When a panel is compared to a `Shape`, the `Shape` is always placed first. Make sure to sort nested panels as well!
* Make all Nodes `cloneable`. What is the advantage?
