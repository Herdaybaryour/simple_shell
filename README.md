This is a simple implementation of a UNIX command line interpreter. The shell can interpret and execute command line arguments read from the standard input. the shell read lines from a file or terminal line which is then interpreted and executed if the command is valid 
  
 # Requirements 
 All the files are to be compiled on an Ubuntu 14.04 LTS machine with: gcc -Wall -Werror -Wextra -pedantic *.c 
 All files ends end with a new line, with no memory leaks 
 All code will use the Betty style. It will be checked using betty-style.pl and betty-doc.pl 
 All code will be tested using the test files in the test folder. 
 The simple shell supports most shell commands, such as cat, pwd, ls -la and more. 
 Return Value : 
 The shell returns a value of 0 if the command is valid and the command is executed successfully. 
  
 # Output 📁 
 The program must have the exact same output as sh (/bin/sh) as well as the exact same error output. 
 The only difference is when you print an error, the name of the program must be equivalent to the argv[0] 
 Usage 
 # List of fucntions and system calls used 
 - access (man 2 access) 
 - chdir (man 2 chdir) 
 - close (man 2 close) 
 - closedir (man 3 closedir) 
 - execve (man 2 execve) 
 - exit (man 3 exit) 
 - _exit (man 2 _exit) 
 - fflush (man 3 fflush) 
 - fork (man 2 fork) 
 - free (man 3 free) 
 - getcwd (man 3 getcwd) 
 - getline (man 3 getline) 
 - isatty (man 3 isatty) 
 - kill (man 2 kill) 
 - malloc (man 3 malloc) 
 - open (man 2 open) 
 - opendir (man 3 opendir) 
 - perror (man 3 perror) 
 - read (man 2 read) 
 - readdir (man 3 readdir) 
 - signal (man 2 signal) 
 - stat (__xstat) (man 2 stat) 
 - lstat (__lxstat) (man 2 lstat) 
 - fstat (__fxstat) (man 2 fstat) 
 - strtok (man 3 strtok) 
 - wait (man 2 wait) 
 - waitpid (man 2 waitpid) 
 - wait3 (man 2 wait3) 
 - wait4 (man 2 wait4) 
 - write (man 2 write) 
  
 # Compilation 
 The shell will be compiled this way: gcc -Wall -Werror -Wextra -pedantic -std=gnu89 *.c -o hsh 
  
 # Testing 
 The shell works like this in interactive mode: 
  
 $ ./hsh 
  ($) /bin/ls 
  hsh main.c shell.c 
  ($) 
  ($) exit 
 $ 
  
 But also in non-interactive mode: 
  
 $ echo "/bin/ls" | ./hsh 
 hsh main.c shell.c test_ls_2 
 $ 
 $ cat test_ls_2 
  /bin/ls 
  /bin/ls 
 $ 
 $ cat test_ls_2 | ./hsh 
  hsh main.c shell.c test_ls_2 
  hsh main.c shell.c test_ls_2 
 $ 
 ## Mandatory Tasks 
 # 0. Betty would be proud 
 Write a beautiful code that passes the Betty checks 
  
 # 1. Simple shell 0.1 
 Write a UNIX command line interpreter. 
  
 Usage: simple_shell Your Shell should: 
  
 Display a prompt and wait for the user to type a command. A command line always ends with a new line. The prompt is displayed again each time a command has been executed. The command lines are simple, no semicolons, no pipes, no redirections or any other advanced features. The command lines are made only of one word. No arguments will be passed to programs. If an executable cannot be found, print an error message and display the prompt again. Handle errors. You have to handle the “end of file” condition (Ctrl+D) You don’t have to: 
  
 use the PATH implement built-ins handle special characters : ", ', `, \, *, &, # be able to move the cursor handle commands with arguments execve will be the core part of your Shell, don’t forget to pass the environ to it… 
  
 # 3. Simple shell 0.3 
 Simple shell 0.2 + 
  
 Handle the PATH fork must not be called if the command doesn’t exist 
  
 # 4. Simple shell 0.4 
 Simple shell 0.3 + 
  
 Implement the exit built-in, that exits the shell Usage: exit You don’t have to handle any argument to the built-in exit 
  
 # 5. Simple shell 1.0 
 Simple shell 0.4 + 
  
 Implement the env built-in, that prints the current environment 
  
 end of mandatory 
  
 Advanced Tasks 
 # 6. Simple shell 0.1.1 
 Simple shell 0.1 + 
  
 Write your own getline function 
 Use a buffer to read many chars at once and call the least possible the read system call 
 You will need to use static variables 
 You are not allowed to use getline 
 You don't have to: 
  
 be able to move the cursor 
 # 7. Simple shell 0.2.1 
 Simple shell 0.2 + 
  
 You are not allowed to use strtok 
 # 8. Simple shell 0.4.1 
 Simple shell 0.4 + 
  
 handles arguments for a built-in exit 
 Usage: exit status, where status is an integer used to exit the shell 
 julien@ubuntu:~/shell$ ./shell_0.4.1 
 $ exit 98 
 julien@ubuntu:~/shell$ echo $? 
 98 
 julien@ubuntu:~/shell$ 
  
 # 9. setenv, unsetenv 
 Simple shell 1.0 + 
  
 Implement the setenv and unsetenv builtin commands 
  
 setenv 
 initialize a new environment variable, or modify an existing one 
 Command syntax: setenv VARIABLE VALUE 
 Should print something on stderr on failure 
 unsetenv 
 Remove an environment variable 
 Command syntax: unsetenv VARIABLE 
 Should print something on stderr on failure 
 # 10. cd 
 Simple sell 1.0 + 
  
 Implement the builtin command cd: 
  
 Changes the current directory of the process 
 Command syntax: cd [DIRECTORY] 
 If no argument is given to cd the command must be interpreted like cd $HOME 
 You have to handle the command cd - 
 You have to update the environment variable PWD when you change directory 
 man chdir, man getcwd 
  
 # 11. ; 
 Simple shell 1.0 + 
  
 Handle the commands separator ; 
 alex@~$ ls /var ; ls /var 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 alex@~$ ls /hbtn ; ls /var 
 ls: cannot access /hbtn: No such file or directory 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 alex@~$ ls /var ; ls /hbtn 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 ls: cannot access /hbtn: No such file or directory 
 alex@~$ ls /var ; ls /hbtn ; ls /var ; ls /var 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 ls: cannot access /hbtn: No such file or directory 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 alex@~$ 
 # 12. && and || 
 Simple shell 1.0 + 
  
 Handle the && and || shell logical operators 
 alex@~$ ls /var && ls /var 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 alex@~$ ls /hbtn && ls /var 
 ls: cannot access /hbtn: No such file or directory 
 alex@~$ ls /var && ls /var && ls /var && ls /hbtn 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 ls: cannot access /hbtn: No such file or directory 
 alex@~$ ls /var && ls /var && ls /var && ls /hbtn && ls /hbtn 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 ls: cannot access /hbtn: No such file or directory 
 alex@~$ 
 alex@~$ ls /var || ls /var 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 alex@~$ ls /hbtn || ls /var 
 ls: cannot access /hbtn: No such file or directory 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 alex@~$ ls /hbtn || ls /hbtn || ls /hbtn || ls /var 
 ls: cannot access /hbtn: No such file or directory 
 ls: cannot access /hbtn: No such file or directory 
 ls: cannot access /hbtn: No such file or directory 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 alex@~$ ls /hbtn || ls /hbtn || ls /hbtn || ls /var || ls /var 
 ls: cannot access /hbtn: No such file or directory 
 ls: cannot access /hbtn: No such file or directory 
 ls: cannot access /hbtn: No such file or directory 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp 
 alex@~$ 
 # 13. alias 
 Simple shell 1.0 + 
  
 Implement the alias builtin command 
 Usage: alias [name[='value'] ...] 
 alias: Prints a list of all aliases, one per line, in the form name='value' 
 alias name [name2 ...]: Prints the aliases name, name2, etc 1 per line, in the form name='value' 
 alias name='value' [...]: Defines an alias for each name whose value is given. If name is already an alias, replaces its value with value 
 # 14. Variables 
 Simple shell 1.0 + 
  
 Handle variables replacement 
 Handle the $? variable 
 Handle the $$ variable 
 julien@ubuntu:~/shell$ ./hsh 
 $ ls /var 
 backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  snap  spool  tmp 
 $ echo $? 
 0 
 $ echo $$ 
 5104 
 $ echo $PATH 
 /home/julien/bin:/home/julien/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin 
 $ exit  
 julien@ubuntu:~/shell$  
 # 15. Comments 
 Simple shell 1.0 + 
  
 Handle comments (#) 
  
 julien@ubuntu:~/shell$ sh 
 $ echo $$ # ls -la 
 5114 
 $ exit 
 julien@ubuntu:~/shell$  
 # 16. File as input 
 Simple shell 1.0 + 
  
 ## Usage: simple_shell [filename] 
 Your shell can take a file as a command line argument 
 The file contains all the commands that your shell should run before exiting 
 The file should contain one command per line 
 In this mode, the shell should not print a prompt and should not read from stdin 
 # Contributors 👫 
  
 Adebayo Adebowale
  
 Christianah 613
