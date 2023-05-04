Download Link: https://assignmentchef.com/product/solved-cs439-project-0-the-shell
<br>
5/5 - (2 votes)

<article id="grip-content" class="markdown-body entry-content">

 <center>

  <span style="font-size: 2em;">Introduction</span>







 </center>Welcome to the first CS 439 project! Like all other projects in this course, you will be working in C. While your previous classes have taught you the basics of the C language, you have likely never written large programs in the language before. In this project, you will write a mid-sized program in C.




 The program you will write in this assignment is a simple Unix shell. The shell is the basic text interface of the Unix world, and you will use shells for most of the remaining projects in this course (not the one you wrote!). While building this shell, you should gain a much better understanding of how real Unix shells work.

 Finally, you will get a chance to practice process creation and control.

 <h2><a id="user-content-overview-of-shells" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#overview-of-shells" aria-hidden="true"></a>Overview of Shells</h2>

 A <em>command-line interpreter</em> (CLI), or a <em>shell</em>, is a program that runs other programs on the behalf of its user. A shell repeatedly prints a prompt, waits for input from the user, and then executes the actions that were requested. The shell you implement in this project will be similar to, but much simpler than, the shell you use when you log in to a typical Unix system.

 The input provided by the user takes the form of a sequence of <em>command lines</em>. A command line is a sequence of ASCII words separated by whitespace. The first word in the command line is either the name of a built-in command or the name of an executable file. The remaining words are command-line arguments.

 Shells will usually execute the requested actions by running other programs. However, some actions simply cannot be executed by other programs. For these, the shell provides a set of commands known as <em>built-in commands</em>, and it processes these differently. You will implement these details later in the project.

 Shells also offer other convenience features. For example, the user may want to capture the output of a program in a file, for later analysis. The user may also want to be able to run several child processes at the same time. You will implement both these features in this project.

 At the end of this project, you will have a fully-functioning (albeit relatively simple) Unix shell.

 <h2><a id="user-content-typographical-conventions" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#typographical-conventions" aria-hidden="true"></a>Typographical Conventions</h2>

 Vocabulary/terminology that you should know will be <em>italicized</em>.

 Things that need to be emphasized will be in <strong>bold font</strong>.

 Filenames, code, and terminal output (generally, anything you might expect to see in the terminal when working on this project) will be in <tt>teletype</tt>. Usually, if it’s prefaced by <tt>unix&gt;</tt>, this is something you should type in your regular shell, while things prefaced by <tt>utcsh&gt;</tt> should be given as input to your project.

 &#x1f41a; The shell emoji will be used when we wish to point out a difference between how this project works and how most real-world shells (e.g. bash, zsh) work.

 <h2><a id="user-content-getting-started-with-your-partner" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#getting-started-with-your-partner" aria-hidden="true"></a>Getting Started with Your Partner</h2>

 Begin by talking with your partner and agree on how you will collaborate. If you need to work remotely, you can find some ideas in the <a href="https://docs.google.com/document/d/1uoBtOX_HzZj9hUFFYbmZMpB6WKA7dwYQevJvAda64bQ/edit?usp=sharing" rel="nofollow">remote collaboration guide</a>

 Set up a repository on the UTCS GitLab server in accordance with the <a href="https://docs.google.com/document/d/1WRGVUwYcXOjTsgp0jXkfaq_9wrkjx_81BXa2t_kw2oI" rel="nofollow">Git Instructions</a>

 As you get started this week, please submit your answers to the questions in our <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell_group_planning.txt" rel="nofollow">Group Planning document</a> this Friday evening. On the second Friday of the project, we will ask you to submit a Group Reflections document.

 <h2><a id="user-content-getting-started-with-the-shell-project" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#getting-started-with-the-shell-project" aria-hidden="true"></a>Getting Started with the Shell Project</h2>

 We provide <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell_project.tar.gz" rel="nofollow">starter code</a> for this project. Get it from the class web page either by running the following command from the command line:

 <pre class="language-" data-role="codeBlock" data-info="">unix&gt; wget https://www.cs.utexas.edu/%7Eans/classes/cs439/projects/shell_project/shell_project.tar.gz</pre>

 or by downloading it in your browser.

 Put the file <tt>shell_project.tar.gz</tt> in the protected directory (the project directory) in which you plan to do your work. Then do the following:

 <ol>

  <li>Type the command <tt>tar xvzf shell_project.tar.gz</tt> to expand the tar archive. Once the command has finished expanding the archive, you should see the following files:</li>

 </ol>

 <pre class="language-" data-role="codeBlock" data-info="">  Files:  Makefile         # Compiles your shell program and runs the tests  README.shell     # Used for submission  # Files for Part 0  fib.c            # Implement fibonacci here  # Files for Part 1/2  argprinter.c     # A test program which can be used to debug execv issues  util.c           # Instructor-provided utility functions  util.h           # The header file for util.c  utcsh.c          # Implement your shell here  tests            # A directory of tests for your shell  examples         # A directory with example shell scripts in it</pre>

 <ol>

  <li>Type the command <tt>make</tt> to ensure that your compiler can build the skeleton code.</li>

  <li>Fill out the requested information in <tt>README.shell</tt>, where applicable.</li>

  <li>Download and read over the questions in the <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell_design.txt" rel="nofollow">design document</a></li>

  <li>Log your time (now and every time you work!) in the <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/pair_programming_log.txt" rel="nofollow">Pair Programming Log</a>.</li>

 </ol>

 <strong>Read this entire handout and consider the overall design of your shell before writing any code.</strong> To help you consider your design, please look over the questions in the <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell_design.txt" rel="nofollow">design document</a>. If you do not do this, you may discover that you need to rewrite major portions of your code as you progress!

 <h2><a id="user-content-part-0-forkwait" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-0-forkwait" aria-hidden="true"></a>Part 0: fork()/wait()</h2>

 In this phase of the project, you will learn about the <tt>fork()</tt> and <tt>wait()</tt> system calls that you will use in the rest of the project.

 <h4><a id="user-content-part-01-reading" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-01-reading" aria-hidden="true"></a>Part 0.1: Reading</h4>

 <a href="http://pages.cs.wisc.edu/~remzi/OSTEP/cpu-api.pdf" rel="nofollow">Sections 5.4 and 5.6 of OSTEP</a> may be helpful to read before starting this project. You may also wish to consult the class resources (e.g. on C programming and shell usage) before starting.

 <h4><a id="user-content-part-02-fibonacci" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-02-fibonacci" aria-hidden="true"></a>Part 0.2: Fibonacci</h4>

 Update fib.c so that if invoked on the command line with some integer argument n, where n is less than or equal to 13, it recursively computes the nth Fibonacci number.

 To ensure that you learn about <tt>fork()</tt>/<tt>wait()</tt>, there are restrictions on how your <tt>fib</tt> program must be written. The full rules are below, but the general idea is that the program will be written in a recursive manner, and each recursive call must be made by a new process (i.e. by calling <tt>fork()</tt> followed by <tt>doFib()</tt>). The child then returns its result to the parent, which waits until the child is done.

 Example outputs:

 <pre class="language-" data-role="codeBlock" data-info="">unix&gt; fib 32unix&gt; fib 1055</pre>

 Your fib program must conform to the following rules:

 <ul>

  <li>The output when given an argument <tt>n</tt> between 0 and 13 (inclusive) must be the <tt>n</tt>-th Fibonacci number.</li>

  <li>Fibonacci numbers must be computed recursively, with each recursive call occurring in a new process.</li>

  <li>The final result must be printed by the original process.</li>

  <li>You are allowed to modify the body of <tt>doFib()</tt>.</li>

  <li>You must <strong>not</strong> modify the number of parameters or return values of <tt>doFib()</tt>.</li>

  <li>You are allowed to create helper methods, as long as the computation of the Fibonacci number is done through creation of child processes.</li>

  <li>If given invalid arguments, your <tt>fib</tt> program should print the usage message and exit.</li>

  <li>Your program must not create a fork bomb when run. Any fork bomb behavior will result in a zero for this part of the project.</li>

  <li>Your output must <strong>exactly</strong> match the examples given above!</li>

 </ul>

 <h2><a id="user-content-part-1-shell-skeleton" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-1-shell-skeleton" aria-hidden="true"></a>Part 1: Shell Skeleton</h2>

 In this part of the assignment, you will start building the basic framework of your shell. At the end of this section, you should have a basic functioning shell framework, which you will extend and upgrade in future sections.

 Your basic shell will be called <tt>utcsh</tt><sup id="user-content-a1"><a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#utcshname">1</a></sup>.

 Note: Parts 1 and 2 will walk you through a recommended implementation order for the shell. You are not required to implement everything in this order, however, you must implement all functionality in both parts to receive full credit.

 <strong>Remember to read this entire document before implementing anything!</strong>

 <h4><a id="user-content-part-11-reading" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-11-reading" aria-hidden="true"></a>Part 1.1: Reading</h4>

 Before you implement anything, you should read this entire document, as well as the design document template. Yes, that is a <strong>lot</strong> of reading. Yes, you should do it anyways (at least skim the documents!).

 No additional external reading is required, though if you have not worked with command line interfaces before, you may wish to read Ubuntu’s <a href="https://ubuntu.com/tutorials/command-line-for-beginners" rel="nofollow">command line tutorial</a>

 You may also find it helpful to read the manpages for <tt>strtok</tt>, <tt>strcmp</tt>, and <tt>execv</tt>, though this will not be required until later.

 <h4><a id="user-content-part-12-repl" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-12-repl" aria-hidden="true"></a>Part 1.2: REPL</h4>

 The core of any shell is the REPL, or the <em>read-evaluate-print loop</em>. This is a loop that does the following three actions repeatedly:

 <ol>

  <li><strong>Read</strong> input from the user (or from <em>script</em> the user specifies).</li>

  <li><strong>Evaluate</strong> the input, figuring out what the user wants to do and doing it.</li>

  <li><strong>Print</strong> any output associated with the requested action.</li>

 </ol>

 Implement a REPL in the <tt>main()</tt> function in <tt>utcsh.c</tt>. Print <tt>utcsh&gt; </tt>at the start of the line, then read the user’s input.

 For now, your REPL should ignore most inputs. The only command it will respond to is the built-in command <tt>exit</tt>, which will cause the shell to exit by calling <tt>exit(0)</tt>. You should also call <tt>exit(0)</tt> if you reach the end-of-file while reading input.

 For reading lines of input, you should use <tt>getline()</tt>. Use <tt>man getline</tt> to learn more about this function.

 &#x1f41a; An interesting point is that, in C, 0 is false and nonzero is true, while in the world of UNIX exit codes, 0 indicates success and nonzero indicates failure. This turns out to be very useful, but can be a bit hard to keep track of when you’re initially learning how to work with shells.

 <h4><a id="user-content-part-13-parsing-and-built-in-commands" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-13-parsing-and-built-in-commands" aria-hidden="true"></a>Part 1.3: Parsing and Built-in Commands</h4>

 Recall from the introduction that a <em>command line</em> consists of ASCII words separated by space. Implement some way to split the command line so that you can recover these words, e.g. you should be able to immediately tell that the 4th word of <tt>"path a b c d e"</tt> is <tt>"d"</tt>.

 We recommend that you use <tt>strtok()</tt> for this. Read the manpage for this function <strong>carefully</strong>. Careless use of this function has been known to lead to many hours of debugging.

 Expand your shell’s ability to process built-in commands by adding error checking to <tt>exit</tt> and implementing two new built-in commands:

 <ul>

  <li><tt>exit</tt>: You implemented this built-in in the last section. Now add error handling: It is an <strong>error</strong> to pass any arguments to <tt>exit</tt>. See the next section (1.4) for details about how to handle errors.</li>

  <li><tt>cd</tt>: <tt>cd</tt> always takes exactly one argument (any other number is an error). This should call the <tt>chdir()</tt> system call with the user-supplied argument. If the <tt>chdir</tt> fails, that is also an error.</li>

  <li><tt>path</tt>: the <tt>path</tt> command takes zero or more arguments, with each argument separated by whitespace from the others. A typical usage might look like this:<pre class="language-" data-role="codeBlock" data-info="">utcsh&gt; path /bin /usr/bin</pre>This command will be used in Part 2.1–for now, just worry about being able to separate the arguments of this command without crashing.</li>

 </ul>

 <h4><a id="user-content-part-14-handling-errors" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-14-handling-errors" aria-hidden="true"></a>Part 1.4: Handling Errors</h4>

 The previous section has our first encounter with errors. For ease of implementation, your shell will only ever have one error message: “An error has occurred”.

 Whenever an error occurs, your shell should print the error message on <tt>stderr</tt> and continue. The only time your shell should exit in response to an error is described in Part 1.6. <sup id="user-content-a2"><a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#writecall">2</a></sup>

 An example snippet for how to print the error is given below. If the snippet does not meet your needs, you should write your own function:

 <pre class="language-" data-role="codeBlock" data-info="">  char emsg[30] = "An error has occurred
