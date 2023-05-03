Download Link: https://assignmentchef.com/product/solved-cs2030s-problem-set-6-functional-interfaces-and-lambda-expressions
<br>
Functional Interfaces and Lambda Expressions

<ol>

 <li>What is the difference between

  <ul>

   <li>out.println(‘‘CS2030’’), and</li>

   <li>()-&gt;System.out.println(‘‘CS2030’’) ?</li>

  </ul></li>

</ol>

Explain in terms of the data type and the execution of the printing.

<ol start="2">

 <li>Consider the Point

  <ul>

   <li>Complete the code below to provide the add and scale</li>

  </ul></li>

</ol>

public class Point { private final double x; private final double y;

public Point(double x, double y) { this.x = x; this.y = y;

}

@Override public String toString() { return “(” + this.x + “, ” + this.y + “)”;

}

public Point add(Point q) {

// insert code to return a new point that is the

// sum of this point and point q. Just sum the // corresponding x and y coordinates.

}

public Point scale(double k) {

// insert code to return a new point whose x,y

// coordinates are k times those of this point. }

}

<ul>

 <li>Recall the generic average function:</li>

</ul>

import java.util.function.BinaryOperator; import java.util.function.BiFunction;

&lt;T&gt; T average(List&lt;T&gt; list, BinaryOperator&lt;T&gt; add, BiFunction&lt;T,Double,T&gt; scale) {

T sum = list.get(0);             // assume list is non-empty int size = list.size(); for (T item : list.subList(1, size)) sum = add.apply(sum, item);

return scale.apply(sum, new Double(1.0/size));

}

Provide appropriate lambdas in the code below to compute the average of the three points.

List&lt;Point&gt; list = new ArrayList&lt;&gt;(); list.add(new Point(1.0, 1.0)); list.add(new Point(1.0, 2.0)); list.add(new Point(-1.0, 1.0)); average(list, ??, ??);

<ul>

 <li>Now, in the Circle class, write an add(other) method that returns a new circle whose centre is the sum of the centres of this and other circle, and whose radius is the sum of their corresponding radii.</li>

</ul>

Likewise, write a scale(k) method that returns a new circle whose radius and centre are scaled by k. Finally, create a list of three circles with different centres and radii, and find the circle whose centre lies at the average of the centres of the three, and whose radius is their average radii. Don’t forget to override the toString method in Circle for displaying it. public class Circle { private final Point centre; private final double radius;

public Circle(Point c, double r) { this.centre = c; this.radius = r;

}

//Don’t change the above, but insert code here

//for add(other) and scale(k) methods

}

List&lt;Circle&gt; list = new ArrayList&lt;&gt;(); list.add(new Circle(new Point(1.0, 1.0), 1.0)); list.add(new Circle(new Point(1.0, 2.0), 4.0)); list.add(new Circle(new Point(-1.0, 1.0), 2.0)); average(list, ??, ??);

<ol start="3">

 <li>Read the Java documentation of the andThen method in java.util.function.Function.</li>

</ol>

<ul>

 <li>It is possible to compose functions without using andThen. Complete the code below to do so: import java.util.function.Function;</li>

</ul>

&lt;T,U,R&gt; Function&lt;T,R&gt; compose(Function&lt;T,U&gt; f, Function&lt;U,R&gt; g) {

// Insert code here to return a function h, such that

// h(x) = g(f(x))

}

<ul>

 <li>Compose the given functions f and g, and apply it to 5 to get 49 as the result. What if you wanted a result of 729?</li>

</ul>

Function&lt;Integer,Integer&gt; f = x -&gt; x+2;

Function&lt;Integer,Integer&gt; g = x -&gt; x*x; (c) Suppose these two methods are defined in the Point class: public double distanceTo(Point q) { return Math.sqrt(sumOfSquares(this.x – q.x, this.y – q.y));

}

public static double sumOfSquares(double a, double b) { return a*a + b*b;

}

Run the following code in JShell to see what happens. Explain. (Note that the var keyword may be used to denote “some suitable type”. The Java compiler will infer the type of the variable based on the right hand side of the assignment. Also note the use of <em>method references</em>.)

double howFarFromHere(Circle c, Point here) { return compose(Circle::getCentre, here::distanceTo).apply(c);

}

var c = new Circle(new Point(3.0, 4.0), 1.0); var p = new Point(0.0, 0.0); howFarFromHere(c, p);

<ol start="4">

 <li><em>Currying</em><a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> is the conversion a function of two arguments into two functions, each taking one argument, such that their sequencing computes the same result as that of the original function.</li>

</ol>

For example: suppose <em>f</em>(<em>x,y</em>) = <em>x </em>+ <em>y</em><sup>2</sup>. Define <em>h<sub>x</sub></em>(<em>y</em>) = <em>x </em>+ <em>y</em><sup>2</sup>, ie. it is a function of one argument <em>y</em>, since the value of <em>x </em>is fixed. Also define <em>g</em>(<em>x</em>) = <em>h<sub>x</sub></em>. Then clearly, <em>f</em>(<em>x,y</em>) = <em>h<sub>x</sub></em>(<em>y</em>) = <em>g</em>(<em>x</em>)(<em>y</em>). We say that <em>curry</em>(<em>f</em>) = <em>g</em>. This idea is readily expressed as:<sup>2</sup>

import java.util.function.BiFunction;

&lt;X,Y,Z&gt; Function&lt;Y, Function&lt;X,Z&gt;&gt; curry(BiFunction&lt;X,Y,Z&gt; f) { return y -&gt; (x -&gt; f.apply(x,y));

}

<ul>

 <li>What is the result of executing the following code, and how does this compare withslide 19 of the lecture notes on Functional Interfaces?</li>

</ul>

Function&lt;Integer, Function&lt;Integer, Integer&gt;&gt; addN = curry( (n,x) -&gt; n+x ); Function&lt;Integer, Integer&gt; add5 = addN.apply(5); add5.apply(7);

<ul>

 <li>What is the result of: apply(10).apply(7) ?</li>

 <li>What should ??? be in: ??? mystery = curry(Point::sumOfSquares); That is, what’s the type of mystery? Note that sumOfSquares was defined in Q3(c).</li>

 <li>Show how you would use mystery to calculate 3<sup>2 </sup>+ 4<sup>2</sup>.</li>

</ul>

<a href="#_ftnref1" name="_ftn1">[1]</a> Named after Haskell Curry. See https://en.wikipedia.org/wiki/Currying <sup>2</sup>Look up BiFunction in the Java documentation.