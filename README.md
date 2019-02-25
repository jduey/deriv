
The write up explaining this is [here](http://www.toccata.io/2019/02/RefCounting.html).

The Toccata code in `deriv.toc` is horribly ugly. This is usually what happens when you optimize code heavily. It's mostly a reault of Toccata not having polymorphic dispatch on arguments except the first one and the lack of pattern matching.

Currently, Toccata doesn't have an `if` expression, which would probably have let me close the performance gap. I'm thinking seriuosly about adding one.


Here are the results of the [original Ocaml code](https://gist.github.com/jdh30/f3d90a65a7abc7c9faf5c0299b002db3) by Jon Harrop on my machine.

    Command being timed: "../deriv-ocaml/a.out 10"
    User time (seconds): 1.56
    System time (seconds): 0.09
    Percent of CPU this job got: 100%
    Elapsed (wall clock) time (h:mm:ss or m:ss): 0:01.66
    Average shared text size (kbytes): 0
    Average unshared data size (kbytes): 0
    Average stack size (kbytes): 0
    Average total size (kbytes): 0
    Maximum resident set size (kbytes): 432784
    Average resident set size (kbytes): 0
    Major (requiring I/O) page faults: 0
    Minor (reclaiming a frame) page faults: 109219
    Voluntary context switches: 1
    Involuntary context switches: 1
    Swaps: 0
    File system inputs: 0
    File system outputs: 0
    Socket messages sent: 0
    Socket messages received: 0
    Signals delivered: 0
    Page size (bytes): 4096
    Exit status: 0

And here are the results of the Toccata code.

    Command being timed: "./deriv 10"
    User time (seconds): 3.00
    System time (seconds): 0.08
    Percent of CPU this job got: 100%
    Elapsed (wall clock) time (h:mm:ss or m:ss): 0:03.09
    Average shared text size (kbytes): 0
    Average unshared data size (kbytes): 0
    Average stack size (kbytes): 0
    Average total size (kbytes): 0
    Maximum resident set size (kbytes): 299448
    Average resident set size (kbytes): 0
    Major (requiring I/O) page faults: 0
    Minor (reclaiming a frame) page faults: 74497
    Voluntary context switches: 8
    Involuntary context switches: 4
    Swaps: 0
    File system inputs: 0
    File system outputs: 0
    Socket messages sent: 0
    Socket messages received: 0
    Signals delivered: 0
    Page size (bytes): 4096
    Exit status: 0
																				      