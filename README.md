Download Link: https://assignmentchef.com/product/solved-cs2123-data-structures-assignment-3-multilevelqueuescheduler-solveed
<br>
In this assignment you will be simulating some of the work performed by an operating system (albeit at a super high level). Specifically you will track the simulated processes that currently need to run and then schedule them to run on the CPU according to a given set of rules.

<h1>Introduction</h1>

In “process.h” you should complete the struct process. Each process has the following data:

<ul>

 <li>An identifier (i.e., processName)</li>

 <li>A number of time steps it needs to run (i.e., runtime)</li>

 <li>An array of data that belongs to that process (i.e., a processData struct)</li>

 <li>A priority of either FOREGROUND or BACKGROUND</li>

 <li>You can add other data that will help in simulating the schedule.</li>

 <li>In particular, what time the process was added to the queue may be useful</li>

</ul>

In “multilevelQueueScheduler.h” you should complete the struct schedule. Each schedule should have the following data:

<ul>

 <li>A queue of FOREGROUND processes</li>

 <li>A queue of BACKGROUND processes</li>

 <li>You can add other data that will help in simulating the schedule.</li>

 <li>In particular, the number of time steps since the start of the simulation may be useful</li>

</ul>

<h1>Code: createSchedule (1 point)</h1>

Mallocs and returns a new schedule. Be sure to also create queues for your schedule.

<strong>Code: isScheduleUnfinished (1 point)</strong>

Returns true if given schedule has any processes in either of its queues.

<h1>Code: addNewProcessToSchedule (3 points)</h1>

You are passed a process identifier and priority to add to the appropriate queue in the schedule.

<h1>Code: simulateNextTimeStep (9 points)</h1>

Simulates running <strong>one time step </strong>of the next process. The “driverSimOS.c” code repeatedly calls this function until there are no processes left in the schedule. There are important helper methods in “processSimulator.c” so be sure to read through them. Below are the rules for which process to run:

<ul>

 <li>Every process that has remained in the BACKGROUND queue for 50 time steps is promoted to being a FOREGROUND process (i.e, move it to the rear of the FOREGROUND queue).</li>

 <li>If there exists a FOREGROUND process in the schedule then no BACKGROUND process is run.</li>

 <li>Rules for running a FOREGROUND process:

  <ul>

   <li>The queue follows a round-robin schedule scheme. In particular, you should run the process at the front of the FOREGROUND queue for one time step. If this is the 5th time that process was run it is moved to the back of the FOREGROUND queue.</li>

   <li>If this process has run the specified number of times remove it from the queue and free the process as well as its process data.</li>

  </ul></li>

 <li>Rules for running BACKGROUND processes:

  <ul>

   <li>The queue follows a FCFS (first-come, first-serve) schedule scheme. Processes are completed in the order they were added to the queue. In particular, you should run the process at the front of the BACKGROUND queue for one time step.</li>

   <li>If this process has run the specified number of times remove it from the queue and free the process as well as its process data.</li>

  </ul></li>

 <li>The simulated process will return a string containing the name of another process or a NULL. Either way you do not need to do anything with the value except return it.</li>

</ul>

<strong>Code: freeSchedule (1 point)</strong>

Free all of the memory associated with the given schedule.

<h1>Analysis: Runtime of Your Code (2 points)</h1>

<ul>

 <li>What is the asymptotic runtime of your addNewProcessToSchedule?</li>

 <li>What is the asymptotic runtime of your simulateNextTimeStep?</li>

</ul>

<h1>Analysis: Priority Queue (3 points)</h1>

Suppose we combined the FOREGROUND and BACKGROUND queues from part one into a single priority queue.

<ul>

 <li>Would the asymptotic runtime of addNewProcessToSchedule be increased, decreased, or say the same?</li>

 <li>Specifically, what is the new asymptotic runtime of addNewProcessToSchedule?</li>

 <li>Justify your reasoning for this runtime in one or two sentences. The answer depends on how you setup your priority queue so this justification is critical for earning points.</li>

</ul>

<strong>Deliverables:</strong>

Your solution to the <strong>code </strong>portion of the assignment should be submitted as “multilevelQueueScheduler.c”, “multilevelQueueScheduler.h”, and “process.h”. The <strong>analysis </strong>portion should be submitted as separate .pdf file.

Upload these file to Blackboard under Assignment 3. <strong>Do not zip your files</strong>.

To receive full credit, your code must compile and execute. You should use valgrind to ensure that you do not have any memory leaks.

<strong>Getting started:</strong>

The provided code is deliberately obtuse (especially “processSimulator.c”). You should focus less on what the code specifically does and more on where to call the code in your functions (hints to this were given in the function comment headers so be sure to read them).

When in doubt <strong>try running your code! </strong>Don’t be afraid to add print statements to help you better understand what data is being stored in a struct or passed by a function.