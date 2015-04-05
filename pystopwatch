#!/usr/bin/env python3

from __future__ import print_function, division

import datetime
import os
import signal

from termcolor import colored, cprint

APPNAME = 'PyStopwatch'

class Stopwatch(object):
    def __init__(self):
        self.time = datetime.datetime.now()
        self.state = True
        self.seconds = 0
        self.logfile = self.init_logfile()
        cprint('Started', 'green')
        self.print_out_and_log()

    def switch(self):
        if self.state:
            diff = datetime.datetime.now() - self.time
            self.seconds += diff.total_seconds()
            self.time = datetime.datetime.now()
        else:
            self.time = datetime.datetime.now()
        self.state = not self.state
        self.print_out_and_log()

    def print_out_and_log(self):
        timestr = self.time.strftime('%H:%M:%S')
        statestr = 'Running' if self.state else 'Paused'
        stateclr = 'green' if self.state else 'red'
        statemsg = "%s at %s." % (statestr, timestr)
        elapsemsg = "Elapsed time: %s" % self.elapsed_str()
        log_msg = '%s %s\n' % (statemsg, elapsemsg)
        print_msg = '%s %s' % (colored(statemsg, stateclr), elapsemsg)
        self.logfile.write(log_msg)
        print(print_msg)

    def elapsed_str(self):
        hours = self.seconds // 3600
        minutes = (self.seconds - 3600*hours) // 60
        seconds = (self.seconds % 60) // 1
        rest = self.seconds - 3600*hours - 60*minutes - seconds
        milli = round(rest*100.0)
        return '%02i:%02i:%02i:%02i' % (hours, minutes, seconds, milli)

    def logdir(self):
        dirname = os.path.expanduser(os.path.join('~', '.' + APPNAME))
        if not os.path.exists(dirname):
            os.makedirs(dirname)
        return dirname

    def init_logfile(self):
        fname = '%s/%s_pystopwatch.log' % (self.logdir(), 
                self.time.strftime('%Y%m%d%H%M%S'))
        return open(fname, 'w')

    def stop(self):
        if self.state:
            self.switch()
        else:
            self.print_out_and_log()

    def cleanup(self):
        self.logfile.close()
        cprint('Stopped', 'red')

def sigterm_hdl(signal, frame):
    raise SystemExit

def main():
    signal.signal(signal.SIGTERM, sigterm_hdl)
    sw = Stopwatch()
    try:
        while True:
            if sw.state:
                input('Press Enter to pause ...')
            else:
                input('Press Enter to continue ...')
            sw.switch()
    except (KeyboardInterrupt, EOFError):
        pass
    finally:
        print()
        sw.stop()
        sw.cleanup()

if __name__ == '__main__':
    main()
