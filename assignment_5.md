*Jan Kaufmann*
# Assignment 5
### 1. Race Condition
* A race condition describes the fact that when two processes enter a "critical region" at the same time or shortly offset, the process that enters last will "win" because it will overwrite the data that the first process wrote e.g. printer queue.

### 2. Disabling Interrupts
#### i)
* Because the interrupts only take effect on the core they where disabled and the other cores would still be able to work normaly and enter the critical region.

#### ii)
Because a user process with malicious intent could abuse this power to, for example, disable the interrupts then entering a infinite loop thus completly blocking the machine.

### 3. Peterson's Solution
#### i)
* In enter_region() first the other process is evaluated. Then the calling        process sets the value of a bool[] true so that other processes know that a process is interested in the critical region. Then the loser variable is set because the first to come is the loser. Then the process checks if it is the loser and if anybody else is interested in the critical region if that is the case the process will enter a infinite loop, if not the region is entered.

#### ii)
* When two processes enter enter_region() at the same time or slightly offset they might check the while loop when the other process has not set the lock variable to true so both processes will enter the critical region.

#### iii)
* The loser variable defines the process that has to wait before other processes.
It only has effect when a other process is interested in the critical region.

##### iiii)
  ```
    int loser // shared variable
    Bool interested[2] // two processes only
    void enter_region(int process)
    {
        if(process == 0)
        {
            int other_one = 1;
            int other_two = 2;
        }
        else if(process == 1)
        {
            int other_one = 0;
            int other_two = 2;
        }
        else
        {
            int other_one = 0;
            int other_two = 1;
        }
        interested[process] = True;
        loser = process;
        while (loser == process && (interested[other_one] || interested[other_two])) ;
    }
  ```

  ```
    void leave_region(int process)
    {
        interested[process] = False;
    }
  ```
