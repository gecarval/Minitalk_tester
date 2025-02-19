# Minitalk_tester
<p align="center">
	<img alt="GitHub code size in bytes" src="https://img.shields.io/github/languages/code-size/ailopez-o/42Barcelona-pushswap-prochecker?color=lightblue" />
	<img alt="Code language count" src="https://img.shields.io/github/languages/count/ailopez-o/42Barcelona-pushswap-prochecker?color=yellow" />
	<img alt="GitHub top language" src="https://img.shields.io/github/languages/top/ailopez-o/42Barcelona-pushswap-prochecker?color=blue" />
	<img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/ailopez-o/42Barcelona-pushswap-prochecker?color=green" />
</p>
The minitalk tester is a project made for testing the 42 Minitalk project, by sending multiple messages using interprocess comunication using bitwise operator to receive the messages from a client and signals `SIGUSR1` and `SIGUSR2` to send the data to the server.

In the project you are allowed to use several functions as write, printf, malloc, free and all the functions from the 42 libft. but in the essence of the project we get to know functions essential for UNIX systems interprocess comunication and understand how it works. For example
## signal()
`sighandler_t signal(int signum, sighandler_t handler);`

The signal function in the <signal.h> C library is a way to specify a function, called a signal handler, to be called when a specific signal is received by a running program. A signal is a message from a UNIX based operating system to a program indicating that some event has occurred. The signal function allows you to specify a function to be called when a particular signal is received, so that you can take some action in response to the signal.
``` C
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>

void signal_handler(int signum)
{
  printf("Received SIGINT!\n", signum);
  exit(0);
}

int main()
{
  // Set the signal handler for the SIGINT and SIGTERM signals
  // to the signal_handler function  signal(SIGINT, signal_handler);
  signal(SIGTERM, signal_handler);

  while (1)
  {
    ;// Do some work here...
  }
  return (42);
}
```
> [!NOTE]
> In the above C code we've redefined the Behavior of both `SIGINT` and `SIGTERM` that so when the user presses CTRL+C in the terminal wich causes the signal `SIGINT` to be sent to the process to act as defined by the function.
> With this we set behavior and examples of how can we proceed with certain UNIX signal, example a `SIGSEGV` which is the signal for a segmentation fault, and proceed in a especific way by the user than letting the program be handled by the operating system or leaving resources in an undefined state.

## kill()
`int kill(pid_t pid, int sig);`

The kill function is a system call that sends a signal to a process. As before stated is also defined in the signal.h header file. The pid argument specifies the process ID of the process you want to communicate with. The sig argument specifies the signal to be sent to the process.

There are various signals that can be sent, each corresponding to a different purpose. For example, the SIGKILL signal is used to terminate processes that are unresponsive or stuck in an infinite loop. Here is an example of using the kill function to terminate a process with the SIGKILL signal:
``` C
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

int main()
{
  pid_t pid = getpid();  // get the process ID of the current process
  int result = kill(pid, SIGKILL);  // send the SIGKILL signal to the process

  if (result == 0)
  {
    printf("Process terminated successfully.\n");
  }
  else
  {
    perror("Error terminating process");
  }
  return (42);
}
```
> [!NOTE]
> Using the kill function to terminate a process should generally be avoided, as it can leave resources allocated to the process in an undefined state. Instead, it is usually better to allow the process to terminate gracefully by providing it with an opportunity to clean up and release resources before exiting.

> [!WARNING]
> Sending signals to random PID's may cause issues in the operating system.

## getpid()
`pid_t getpid(void);`

In C, the getpid function returns the process ID of the current process. It is declared in the unistd.h header file. In an operating system, a process is an instance of a program that is being executed. A process ID (PID) is a unique identifier assigned to each process by the operating system when it is created.

Process IDs are useful for a variety of purposes in coding. Here are a few examples:Identifying and tracking processes: As mentioned earlier, the process ID is a unique identifier for a process, so it can be used to identify and track specific processes within the system.Sending signals to processes: The kill function in C allows you to send a signal to a process, and you can specify the process to send the signal to using the process ID. This can be useful for controlling and interacting with processes from your code.Process communication: Process IDs can be used as a way for processes to communicate with each other.

For example, one process might create a new process using the fork function, and then pass the child process's ID back to the parent process so that the parent can communicate with the child.Debugging: Process IDs can be helpful in debugging, as they can be used to identify which processes are causing problems or behaving unexpectedly.Overall, process IDs are a useful tool for managing and interacting with processes in your code.
``` C
#include <stdio.h>
#include <unistd.h>

int main(void)
{
  pid_t pid;

  pid = getpid();
  printf("The process ID is %d\n", pid);
  return (42);
}
```
> [!NOTE]
> This program will print the process ID of the current process to the console. The process ID is a unique identifier assigned to each process by the operating system. It is used to identify and track processes within the system.

## sleep()
`unsigned int sleep(unsigned int seconds);`

`sleep()` is also a function in the C standard library that causes the calling process to sleep for a specified number of seconds.
``` C
#include <stdio.h>
#include <unistd.h>

int main(void)
{
    printf("Sleeping for 3 seconds...\n");
    sleep(3); // The program waits 3 seconds
    printf("Done sleeping.\n");
    return (42);
}
```

# usleep()
`int usleep(useconds_t usec);`

`usleep()` is a function in the C standard library that causes the calling process to sleep for a specified number of microseconds.
``` C
#include <stdio.h>
#include <unistd.h>
int main(void)
{
    printf("Sleeping for 500000 microseconds...\n");
    usleep(500000);
    printf("Done sleeping.\n");
    return (42);
}
```

# Intructions

To get started go to your minitalk project working directory an the clone the current repository in the the same as your executables:
``` sh
git clone https://github.com/gecarval/Minitalk_tester.git
```

Then move the `tester.sh` file to the minitalk work directory:
``` sh
mv ./Minitalk_tester/tester.sh .
```

Execute the server side of the project in a different terminal/tty:
``` sh
./server
```

Then in diferent terminal execute the tester:
``` sh
./tester.sh -m -1 -2 PID
```

## Execution

Standtard execution:
``` sh
./tester.sh -m -1 -2 PID
```

Bonus execution:
``` sh
./tester.sh -m -3 -4 -5 PID
```

Standtard + Bonus execution:
``` sh
./tester.sh -m -1 -2 -3 -4 -5 PID
```

 ### Features

`-m` -Activates the use of the flags.

-Execute a specific test:

`-1` -Simple ASCII;

`-2` -ALL ASCII;

`-3` -Simple UNICODE;

`-4` -A LOT of UNICODE;

`-5` -GO CRAZY.

> [!TIP]
> Tests are fundamental for a professional or expert in the area, even if this could be a good stantard for tests, this does not substitute the test the owner of the project should do.
