Download Link: https://assignmentchef.com/product/solved-adv-lab-3-more-recursion-with-scala
<br>
In this lab you will practice further with recursion in Scala. You can use whichever of the tools introduced in Lab 1 you prefer to attempt the following exercises. You should use your lecture notes (part 4) and references listed under ‘Further reading’ to help you.

Task 1. Lists and recursion

In Scala functional programming we think of lists as being composed of two parts:

<ul>

 <li><strong>head</strong> – the first element in this list</li>

 <li><strong>tail</strong> – the rest of the list (NOT the last element in the list!)</li>

</ul>

We also have the concept of an empty list, which we refer to as <strong><em>Nil</em></strong>.

You can create and match lists using the <em>“cons”</em> syntax:

<ul>

 <li>Uses the <strong>::</strong> operator (actually it’s a method of the List class) that takes two arguments, a “head”, which is a single element, and a “tail”, which is a List</li>

 <li>A single element list is <em>“cons”</em>tructed from an element (head) and empty list (tail) – i.e. the tail is Nil</li>

</ul>

val single_element_list = 1::Nil

val longer_list = 1 :: 2 :: 3 :: Nil

You can also create a list using the <em>range</em> method of List:




val x = List.range(1,6)

<ol>

 <li>Include the following import statement so that you can use cons syntax:</li>

</ol>




import scala.collection.immutable.::




<ol start="2">

 <li>Use cons syntax to create a list <em>list1</em> with the values 1,2,3,4,5,6,7,8,9,10, and use the <em>range</em> method to create a list <em>list2</em> with the same values. Declare <em>list2</em> as a <em>var</em> rather than a <em>val</em>.</li>

</ol>




<ol start="3">

 <li>Write an expression that joins the two lists with the <strong>:: </strong> Look carefully at the result. Write another expression that uses the <strong>:::</strong> operator instead. Look carefully at the result of this, and deduce the difference between the purpose of these operators. Write another expression that uses the ++ operator instead. Which of the other operators does this behave like? (Scala often seems to have more than one way of doing the same thing!)</li>

</ol>




<ol start="4">

 <li>The List type has methods to get the head and tail of a list, so you can easily split a list into its head and tail. The head is a single element, the tail is another list (which may be empty). However, you need to do a little bit more work to find the last element of a list.You can get the last element using recursion – you split the list initially into head and tail. If the tail is empty, then the head of the list is the last element. If not, you repeat exactly the same process with the tail. You keep repeating this (recursion) until you have a list with an empty tail (stopping condition) and then return the head of that list.</li>

</ol>




<ol start="5">

 <li>Test the following function that does this by writing the function and calling it on <em>list1</em>.</li>

</ol>




def <strong>lastif</strong>(ls:List[Int]):Int = {if(ls.tail == Nil)ls.headelse<strong>lastif</strong>(ls.tail)}




<ol start="6">

 <li>Test the following version of the same function that uses pattern matching instead of an if expression (you may get a warning about exhaustiveness with this one, ignore that for now). Which style do you prefer?</li>

</ol>




def <strong>last</strong>(ls: List[Int]): Int = ls match {case h :: Nil =&gt; hcase _ :: tail =&gt; <strong>last</strong>(tail)}




<ol start="7">

 <li>Write a function <em>sum</em> that uses recursion to calculate the <em>sum</em> of the elements of a list of Ints. You can use either an <em>if</em> expression or a <em>match</em> What will the stopping condition be in this case – It’s actually slightly simpler than the length example?</li>

</ol>




Note that List has a method <em>sum</em> that does the same job as your sum function – test this and check that it gives the same result. It is generally better to use the built-in method where available, but it is useful to understand how to use recursion on a list if you need to do something that is not already available.

Task 2 Tail recursion

In this task you will continue to use the lists you created in Task 1.

<ol>

 <li>Test thefollowing function that calculates the length of a list. You can call the function to get the length of <em>list2</em>.</li>

</ol>

def listLength(ls:List[_]):Int = ls match{case Nil =&gt; 0case h :: tail =&gt; 1 + listLength(ls.tail)}

(this can also be written with an <em>if</em> expression – see listing at end)

If you are using a Scala Worksheet in IntelliJ, note the symbol next to the function name. Hover the cursor over this for an explanation.

<ol start="2">

 <li>Add the following statement before your call to <em>listLength</em>. This builds <em>list2</em> into a much longer list.</li>

</ol>

1 to 15 foreach(x=&gt; list2 = list2++list2)

What happens? Why?

<ol start="3">

 <li>Replace<em>listLength</em> with the following tail-recursive version and repeat the test.</li>

</ol>

def listLength(ls:List[_]):Int = {def listLength_nested(ls:List[_], len: Int):Int = ls match{case Nil =&gt; lencase h :: tail =&gt; listLength_nested(ls.tail, len+1)}listLength_nested(ls, 0)}




(this can also be written with an <em>if</em> expression – see listing at end)




What happens now? What symbol do you see next to the function name in IntelliJ, and what explanation is given when you hover over it?




<ol start="4">

 <li>Write and test a tail-recursive version of your <em>sum</em> function</li>

</ol>




<ol start="5">

 <li>Write and test a tail-recursive version of the recursive <em>power</em> function you created in Lab 2.</li>

</ol>




<ol start="6">

 <li>(Challenge) The following function (if and match versions shown) calculates the nth element of the Fibonacci sequence 1,1,2,3,5,8,13,… (each element is the sum of the two previous ones)</li>

</ol>




def fib(n: Int): Int = n match {case 0 =&gt; 0case 1 =&gt; 1case _ =&gt; fib(n – 1) + fib(n – 2)}




def fib(n: Int): Int = {if (n &lt;= 1)nelsefib(n – 1) + fib(n – 2)}




So, <em>fib(6)</em> gives the result 8.




This is not tail-recursive. Write a tail-recursive version of this function.










Versions of <em>listLength</em> function using <em>if</em> expressions:




def listLength(ls:List[_]):Int = {if(ls == Nil)

0else

1 + listLength(ls.tail)}










def listLength(ls:List[_]):Int = {def listLength_nested(ls:List[_], len: Int):Int = {if(ls == Nil) lenelse listLength_nested(ls.tail, len+1)}listLength_nested(ls, 0)}


