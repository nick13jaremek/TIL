# Problem

There is a need to count the number of file descriptors currently open by a certain process on a Linux machine. There must be some way to calculate this number in a somewhat trivial way.

# Solution

Enter the following series of commands to obtain the number of file descriptors associated to a certain Linux process.

1. `ps aux`: lists the current processes. On the *PID* column, find the process associated to your application and copy its PID.
2. `ls -l /proc/<PID of process>/fd | wc -l`: shows the number of file descriptors opened for the process whose PID matches *<PID of process>*.

