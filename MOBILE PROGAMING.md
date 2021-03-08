# odieq
2. Create a simple Dart class
You'll start by building a simple Dart class with the same functionality as the Bicycle class from the Java Tutorial. The Bicycle class contains some private instance variables with getters and setters. A main() method instantiates a Bicycle and prints it to the console.

99c813a1913dcc42.png c97a12197358d545.png

Launch DartPad
This codelab provides a new DartPad instance for every set of exercises. The link below opens a fresh instance, which contains a default "Hello" example. You can continue to use the same DartPad throughout the codelab, but if you click Reset, DartPad takes you back to the default example, losing your work.

Note: For your convenience, at the top of each codelab page is a DartPad instance that reflects the state at the beginning of each exercise.

b2f84ff91b0e1396.png Open DartPad

Define a Bicycle class
b2f84ff91b0e1396.png Above the main() function, add a Bicycle class with three instance variables. Also remove the contents from main(), as shown in the following code snippet:


class Bicycle {
  int cadence;
  int speed;
  int gear;
}

void main() {
}
cf1e10b838bf60ee.png Observations

Dart's main method is named main(). If you need access to command-line arguments, you can add them: main(List<String> args).
The main() method lives at the top level. In Dart, you can define code outside of classes. Variables, functions, getters, and setters can all live outside of classes.
The original Java example declares private instance variables using the private tag, which Dart doesn't use. You'll learn more about privacy a little later, in "Add a read-only variable."
Neither main() nor Bicycle is declared as public, because all identifiers are public by default. Dart doesn't have keywords for public, private, or protected.
Dart uses two-character indentation by convention instead of four. You don't need to worry about Dart's whitespace conventions, thanks to a handy tool called dartfmt. As the Dart code conventions ( Effective Dart) say, "The official whitespace-handling rules for Dart are whatever dartfmt produces."
Define a Bicycle constructor
b2f84ff91b0e1396.png Add the following constructor to the Bicycle class:


Bicycle(this.cadence, this.speed, this.gear);
cf1e10b838bf60ee.png Observations

This constructor has no body, which is valid in Dart.
If you forget the semicolon (;) at the end of a no-body constructor, DartPad displays the following error: "A function body must be provided."
Using this in a constructor's parameter list is a handy shortcut for assigning values to instance variables.
The code above is equivalent to the following:

Bicycle(int cadence, int speed, int gear) {
  this.cadence = cadence;
  this.speed = speed;
  this.gear = gear;
}
Format the code
Reformat the Dart code at any time by clicking Format at the top of the DartPad UI. Reformatting is particularly useful when you paste code into DartPad and the justification is off.

b2f84ff91b0e1396.png Click Format.

Instantiate and print a Bicycle instance
b2f84ff91b0e1396.png Add the following code to the main() function:


void main() {
  var bike = new Bicycle(2, 0, 1);
  print(bike);
}
b2f84ff91b0e1396.png Remove the optional new keyword:


var bike = Bicycle(2, 0, 1);
cf1e10b838bf60ee.png Observation

The new keyword became optional in Dart 2.
If you know that a variable's value won't change, then you can use final instead of var.
Run the example
b2f84ff91b0e1396.png Execute the example by clicking Run at the top of the DartPad window. If Run isn't enabled, see the Problems section later in this page.

You should see the following output:


Instance of 'Bicycle'
cf1e10b838bf60ee.png Observation

No errors or warnings should appear, indicating that type inference is working, and that the analyzer infers that the statement that begins with var bike = defines a Bicycle instance.
Improve the output
While the output "Instance of ‘Bicycle'" is correct, it's not very informative. All Dart classes have a toString() method that you can override to provide more useful output.

b2f84ff91b0e1396.png Add the following toString() method anywhere in the Bicycle class:


@override
String toString() => 'Bicycle: $speed mph';
cf1e10b838bf60ee.png Observations

The @override annotation tells the analyzer that you are intentionally overriding a member. The analyzer raises an error if you fail to properly perform the override.
Dart supports single or double quotes when specifying strings.
Use string interpolation to put the value of an expression inside a string literal: ${expression}. If the expression is an identifier, you can skip the braces: $variableName.
Shorten one-line functions or methods using fat arrow (=>) notation.
Run the example
b2f84ff91b0e1396.png Click Run.

You should see the following output:


Bicycle: 0 mph
Problems?Check your code.

Add a read-only variable
The original Java example defines speed as a read-only variable—it declares it as private and provides only a getter. Next, you'll provide the same functionality in Dart.

b2f84ff91b0e1396.png Open bicycle.dart in DartPad (or continue using your copy).

To mark a Dart identifier as private to its library, start its name with an underscore (_). You can convert speed to read-only by changing its name and adding a getter.

Make speed a private, read-only instance variable

b2f84ff91b0e1396.png In the Bicycle constructor, remove the speed parameter:


Bicycle(this.cadence, this.gear);
b2f84ff91b0e1396.png In main(), remove the second (speed) parameter from the call to the Bicycle constructor:


var bike = Bicycle(2, 1);
b2f84ff91b0e1396.png Change the remaining occurrences of speed to _speed. (Two places)

Tip: If you are using a JetBrains IDE, you can simultaneously rename all instances of a variable by right-clicking the name, and choosing Refactor > Rename from the popup menu.

b2f84ff91b0e1396.png Initialize _speed to 0:


int _speed = 0;
b2f84ff91b0e1396.png Add the following getter to the Bicycle class:


int get speed => _speed;
cf1e10b838bf60ee.png Observations

Uninitialized variables (even numbers) have the value null.
The Dart compiler enforces library privacy for any identifier prefixed with an underscore. Library privacy generally means that the identifier is visible only inside the file (not just the class) that the identifier is defined in.
By default, Dart provides implicit getters and setters for all public instance variables. You don't need to define your own getters or setters unless you want to enforce read-only or write-only variables, compute or verify a value, or update a value elsewhere.
The original Java sample provided getters and setters for cadence and gear. The Dart sample doesn't need explicit getters and setters for those, so it just uses instance variables.
You might start with a simple field, such as bike.cadence, and later refactor it to use getters and setters. The API stays the same. In other words, going from a field to a getter and setter is not a breaking change in Dart.
Finish implementing speed as a read-only instance variable

b2f84ff91b0e1396.png Add the following methods to the Bicycle class:


void applyBrake(int decrement) {
  _speed -= decrement;
}

void speedUp(int increment) {
  _speed += increment;
}
The final Dart example looks similar to the original Java, but is more compact at 23 lines instead of 40:


class Bicycle {
  int cadence;
  int _speed = 0;
  int get speed => _speed;
  int gear;

  Bicycle(this.cadence, this.gear);

  void applyBrake(int decrement) {
    _speed -= decrement;
  }

  void speedUp(int increment) {
    _speed += increment;
  }

  @override
  String toString() => 'Bicycle: $_speed mph';
}

void main() {
  var bike = Bicycle(2, 1);
  print(bike);
}
