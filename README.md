Download Link: https://assignmentchef.com/product/solved-ece253-lab-7-and-8-using-the-arm-a9-processor
<br>
This exericse provides an introduction to the ARM A9 processor, its assembly language, and development tools.

To prepare for this exercise you need to be familiar with the ARM A9 processor architecture and its assembly language. This processor is described in the tutorial called <em>Introduction to the ARM Processor</em>, which is available in the Computer Organization section of Altera’s University Program website. The ARM processor is also described in Appendix D of the textbook for ECE253.

For this exercise you will use an ARM A9 processor that is part of a computer system called the <em>DE1-SoC Computer</em>. This computer system is implemented inside the Altera Cyclone V SoC chip on the Altera DE1SoC lab board. A detailed description of the DE1-SoC Computer can be found in the document entitled <em>DE1-SoC Computer with ARM</em>, which can be found in the Computer Systems secton of Altera’s University Program website.

Software to Install for the Computer Organization Lab Exercises

The Computer Organization lab exercises require additional software other than Quartus. To use the ARM processor on your own computer, you need to have installed the software package called the <em>Altera Monitor Program</em>, as described below. <strong><u>Lab 7</u></strong>

Part I

In this part of the exercise you will become familiar with the <em>Altera Monitor Program</em>. You will use this tool to develop software programs that run on the ARM processor. You will be able to compile your code, download the compilation results into the DE1-SoC Computer on the DE1-SoC board, and then execute and debug your code on the ARM processor.

Before you can use the Altera Monitor Program, it has to be installed on your computer. Instructions for installing this program are given in the document <em>Altera Monitor Program Tutorial for ARM</em>. Obtain this tutorial from the Computer Organization section of Altera’s University Program web site.

After successfully installing the Monitor Program, perform the steps found in Section 3 of the tutorial to learn about the features of the tool. In these steps you will create a Monitor Program project that targets the ARM processor in the DE1-SoC Computer. You will use a sample of an assembly language program that is provided in the Monitor Program tool, and you will learn about compiling code, downloading compiled programs onto the DE1-SoC board, and executing and debugging programs.

You do not need to perform the steps in the tutorial after Section 3; those steps deal with advanced topics such as working with interrupts (we will learn about interrupts later in this course) and working with C programs.

Part II

In this part you will create your own assembly language program and execute it on the ARM processor in the DE1-SoC Computer.

Perform the following:

<ol>

 <li>Create a new, empty, folder to hold your Monitor Program project for this part. Create a file called <em>s</em>, and type the assembly language code shown in Figure 1 into this file. This code uses an algorithm to count the longest string of 1s in a word of data. The algorithm uses shift and AND operations to find the required result—make sure that you understand how this works.</li>

 <li>Make a new Monitor Program project in the folder where you stored the <em>s </em>file. Use the DE1-SoC Computer for this project, and specify the assembly language file that you created (rather than a sample program as was done in the <em>Altera Monitor Program Tutorial for ARM</em>).</li>

 <li>Compile and load the program. Fix any errors that you encounter (if you mistyped some of the code). Oncethe program is loaded into memory in the DE1-SoC Computer, single step through it to see how the program works.</li>

</ol>

/* Program that counts consecutive 1’s */

.text

<table width="459">

 <tbody>

  <tr>

   <td width="80">start:</td>

   <td width="59">.global</td>

   <td colspan="2" width="320">start</td>

  </tr>

  <tr>

   <td width="80"> </td>

   <td width="59">LDR</td>

   <td colspan="2" width="320">R1, TEST NUM // load the data word into R1</td>

  </tr>

  <tr>

   <td width="80"> </td>

   <td width="59">MOV</td>

   <td width="99">R0, #0</td>

   <td width="221">// R0 will hold the result</td>

  </tr>

  <tr>

   <td width="80">LOOP:</td>

   <td width="59">CMP</td>

   <td width="99">R1, #0</td>

   <td width="221">// loop until the data contains no more 1’s</td>

  </tr>

  <tr>

   <td width="80"> </td>

   <td width="59">BEQ</td>

   <td width="99">END</td>

   <td width="221"> </td>

  </tr>

  <tr>

   <td width="80"> </td>

   <td width="59">LSR</td>

   <td width="99">R2, R1, #1</td>

   <td width="221">// perform SHIFT, followed by AND</td>

  </tr>

  <tr>

   <td width="80"> </td>

   <td width="59">AND</td>

   <td width="99">R1, R1, R2</td>

   <td width="221"> </td>

  </tr>

  <tr>

   <td width="80"> </td>

   <td width="59">ADD</td>

   <td width="99">R0, #1</td>

   <td width="221">// count the string lengths so far</td>

  </tr>

  <tr>

   <td width="80"> </td>

   <td width="59">B</td>

   <td width="99">LOOP</td>

   <td width="221"> </td>

  </tr>

  <tr>

   <td width="80">END:</td>

   <td width="59">B</td>

   <td width="99">END</td>

   <td width="221"> </td>

  </tr>

  <tr>

   <td colspan="2" width="139">TEST NUM: .word</td>

   <td width="99">0x103fe00f</td>

   <td width="221"> </td>

  </tr>

 </tbody>

</table>

.end

Figure 1. A program that counts consecutive 1s. <strong><u>Lab 8</u></strong>

Part III

Perform the following.

<ol>

 <li>Make a new folder and make a copy of the file <em>s </em>in that new folder.</li>

 <li>In the new copy of the <em>s </em>file, take the code which calculates the number of consecutive 1s and make it into a subroutine called ONES. Have the subroutine use register R1 to receive the input data and register R0 for returning the result.</li>

 <li>Add more words in memory starting from the label TEST NUM. You can add as many words as you like— but include at least 10 words.</li>

 <li>In your main program, call the newly-created subroutine in a loop for every word of data that you placed inmemory. Keep track of the longest string of 1s in any of the words, and have this result in register R5 when your program completes execution.</li>

 <li>Make sure to use the single-step capability of the Monitor Program to step through your code and observewhat happens when your subroutine call and return instructions are executed.</li>

</ol>

Part IV

One might be interested in the longest string of 0s, or even the longest string of alternating 1s and 0s. For example, the binary number 101101010001 has a string of 6 alternating 1s and 0s. The number 1010 has a string of 4 consecutive 1s and 0s.

Write a program that determines the following:

<ul>

 <li>Longest string of 1s in a word of data—write the result to register R5</li>

 <li>Longest string of 0s in a word of data—write the result to register R6</li>

 <li>Longest string of alternating 1s and 0s in a word of data—write the result to register R7 (Hint: What happens when an n-bit number is XORed with an n-bit string of alternating 0s and 1s?)</li>

</ul>

Make each calculation in a separate subroutine (called ONES, ZEROS, and ALTERNATE). Call each of these subroutines in the loop that you wrote in Part III, and keep track of the largest result for each calculation, from your list of data.