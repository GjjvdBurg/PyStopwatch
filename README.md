PyStopwatch
===========

A very simple command line stopwatch written in Python.

Usage
-----

PyStopwatch can be started using

    python stopwatch

This will automatically start the stopwatch. By pressing Enter you can toggle 
the state of the Stopwatch from running to paused. The total time since the 
stopwatch was started will be printed on the screen. Using Ctrl+C stops the 
stopwatch, and prints out the total elapsed time. The output will look 
something like this:

    Started stopwatch at: 18:04:19
    Press Enter to pause...
    Stopped: 00:00:01:54 seconds passed
    Press Enter to continue...
    Running: 00:00:01:54 seconds passed
    Press Enter to pause...^C
    Stopped: 00:00:03:17 seconds passed
    Stopped stopwatch at: 18:04:23

A logfile is kept in the `~/.PyStopwatch` directory.
