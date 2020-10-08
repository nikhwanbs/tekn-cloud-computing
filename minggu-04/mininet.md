<h1>Mininet Walkthrough</h1>
<h1>Part 1: Everyday Mininet Usage</h1>
First, a (perhaps obvious) note on command syntax for this walkthrough:
<ol>
<li>$ preceeds Linux commands that should be typed at the shell prompt</li>
<li>mininet> preceeds Mininet commands that should be typed at Mininet’s CLI,</li>
<li># preceeds Linux commands that are typed at a root shell prompt</li>
</ol>
In each case, you should only type the command to the right of the prompt (and then press return, of course!)
<h2>Display Startup Options</h2>
Let’s get started with Mininet’s startup options.

Type the following command to display a help message describing Mininet’s startup options:
<br>
<img src=img/Screenshot_38a.png>
<br>
<br>
<img src=img/Screenshot_38b.png>
<br>
This walkthrough will cover typical usage of the majority of options listed.
<h2>Interact with Hosts and Switches</h2>
Start a minimal topology and enter the CLI:
<br>
<img src=img/Screenshot_1.png>
<br>
Display Mininet CLI commands:
<br>
<img src=img/Screenshot_2.png>
<br>
Display nodes:
<br>
<img src=img/Screenshot_3.png>
<br>
Display links:
<br>
<img src=img/Screenshot_4.png>
<br>
Dump information about all nodes:
<br>
<img src=img/Screenshot_5.png>
<br>
You should see the host’s h1-eth0 and loopback (lo) interfaces. Note that this interface (h1-eth0) is not seen by the primary Linux system when ifconfig is run, because it is specific to the network namespace of the host process.
<br>
<img src=img/Screenshot_6.png>
<br>
In contrast, the switch by default runs in the root network namespace, so running a command on the “switch” is the same as running it from a regular terminal:
<br>
<img src=img/Screenshot_7.png>
<br>
This will show the switch interfaces, plus the VM’s connection out (eth0).
Note that only the network is virtualized; each host process sees the same set of processes and directories. For example, print the process list from a host process:
<br>
<img src=img/Screenshot_8.png>
<br>
This should be the exact same as that seen by the root network namespace:
<br>
<img src=img/Screenshot_9.png>
<br>
It would be possible to use separate process spaces with Linux containers, but currently Mininet doesn’t do that. Having everything run in the “root” process namespace is convenient for debugging, because it allows you to see all of the processes from the console using ps, kill, etc.
<h2>Test connectivity between hosts</h2>
Now, verify that you can ping from host 0 to host 1:
<br>
<img src=img/Screenshot_10.png>
<br>
If a string appears later in the command with a node name, that node name is replaced by its IP address; this happened for h2.
Now the first host knows the MAC address of the second, and can send its ping via an ICMP Echo Request. This request, along with its corresponding reply from the second host, both go the controller and result in a flow entry pushed down (along with the actual packets getting sent out).

Repeat the last ping:
<br>
<img src=img/Screenshot_11.png>
<br>
You should see a much lower ping time for the second try (< 100us). A flow entry covering ICMP ping traffic was previously installed in the switch, so no control traffic was generated, and the packets immediately pass through the switch.

An easier way to run this test is to use the Mininet CLI built-in pingall command, which does an all-pairs ping:
<br>
<img src=img/Screenshot_12.png>
<br>
<h2>Run a simple web server and client</h2>
Remember that ping isn’t the only command you can run on a host! Mininet hosts can run any command or application that is available to the underlying Linux system (or VM) and its file system. You can also enter any bash command, including job control (&, jobs, kill, etc..)

Next, try starting a simple HTTP server on h1, making a request from h2, then shutting down the web server:
<br>
<img src=img/Screenshot_13.png>
<br>
Exit the CLI:
<br>
<img src=img/Screenshot_14.png>
<br>
<h2>Cleanup</h2>
If Mininet crashes for some reason, clean it up:
<br>
<img src=img/Screenshot_15.png>
<br>
<h1>Part 2: Advanced Startup Options</h1>
<h2>Run a Regression Test</h2>
You don’t need to drop into the CLI; Mininet can also be used to run self-contained regression tests.

Run a regression test:
<br>
<img src=img/Screenshot_16.png>
<br>
This command created a minimal topology, started up the OpenFlow reference controller, ran an all-pairs-ping test, and tore down both the topology and the controller.

Another useful test is iperf (give it about 10 seconds to complete):
<br>
<img src=img/Screenshot_17.png>
<br>
This command created the same Mininet, ran an iperf server on one host, ran an iperf client on the second host, and parsed the bandwidth achieved.
<h2>Changing Topology Size and Type</h2>
The default topology is a single switch connected to two hosts. You could change this to a different topo with --topo, and pass parameters for that topology’s creation. For example, to verify all-pairs ping connectivity with one switch and three hosts:

