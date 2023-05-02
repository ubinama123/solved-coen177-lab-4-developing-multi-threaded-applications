Download Link: https://assignmentchef.com/product/solved-coen177-lab-4-developing-multi-threaded-applications
<br>
<strong>Objectives</strong>

<h5>1.     To develop multi-threaded application programs</h5>

<h5>2.     To demonstrate the use of threads in matrix multiplication</h5>

<h5></h5>

<h5><strong>Guidelines</strong></h5>

<h5>As noted in the class text book<a href="#_ftn1" name="_ftnref1">[1]</a> there is an increasing importance of parallel processing that led to the development of lightweight user-level thread implementations. Even so, the topic of whether threads are a better programming model than processes or other alternatives remains open. Several prominent operating systems researchers have argued that normal programmers should almost never use threads because (a) it is just too hard to write multi-threaded programs that are correct and (b) most things that threads are commonly used</h5>

<h5>for can be accomplished in other, safer ways. These are important arguments to understand—even if you agree or disagree with them, researchers point out pitfalls with using threads that are important to avoid. The most important pitfall is the concurrent access of threads to shared memory. When threads concurrently read/write to shared memory, program behavior is undefined. This is because thread schedule on the CPU is non-deterministic. The program behavior completely changes when you rerun the program. This should have been obvious to you by now with you the examples you have run in Lab2.</h5>

<h5>    To ensure a deterministic behavior of programs where threads cooperate to access shared memory, a synchronization mechanism needs to be implemented. Consequently,</h5>

<h5>1.     The program behavior will be related to a specific function of input, not of the sequence of which thread runs first on the CPU</h5>

<h5>2.     The program behavior will be deterministic and will not vary from run to run</h5>

<h5>3.     These facts should not be IGNORED, otherwise the compiler will mess up the results and will not be according what is thought would happen</h5>

<h5></h5>

<h5>This lab is designed to give you the first hands-on programming experience on developing multi-threaded applications. In the coming labs, you will</h5>

<h5></h5>

<strong>C Program with threads (problems 1, 2, 7, and 8 of the class textbook)</strong>

In chapter 4 of the class text book, the threadHello.c program has been discussed. The threads run on the CPU in different orders. Demonstrate each of the following steps to the TA to get a grade on this part of the lab assignment.




<ul>

 <li>Download the slightly revised threadHello.c program from Camino, then compile and run several times. The comment at the top of program explains how to compile and run the program.</li>

</ul>




Explain what happens when you run the threadHello.c program? Do you get the same result if you run it multiple times? What if you are also running some other demanding processes (e.g., compiling a big program, playing a Flash game on a website, or watching streaming video) when you run this program?




The function go() has the parameter arg passed a local variable. Are these variables per-thread or

shared state? Where does the compiler store these variables’ states?




The main() has local variable i. Is this variable per-thread or shared state? Where does the compiler store this variable?







<ul>

 <li>Delete the second for loop in threadHello.c program so that the main routine simply creates NTHREADS threads and then prints “Main thread done.” What are the possible outputs of the program now. Explain.</li>

</ul>




<strong> </strong>

<strong>Matrix multiplication with threads (problem 5 of the class text book)</strong>

<ul>

 <li>Write a program that uses threads to perform a parallel matrix multiply. To multiply two matrices, C = A*B, the result entry C<sub>(i,j)</sub> is computed by taking the dot product of the i<sup>th</sup> row of A and the j<sup>th</sup> column of B: C<sub>i,j</sub> = SUM A<sub>(i,k)</sub>*B<sub>(k,j)</sub> for k = 0 to N-1, where N is the matrix size. We can divide the work by creating one thread to compute each value (or each row) in C, and then executing those threads on different processors in parallel on multi-processor systems. As shown in the following figure, each is cell in the resulting matrix is the sum of the multiplication of row elements of the first matrix by the column elements of the second matrix.</li>

</ul>







You may fill in the entries of A and B matrices (double matrixA[N][M], matrixB[M][L] ) using a random number generator as below:

srand(time(NULL));

for (int i = 0; i &lt; N; i++)

for (int j = 0; j &lt; M; j++)

matrixA[i][j] = rand();




srand(time(NULL));

for (int i = 0; i &lt; M; i++)

for (int j = 0; j &lt; L; j++)

matrixB[i][j] = rand();







The following are important notes:

<ul>

 <li>The number of columns of the first matrix must be equal to the number of rows in the second matrix.</li>

 <li>The values of N, M, and L must be large to exploit parallelism (e.g. N, M, L = 1024).</li>

 <li>The output matrix would be defined double matrixC[N][L];</li>

 <li>The Matrix multiplication is a loosely coupled problem and so decomposable, i.e. multiplication of each row of matrixA with all columns of matrix can be performed independently and in parallel</li>

 <li>The number of threads to be created in the program equals to N and each thread i would be performing the following task:</li>

</ul>

for (int j = 0; j &lt; L; j++){

double temp = 0;

for (int k = 0; k &lt; M; k++){

temp += matrixA[i][k] * matrixB[k][j];

}

matrixC[i][j] = temp;

}




<ul>

 <li>The main thread needs to wait for all other threads before it displays the resulting matrixC</li>

 <li>You may use the code skeleton “lab4Skeleton.c” available on Camino</li>

</ul>




<ul>

 <li>[Bonus] Modify your program in Step 3 to creat N*L threads, each computing i<sup>th</sup> row * j<sup>th</sup></li>

</ul>

<a href="#_ftnref1" name="_ftn1">[1]</a> J. Anderson and M. Dahlin, Operating Systems – Principles and Practice, Recursive Books, 2<sup>nd</sup> Edition, 2014