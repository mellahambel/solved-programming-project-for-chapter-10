Download Link: https://assignmentchef.com/product/solved-programming-project-for-chapter-10
<br>
Build an interpreter and a compiler to C++ for the language BOOLexp. BOOLexp programs are defined by the following context-free grammar in BNF (not EBNF):

<em>&lt;sentence&gt; </em>::= ( <em>&lt;declarations&gt; </em>, <em>&lt;expr&gt; </em>)

<em>&lt;literal&gt; </em>::= t

<em>&lt;literal&gt; </em>::= f

<em>&lt;var&gt; </em>::= a …e <em>&lt;var&gt; </em>::= g …s

<em>&lt;var&gt; </em>::= u …z

where t, f, |, &amp;, and ∼ are terminals which represent true, false, or, and, and not, respectively, and all lower case letters except for f and t are terminals each representing a variable. Each variable in the variable list is bound to true in the expression. Any variable used in any expression not contained in the variable list is assumed to be false.

Factor your system into the following three components:

<ul>

 <li><strong>Front End </strong>(i.e., a shift-reduce parser, automatically generated with flex and bison, which produces a parse tree)</li>

 <li><strong>Interpreter </strong>(i.e., expression evaluator)</li>

 <li><strong>Compiler </strong>(i.e., translator)</li>

</ul>

The general approach to this problem is to build a parse tree for each sentence and then implement two traversals of the tree: one traversal evaluates the expression as it walks the tree (the interpreter component) and

<em>CHAPTER 10. AUTOMATIC PROGRAM GENERATION</em>

the other generates C++ code as it walks the tree (the compiler component).

The following is sample input and output for the interpreter (i.e., expression evaluator) (&gt; is simply the prompt for input and will be the empty string in your system).

&gt; ([], f | t &amp; f | ~t)

((f | (t &amp; f)) | (~t)) is false.

&gt; ([p,q], ~t | p | ~e &amp; ~f &amp; t &amp; ~q | r)

((((~t) | p) | ((((~e) &amp; (~f)) &amp; t) &amp; (~q))) | r) is true.

Notice that when interpreting a BOOLexp program you must not only evaluate the logical expression (the first element of the program pair) but also determine the order in which operators of it are evaluated and illustrate that order in the diagrammed output. Normal precedence rules hold: ∼ has the highest, &amp; has the second highest, and | has the lowest. Assume left-to-right associativity. When compiling a BOOLexp program to C++ you must generate a C++ program with equivalent semantics as the BOOLexp program. <strong>Requirements:</strong>

<ol>

 <li>Use flex and bison to develop the front end of your system (i.e., scanner and parser, respectively).</li>

 <li>Implement a -i option indicating to only interpret and a -c option indicating to only compile. If no command line options are given, then interpret and compile. Alternatively, generate two seperate executables: one for the interpreter and one for the compiler. Only the first approach is demonstrated below.</li>

 <li>Your program must read from standard input and write to standardoutput. Specifically, your program must read a set of expressions from standard input (one per line) and write the corresponding parenthesized expressions (also one per line, in the format used above) to standard output. When compiling, the compiled programs are written to files, rather than standard output.</li>

 <li>Free all memory that you explicitly allocated from the heap. Specifi-cally, free the entire parse tree which means you must free each node,</li>

</ol>

<em>10.5. PROGRAMMING PROJECT FOR CHAPTER 10                                                              </em>335

and for internal (operator) nodes you must free the buffer which stores the pointers to its children, if used.

<ol>

 <li>The C++ programs you compile to must compile with g++ without errors or warnings.</li>

 <li>Write a Makefile that builds your system (interpreter and compiler)</li>

</ol>

as indicated in Programming Exercise 10.5.18,

<strong>Sample Test Data</strong>

Sample standard input is available at <a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexpstdin.txt">http://perugini. </a><a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexpstdin.txt">cps.udayton.edu/teaching/books/SPUC/www/files/ </a><a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexpstdin.txt">boolexpstdin.txt</a> and sample standard output is available at <a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexpstdout.txt">http://perugini.cps.udayton.edu/teaching/books/SPUC/ </a><a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexpstdout.txt">www/files/boolexpstdout.txt</a><a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexpstdout.txt">.</a> A sample test session with boolexp on that data is available at <a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexptestsession.txt">http://perugini.cps.udayton.edu/ </a><a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexptestsession.txt">teaching/books/SPUC/www/files/boolexptestsession.txt</a><a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexptestsession.txt">. </a>These test cases are not exhaustive. There is also a reference boolexp executable solution for this system available at <a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexp">http://perugini.cps. </a><a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexp">udayton.edu/teaching/books/SPUC/www/files/boolexp</a><a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexp">.</a> This sample test data with the reference executable is bundled and available at <a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexpdata.tar">http://perugini.cps.udayton.edu/teaching/books/SPUC/ </a><a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexpdata.tar">www/files/boolexpdata.tar</a><a href="http://perugini.cps.udayton.edu/teaching/books/SPUC/www/files/boolexpdata.tar">.</a>

The following is sample input and output for the interpreter (only) (&gt; is simply the prompt for input and will be the empty string in your system).

$ ./boolexp -i

&gt; ([] , f | t &amp; f | ~ t)

((f | (t &amp; f)) | (~t)) is false. &gt; ([p], f | t &amp; f | ~p)

((f | (t &amp; f)) | (~p)) is false.

&gt; ([] , f | t | f &amp; t | f | t &amp; t &amp; t | ~ t)

(((((f | t) | (f &amp; t)) | f) | ((t &amp; t) &amp; t)) | (~t)) is true.

&gt; ([p, q], ~t | p | ~e &amp; ~f &amp; t &amp; ~q | r)

((((~t) | p) | ((((~e) &amp; (~f)) &amp; t) &amp; (~q))) | r) is true.

&gt; ([] , t &amp; f        &amp; t | ~ t    &amp; ~ f &amp; ~ f | f &amp; t &amp; ~ t)

((((t &amp; f) &amp; t) | (((~t) &amp; (~f)) &amp; (~f))) | ((f &amp; t) &amp; (~t))) is false.

&gt; ([] , t &amp; f | t &amp; f | t &amp; f | f &amp; ~ t | f)

(((((t &amp; f) | (t &amp; f)) | (t &amp; f)) | (f &amp; (~t))) | f) is false.

&gt; ([], t &amp; t &amp; ~ f | f &amp; ~ t | ~ t &amp; f)

((((t &amp; t) &amp; (~f)) | (f &amp; (~t))) | ((~t) &amp; f)) is true.

&gt; ([        ], t &amp; t | ~ f &amp; ~ f | t &amp; f | ~ t)

&gt; ^D

$

preter and compiler): $ ./boolexp

&gt; ([] , t &amp; f

^D

$

$ cat 1.cpp #include&lt;iostream&gt; using namespace std; main() {

bool p = true; bool q = true;

bool e = false; bool r = false; if (result) cout &lt;&lt; “true”;

else

cout &lt;&lt; “.” &lt;&lt; endl;

}

$

$ cat 4.cpp #include&lt;iostream&gt; using namespace std; main() { if (result) cout &lt;&lt; “true”;

else

cout &lt;&lt; “.” &lt;&lt; endl;

}

$

$ ./boolexp

&gt; ([

^D

$

$ ./boolexp -c

$

^D

$

$ cat 1.cpp #include&lt;iostream&gt; using namespace std; main() { if (result) cout &lt;&lt; “true”;

else

cout &lt;&lt; “.” &lt;&lt; endl;

}

<strong>10.6</strong>

<strong>10.7</strong>

<strong>10.8</strong>

<h1>10.9</h1>