";  int nbytes_written = write(STDERR_FILENO, emsg, strlen(emsg));  if(nbytes_written != strlen(emsg)){    exit(2);  // Shouldn't really happen -- if it does, error is unrecoverable  }</pre>

 <strong>It is never acceptable to crash, segfault, or otherwise break the shell in response to bad user input</strong>. Your shell must always exit gracefully, i.e. by calling <tt>exit()</tt> or returning from <tt>main()</tt>.

 &#x1f41a; Of course, most real world shells implement a huge variety of error messages to help the user figure out where something went wrong.

 <h4><a id="user-content-part-15-executing-external-commands" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-15-executing-external-commands" aria-hidden="true"></a>Part 1.5: Executing External Commands</h4>

 If the command given is not one of the three built-in commands, it should be treated as the path to an external executable program.

 For these external commands, execute the program using the fork-and-exec method discussed in class. Here are some hints to help you out:

 <strong>For the child process</strong>: The child process must execute the given command by using the <tt>execv()</tt> call. <strong>You may not call <tt>system()</tt> to run a command</strong>. Remember that if <tt>execv()</tt> returns, there was an error (usually caused by incorrect arguments or the file not existing).

 <strong>For the parent process</strong>: The parent should use <tt>wait()</tt> or <tt>waitpid()</tt> to wait on the child. Note that the parent <strong>does not care</strong> about what happens to the child. As long as <tt>fork()</tt> succeeds, the parent considers the process launch to have been a success.

 &#x1f41a; Typical shells will collect the exit code of the child to communicate information to the programmer. For example, the exit code of the <tt>diff</tt> program can tell you not just whether two files were the same, but <strong>how</strong> they differed. For simplicity, <tt>utcsh</tt> does not worry about this.

 <h4><a id="user-content-part-16-reading-a-script" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-16-reading-a-script" aria-hidden="true"></a>Part 1.6: Reading A Script</h4>

 Sometimes, it is very annoying to have to type in commands one at a time. One common solution for this is to create a <em>script</em> by putting a related sequence of commands into a file and using the shell to run that file.

 Implement a <em>script</em> system: if <tt>utcsh</tt> is invoked with one argument, instead of reading commands from <tt>stdin</tt>, it assumes that its argument is a filename and attempts to read commands one at a time from that file instead of from <tt>stdin</tt>.

 You can find example scripts in the <tt>examples/</tt> directory. <tt>say_hello.utcsh</tt> is the most basic script and consists of a bunch of external commands There is also the more advanced <tt>say_hello_path.utcsh</tt>, which relies on the path feature (which you will implement in 2.1).

 There are two other important changes when operating in script mode:

 <ul>

  <li>The <tt>utcsh&gt; </tt>prompt should not be printed in script mode.</li>

  <li>If the input file is invalid, or there is more than one argument, <tt>utcsh</tt> should print an error message and exit with an error code, i.e. call <tt>exit(1)</tt>. This is the only situation in which an error should cause <tt>utcsh</tt> to exit.</li>

 </ul>

 Note that until you finish this section, you will not be able to run the automated test suite. Once you have finished this section, you may check Section 4 for details on running the tests.

 &#x1f41a; To show you what a script looks like for bash, we’ve included two bash scripts in the examples directory. One does the same thing as the say_hello scripts and can be run with <tt>bash examples/say_hello.bash</tt>. The other can be run with <tt>bash examples/file_exists.bash &lt;filename&gt;</tt> and will tell you whether <tt>&lt;filename&gt;</tt> exists, and if so, if it is a regular file or a directory.

 At this point, you have a basic shell that can run both built-in and external commands, both from a script and from stdin (keyboard input)–for example, you should be able to run the <tt>say_hello.utcsh</tt> script in the <tt>examples</tt> directory.

 Now might be a good time to make a git commit, if you haven’t done so already!

 <h2><a id="user-content-part-2-advanced-shell-features" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-2-advanced-shell-features" aria-hidden="true"></a>Part 2: Advanced Shell Features</h2>

 <h4><a id="user-content-part-21-paths" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-21-paths" aria-hidden="true"></a>Part 2.1: Paths</h4>

 When you implemented external program execution, you assumed that the 0-th argument was the path to an executable file. Unfortunately, this is annoying for users, because nobody wants to type <tt>/usr/local/bin/ls</tt> every time they want to run the <tt>ls</tt> command.

 The solution to this is a <tt>PATH</tt>: a set of user-specified directories to search for external programs. When the shell is given a command it does not recognize, it looks for this program in its <tt>PATH</tt>.

 Note that, for the rest of this document, “path” will refer to a string with slashes in it which is used to locate a file, while <tt>PATH</tt> will be used to refer to a list of paths used to search for binary files. <sup id="user-content-a3"><a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#pathpath">3</a></sup>

 If the program you’re given is not an <em>absolute path</em>, i.e. a path which starts from <tt>/</tt>, you should search for your program in each directory in the <tt>PATH</tt>. For example, if your <tt>PATH</tt> is <tt>"/bin"</tt> <tt>"/usr/bin"</tt>, you would search for <tt>/bin/ls</tt> and <tt>/usr/bin/ls</tt>, executing the first one you found (and returning an error if neither exists). You can check that the file exists and is executable using the functions we provide in the skeleton code. If the file does not exist, or it is not executable, this is an error.

 The user can set the <tt>PATH</tt> with the <tt>path</tt> command. Each argument to the <tt>path</tt> corresponds to an entry in the shell’s <tt>PATH</tt>. The <tt>path</tt> command completely overwrites the existing <tt>PATH</tt>–it does not append entries. If the PATH is empty because the user executed a <tt>path</tt> command with no arguments, <tt>utcsh</tt> cannot execute <strong>any</strong> external programs unless the full path to the program is provided.

 A variable for the <tt>PATH</tt> is already provided for you in the skeleton code, called <tt>shell_paths</tt>. You can manipulate this variable directly, or by using the helper functions in <tt>util.c</tt>/<tt>util.h</tt>.

 &#x1f41a; Real shells also let you specify <em>relative paths</em> to programs, e.g. you can type <tt>bin/myprog</tt> to run a program relative to your current working directory. You do not need to worry about this for utcsh: the program name will either be an absolute path or the name of a program to be searched for in <tt>shell_paths</tt>.

 <strong>Reminder: the shell itself does not implement <tt>ls</tt> or any other program–it simply looks them up in the path and executes them.</strong>

 <h4><a id="user-content-part-22-redirection" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-22-redirection" aria-hidden="true"></a>Part 2.2: Redirection</h4>

 Many times, a shell user prefers to send the output of a program to a file rather than to the screen. Usually, a shell provides this nice feature with the <tt>&gt;</tt> character. Formally this is called <em>redirection</em> of output. Your shell should include this feature.

 For example, if a user types <tt>ls -al /tmp &gt; output</tt>, nothing should be printed to the screen. Instead, the standard output and standard error of the program should be rerouted to the file <tt>output</tt>.

 If the output file already exists, you should overwrite and truncate it. Look through the flags in <tt>man 2 open</tt> to find out how to do this.

 Here are some rules about the redirection operator:

 <ul>

  <li>Multiple redirects in a command are an error, e.g. <tt>ls &gt; file1 &gt; file2</tt>.</li>

  <li>A redirect without a corresponding command is an error, e.g. <tt>&gt; file1</tt>.</li>

  <li>A redirect without a corresponding file is an error, e.g. <tt>ls &gt;</tt></li>

  <li>There will always be spaces around a redirect, e.g. <tt>ls&gt;file1</tt> is requesting command execution of a file called <tt>ls&gt;file1</tt>, not a redirection.</li>

  <li>You do not need to worry about redirection for built-in commands, e.g. we will not test what happens when you type <tt>path /bin &gt; file</tt>.</li>

 </ul>

 &#x1f41a; Real shells usually allow multiple redirects and redirect <tt>stdout</tt> and <tt>stderr</tt> separately, and allow you to redirect them to each other, e.g. you can direct stdout into stderr.

 <h4><a id="user-content-part-23-concurrent-commands" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-23-concurrent-commands" aria-hidden="true"></a>Part 2.3: Concurrent Commands</h4>

 Your shell will allow the user to launch concurrent commands. Remember: when two things are <em>concurrent</em>, they appear to execute at the same time whether they actually run simultaneously or not (<em>logical parallelism</em>). In UTCSH, this is accomplished with the ampersand operator:

 <pre class="language-" data-role="codeBlock" data-info="">utcsh&gt; cmd1 &amp; cmd2 &amp; cmd3 args1</pre>

 Instead of running <tt>cmd1</tt>, waiting for it to finish, and then running <tt>cmd2</tt>, your shell should run <tt>cmd1</tt>, <tt>cmd2</tt>, and <tt>cmd3</tt> (with whatever args were passed) <strong>before</strong> waiting for any of them to complete.

 Then, once all processes have been started, you must use <tt>wait()</tt> or <tt>waitpid()</tt> to make sure that <strong>all</strong> processes have completed before moving on.

 Each individual command may optionally have its own redirection, e.g.

 <pre class="language-" data-role="codeBlock" data-info="">utcsh&gt; cmd1 &gt; file1 &amp; cmd2 arg1 arg2 &gt; file2 &amp; cmd3 &gt; file3</pre>

 Unlike the redirection operator, the ampersand operator might not have spaces around it. For example <tt>cmd1 arg1&amp;cmd2 &gt; file2</tt> is a valid command line, and requests the execution of two commands. In addition, some or all of the commands on either side of the ampersand may be blank. This means that, for example, <tt>&amp;&amp;&amp;&amp;&amp;&amp;&amp;</tt> is a valid command line.

 As you process these commands, there are a number of special cases to consider. In doing so, you may assume the following:

 <ul>

  <li>If a command line has multiple concurrent commands that are all external, the current spec applies.</li>

  <li>If a command line has multiple concurrent commands that are all built-in, the shell should execute them sequentially from left-to-right.</li>

  <li>You may assume that we will not test command lines that have mixed concurrent external/internal built-in commands. Your shell should not crash if this happens, but otherwise, there are no requirements on what it must do.</li>

 </ul>

 &#x1f41a; In most bash-like shells, <tt>&amp;</tt> is actually appended to the end of a command to instruct it to <em>run in the background</em>. You can search for “Bash Job Control” if you want to learn more, but don’t try to use this syntax in your actual shell to run jobs in parallel, or weird things might happen!

 <h2><a id="user-content-part-3-hints" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-3-hints" aria-hidden="true"></a>Part 3: Hints</h2>

 <h3><a id="user-content-general-hints" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#general-hints" aria-hidden="true"></a>General Hints</h3>

 <ul>

  <li>Remember that C does not have strings in the same way that Java does–you will need to be careful about string handling. You can read more about string handling in <a href="http://www.eskimo.com/~scs/cclass/notes/sx8.html" rel="nofollow">these notes</a>. For a refresher on general C principles, please see our <a href="https://docs.google.com/document/d/1c3PF8fE7jBFzrBx-HqvkvlPDqWh6u99bdpmCya3RwNU/edit?usp=sharing" rel="nofollow">guide to C basics</a></li>

  <li>Always, <strong>always</strong> check the return codes of all system calls, from the very beginning of your work. This will often catch mistakes in how you’re using these functions.</li>

  <li>USE GIT. Make a commit every time you have working code, or have implemented a small part of a milestone, not just when you need to get the current version to your partner. Committing more frequently lets you try things out much more easily, since it’s easy to revert changes if you screw things up.</li>

  <li>For more information on using git, check our our <a href="https://docs.google.com/document/d/1WRGVUwYcXOjTsgp0jXkfaq_9wrkjx_81BXa2t_kw2oI/edit?usp=sharing" rel="nofollow">guide to version control and git</a>. In this class, we’ll be using the UTCS GitLab server. For help getting started, check out our <a href="https://utexas.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=26f07913-3137-497f-a4db-ae29003dabfe" rel="nofollow">guide to getting started with UTCS GitLab</a>.</li>

  <li>You are allowed to modify <em>any</em> file you want in this project. You don’t need to ask for permission, or leave a note for us, or say anything on Canvas, just do it! However, note that we use our own copy of tests (any files present under the <tt>tests</tt> directory), so any changes you make to the test cases or testing framework will be reverted before we grade.</li>

  <li>Errors can be debugged with <tt>printf</tt> and <tt>gdb</tt>. For general debugging help, check out our <a href="https://docs.google.com/document/d/1SzvPr9WHrxH7FEc2FHno5OPSKBnHzVP4nFpyYWZECqY/edit?usp=sharing" rel="nofollow">debugging FAQ for CS 439</a>.</li>

 </ul>

 <h3><a id="user-content-hints-for-part-0" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#hints-for-part-0" aria-hidden="true"></a>Hints for Part 0</h3>

 <ul>

  <li>The <tt>waitpid()</tt>, <tt>fork()</tt>, and <tt>exit</tt> functions will come in handy. Use <tt>man</tt> to learn about them. Remember, you can use <tt>man man</tt> to learn about <tt>man</tt>.</li>

  <li>The <tt>WEXITSTATUS</tt> macro described in the <tt>waitpid</tt> manpage may be useful.</li>

 </ul>

 <h3><a id="user-content-hints-for-part-1" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#hints-for-part-1" aria-hidden="true"></a>Hints for Part 1</h3>

 <ul>

  <li>A real concern in any text processing program in C how much memory to allocate for text handling. In order to simplify your shell implementation, you are allowed to limit the size of your inputs according to the macros defined in <tt>util.h</tt>. When interpreting these limits, remember that a command line may consist of multiple commands.If the input violates these limits, you may print the error message and continue processing. <strong>Do not crash the shell</strong> if these limits are violated.It is possible to write the shell in a way that these limits are not needed, but it is slightly more challenging.</li>

  <li>Think <strong>carefully</strong> about how you design your tokenization routines. Right now, you only have to deal with one command. In Part 2, you’re going to deal with multiple commands, possibly each with their own redirects, and each of which can error independently of the others. Make sure your design can grow to accommodate this.A good basic design is to allocate an array of <tt>char*</tt>, then use <tt>strtok</tt> to fill it up one element at a time. At the end of this procedure, <tt>array[0]</tt> should be the 0-th argument, <tt>array[1]</tt> should be the 1st, and so on. You should then store this information in a way that allows multiple copies (i.e. <em>not</em> in a global structure, which tends to be a bad idea anyways).</li>

  <li>Be <strong>extremely careful</strong> about doing <tt>a == b</tt> or <tt>a = b</tt> when <tt>a</tt> and <tt>b</tt> are <tt>char*</tt>. This likely does <strong>not</strong> do what you think it does. In order to do the operations, look into <tt>strcmp()</tt>, <tt>strcpy()</tt>, and <tt>strncpy()</tt> in <tt>string.h</tt>.</li>

 </ul>

 <h3><a id="user-content-hints-for-part-2" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#hints-for-part-2" aria-hidden="true"></a>Hints for Part 2</h3>

 <ul>

  <li>Output redirection can be achieved by using a combination of <tt>open()</tt> and <tt>dup2()</tt>. Check the man pages for more details. You should make these calls after the child process has forked, but before the call to <tt>execv()</tt>. Check <a href="https://www.cs.utexas.edu/~theksong/2020/243/Using-dup2-to-redirect-output/" rel="nofollow">https://www.cs.utexas.edu/~theksong/2020/243/Using-dup2-to-redirect-output/</a> for an example of <tt>dup2()</tt> usage.</li>

  <li>If you’ve been using the recommended functions so far, you might need to add a new function or data structure to make concurrent commands work easily.</li>

  <li>Don’t be afraid to modify the skeleton code. We are <strong>not</strong> checking that your skeleton code is unmodified, we’re checking that your program works and is well-written. If you have to modify, add to, or remove from the skeleton to achieve this, do it!</li>

 </ul>

 <h3><a id="user-content-line-count-hints" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#line-count-hints" aria-hidden="true"></a>Line Count Hints</h3>

 We are providing the rough number of lines of code used in the reference solution as a rough hint for you, so you can see how much work is needed for each function. <strong>These numbers have been rounded to the nearest multiple of 10.</strong>

 <table>

  <thead>

   <tr>

    <th>Function</th>

    <th>Lines of Code</th>

   </tr>

  </thead>

  <tbody>

   <tr>

    <td><tt>tokenize_command_line</tt></td>

    <td>50 lines</td>

   </tr>

   <tr>

    <td><tt>parse_command</tt></td>

    <td>60 lines</td>

   </tr>

   <tr>

    <td><tt>eval</tt></td>

    <td>60 lines</td>

   </tr>

   <tr>

    <td><tt>try_exec_builtin</tt></td>

    <td>60 lines</td>

   </tr>

   <tr>

    <td><tt>exec_external_cmd</tt></td>

    <td>30 lines</td>

   </tr>

   <tr>

    <td><tt>main</tt></td>

    <td>50 lines</td>

   </tr>

  </tbody>

 </table>

 <h2><a id="user-content-part-4-checking-your-work" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-4-checking-your-work" aria-hidden="true"></a>Part 4: Checking Your Work</h2>

 To help you check your work, we’ve provided a small test suite, along with some tools to help you run it.

 Each test in the test suite will check three things from your shell:

 <ul>

  <li>The exit code</li>

  <li>The standard output</li>

  <li>The standard error</li>

 </ul>

 If any of these differ, the test suite will print an error and tell you what part of the output was wrong, along with commands you can run to see the difference.

 In order to make this easier on you, we’ve included some helper rules in the Makefile to let you run tests easily.

 <ul>

  <li>To run the full testsuite, run <tt>make check</tt>.</li>

  <li>To run an individual test, run <tt>make testcase id=#</tt>, e.g. <tt>make testcase id=15</tt>.</li>

  <li>To get a description of a test, run <tt>make describe id=#</tt>. This can be useful if you’re not sure what a test does or want to get commands to run it yourself (e.g. to run it under a debugger)</li>

 </ul>

 No test should run for more than 10 seconds without either passing or failing. If your test runs for longer than this, you likely have an infinite loop in your code.

 In general, you should not look directly at the test files themselves unless you want to understand the test suite or modify the tests. If you want to run the command that the test runs, use <tt>make describe</tt>.

 <h2><a id="user-content-part-5-on-programming-and-logistics" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#part-5-on-programming-and-logistics" aria-hidden="true"></a>Part 5: On Programming and Logistics</h2>

 <h3><a id="user-content-makefile" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#makefile" aria-hidden="true"></a>Makefile</h3>

 Your code will be tested and graded with the output of <tt>make utcsh</tt> or <tt>make</tt> (the two rules are equivalent in the provided Makefile). To aid you in debugging, two additional rules have been created in the makefile:

 <ul>

  <li><tt>make debug</tt> will create a binary which is not heavily-optimized and has more debugging information than the default build. If you want to feed your program into a debugger like <tt>gdb</tt>, <tt>valgrind</tt>, or <tt>rr</tt>, you should use this rule to generate it.</li>

  <li><tt>make asan</tt> will create a binary with <em>sanitizers</em>. Think of these as extra error checking code that the compiler adds to the program for you. When you run a program that has been compiled with sanitizers, the binary itself will warn you about memory leaks, invalid pointer dereferences, and other such issues.We do not enable the sanitizers by default because they can turn an otherwise-correct program into an incorrect one, e.g. if your program is correct except for a small memory leak, the sanitized binary will still exit with an error.</li>

 </ul>

 You may use these rules to quickly generate programs for debugging, but keep in mind that your grade will be based on the binary generated by <tt>make utcsh</tt>.

 <h3><a id="user-content-design-document" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#design-document" aria-hidden="true"></a>Design Document</h3>

 As part of this project, you will submit a <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell_design.txt" rel="nofollow">design document</a>, where you will describe your design to us. Please note that this document is a set of questions that you will answer and is not free form. Your group will submit one design document.

 <h3><a id="user-content-general" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#general" aria-hidden="true"></a>General</h3>

 <ol>

  <li>You must work in two-person teams on this project. Failure to do so will result in a 0 for the project. Once you have contacted your assigned partner, do the following:

   <ol>

    <li>exchange first and last names, EIDs, and CS logins</li>

    <li>fill out the README.shell distributed with the project</li>

    <li>register in Canvas as a Shell Group. (Add yourselves to an empty group of your choosing. Feel free to change the name to something more creative! Keep it clean.)</li>

    <li>Create a private GitLab repo and invite your partner at at least “maintainer” level. See our <a href="https://docs.google.com/document/d/1WRGVUwYcXOjTsgp0jXkfaq_9wrkjx_81BXa2t_kw2oI/edit#heading=h.3fguf535xdp" rel="nofollow">git and version control guide</a> for details on how to do this.</li>

   </ol>You must follow the <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/pairprogramming.html" rel="nofollow">pair programming guidelines</a> set forth for this class. If you have not registered a group by the group registration deadline, we will assign you to a group.<strong>Please see the <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/GradingCriteria.html" rel="nofollow">Grading Criteria</a> to understand how failure to follow the pair programming guidelines OR fill out the README.shell will affect your grade.</strong></li>

  <li>You must follow the guidelines laid out in the <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/CStyleGuide.html" rel="nofollow">C Style Guide</a> or you will lose points. This includes selecting reasonable names for your files and variables.</li>

  <li>This project will be graded on the UTCS public linux machines. Although you are welcome to do testing and development on any platform you like, we cannot assist you in setting up other environments, and you must test and do final debugging on the UTCS public linux machines. The statement “It worked on my machine” will not be considered in the grading process.</li>

  <li>The execution of your solution shell will be evaluated using the test cases that are included in your project directory. To receive credit for the test cases, your shell should pass the provided test case, as determined by <tt>make clean &amp;&amp; make utcsh &amp;&amp; make check</tt>.</li>

  <li>Your code <strong>must</strong> compile without any additions or adjustments, or you will receive a 0 for the test cases portion of your grade.</li>

  <li>Do not use <tt>_exit()</tt> for this assignment–use <tt>exit()</tt> instead.</li>

  <li>You are encouraged to not use linux.cs.utexas.edu for development. Instead, please find another option using the department’s <a href="https://apps.cs.utexas.edu/unixlabstatus/" rel="nofollow">list of public UNIX hosts</a>.</li>

  <li>You are encouraged to reuse <strong>your own</strong> code that you might have developed in previous courses to handle things such as queues, sorting, etc. You are also encouraged to use code provided by a public library such as the GNU library.</li>

  <li>You may not look at the written work of any student other than your partner. This includes, for example, looking at another student’s screen to help them debug or looking at another student’s print-out. See the syllabus for additional details.</li>

  <li>If you find that the problem is under specified, please make reasonable assumptions and document them in the README.shell file. Any clarifications or revisions to the assignment will be posted to EdStem.</li>

 </ol>

 <h3><a id="user-content-submitting-your-work" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#submitting-your-work" aria-hidden="true"></a>Submitting Your Work</h3>

 <ol>

  <li>After you finish your code, use <tt>make turnin</tt> to submit a compressed tarball named <tt>turnin.tar.gz</tt> for submission. It may be a good idea to unpack this tarball into a clean directory on a UTCS linux system to make sure it still compiles. You should then upload the file to the Project 0 Test Cases assignment on Canvas. Make sure you have included the necessary information in the README.shell and placed your pair programming log in the project directory.</li>

  <li>Once you have completed your design document, please submit it to the Project 0 Design and Documentation assignment in Canvas. Make sure you have included your name, CS login, and UT EID in the design document.The purpose of the design document is to explain and defend your design to us. Its grade will reflect both your answers to the questions and the correctness and completeness of the implementation of your design. It is possible to receive partial credit for speculating on the design of portions you do not implement, but your grade will be reduced due to the lack of implementation.</li>

 </ol>

 <h3><a id="user-content-grading" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#grading" aria-hidden="true"></a>Grading</h3>

 Code will be evaluated based on its correctness, clarity, and elegance according to the <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/GradingCriteria.html" rel="nofollow">Grading Criteria</a>. Strive for simplicity. Think before you code.

 The most important factor in grading your code design and documentation will be code inspection and evaluation of the descriptions in the write-ups. Remember, if your code does not follow the standards, it is wrong. If your code is not clear and easy to understand, it is wrong.

 <h2><a id="user-content-footnotes" class="anchor" href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#footnotes" aria-hidden="true"></a>Footnotes</h2>

 Project adapted from one used in OSTEP. Many thanks to the Drs. Arpaci-Dusseau for permission to use their work.

 <b id="user-content-utcshname">[1]:</b> This is both an homage to the UTCS department and a play on the name of the popular <a href="https://en.wikipedia.org/wiki/Tcsh" rel="nofollow"><tt>tcsh</tt> shell</a>. <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#a1">&#x21a9;</a>

 <b id="user-content-writecall">[2]:</b> Note that we check the return value of the write call in spite of the fact that all we can do if it’s wrong is exit. This is good programming practice, and you should be sure to always check the return codes of any system or library call that you make. <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#a2">&#x21a9;</a>

 <b id="user-content-pathpath">[3]:</b> Sometimes you hear <tt>PATH</tt> referred to as “<strong>the</strong> path,” but in most real-world contexts, you will need to deduce which one is meant from context. <a href="https://www.cs.utexas.edu/~ans/classes/cs439/projects/shell_project/shell.html#a3">&#x21a9;</a>

</article>