Run a regression test:
<br>
<img src=img/Screenshot_18.png>
<br>
Another example, with a linear topology (where each switch has one host, and all switches connect in a line):
<br>
<img src=img/Screenshot_19.png>
<br>
Parametrized topologies are one of Mininet’s most useful and powerful features.
<h2>Link variations</h2>
Mininet 2.0 allows you to set link parameters, and these can even be set automatially from the command line:
<br>
<img src=img/Screenshot_20.png>
<br>
If the delay for each link is 10 ms, the round trip time (RTT) should be about 40 ms, since the ICMP request traverses two links (one to the switch, one to the destination) and the ICMP reply traverses two links coming back.
<h2>Adjustable Verbosity</h2>
The default verbosity level is info, which prints what Mininet is doing during startup and teardown. Compare this with the full debug output with the -v param:
<br>
<img src=img/Screenshot_21a.png>
<br>
<br>
<img src=img/Screenshot_21.png>
<br>
Lots of extra detail will print out. Now try output, a setting that prints CLI output and little else:
<br>
<img src=img/Screenshot_22.png>
<br>
Outside the CLI, other verbosity levels can be used, such as warning, which is used with the regression tests to hide unneeded function output.
<h2>Custom Topologies</h2>
Custom topologies can be easily defined as well, using a simple Python API, and an example is provided in custom/topo-2sw-2host.py. This example connects two switches directly, with a single host off each switch:
<br>
<img src=img/Screenshot_23a.png>
<br>
<img src=img/Screenshot_23.png>
<br>
When a custom mininet file is provided, it can add new topologies, switch types, and tests to the command-line. For example:
<br>
<img src=img/Screenshot_24.png>
<br>
<h2>ID = MAC</h2>
By default, hosts start with randomly assigned MAC addresses. This can make debugging tough, because every time the Mininet is created, the MACs change, so correlating control traffic with specific hosts is tough.

The --mac option is super-useful, and sets the host MAC and IP addrs to small, unique, easy-to-read IDs.

Before:
<br>
<img src=img/Screenshot_25.png>
<br>
After:
<br>
<img src=img/Screenshot_26.png>
<br>
<h2>Other Switch Types</h2>
Other switch types can be used. For example, to run the user-space switch:
<br>
<img src=img/Screenshot_27.png>
<br>
Another example switch type is Open vSwitch (OVS), which comes preinstalled on the Mininet VM. The iperf-reported TCP bandwidth should be similar to the OpenFlow kernel module, and possibly faster:
<br>
<img src=img/Screenshot_28.png>
<br>
<h2>Mininet Benchmark</h2>
To record the time to set up and tear down a topology, use test ‘none’:
<br>
<img src=img/Screenshot_29.png>
<br>
<h2>Everything in its own Namespace (user switch only)</h2>
By default, the hosts are put in their own namespace, while switches and the controller are in the root namespace. To put switches in their own namespace, pass the --innamespace option:
<br>
<img src=img/Screenshot_30.png>
<br>
Instead of using loopback, the switches will talk to the controller through a separately bridged control connection. By itself, this option is not terribly useful, but it does provide an example of how to isolate different switches.

<h1>Part 3: Mininet Command-Line Interface (CLI) Commands</h1>
<h2>Display Options</h2>
To see the list of Command-Line Interface (CLI) options, start up a minimal topology and leave it running. Build the Mininet:
<br>
<img src=img/Screenshot_31a.png>
<br>
Display the options:
<br>
<img src=img/Screenshot_31.png>
<br>
<h2>Python Interpreter</h2>
If the first phrase on the Mininiet command line is py, then that command is executed with Python. This might be useful for extending Mininet, as well as probing its inner workings. Each host, switch, and controller has an associated Node object.

At the Mininet CLI, run:
<br>
<img src=img/Screenshot_32.png>
<br>
Print the accessible local variables:
<br>
<img src=img/Screenshot_33.png>
<br>
Next, see the methods and properties available for a node, using the dir() function:
<br>
<img src=img/Screenshot_34.png>
<br>
You can also evaluate methods of variables:
<br>
<img src=img/Screenshot_35.png>
<br>
<h2>Link Up/Down</h2>
For fault tolerance testing, it can be helpful to bring links up and down.

To disable both halves of a virtual ethernet pair:
<br>
<img src=img/Screenshot_36a.png>
<br>
You should see an OpenFlow Port Status Change notification get generated. To bring the link back up:
<br>
<img src=img/Screenshot_36.png>
<br>
<h1>Part 4: Python API Examples</h1>
The examples directory in the Mininet source tree includes examples of how to use Mininet’s Python API, as well as potentially useful code that has not been integrated into the main code base.
<h2>SSH daemon per host</h2>
One example that may be particularly useful runs an SSH daemon on every host:
<br>
<img src=img/Screenshot_37.png>
<br>
<h1>Part 5: Walkthrough Complete!</h1>
Congrats! You’ve completed the Mininet Walkthrough. Feel free to try out new topologies and controllers or check out the source code.