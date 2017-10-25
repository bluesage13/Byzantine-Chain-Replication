# Byzantine-Chain-Replication
Project for Asynchronous Systems

Submitted by 1)Neel Paratkar  2) Jay Torasakar

PLATFORM
================================================================================
We developed tested the code on MacOS using DistAlgo v1.0.9. The version of python installed on the testing machine
is Python3.6.2. This system is developed to run only on a single node and does not support execution on a multi host
platform. Apart from this we also used libsodiyum cryptographic library for signing required during message transmission.


INSTRUCTIONS
================================================================================
The testing machine should have PyNaCl installed on it along with Python version3 and above. The system should also have
DistAlgo v1.0.9 installed or be able to import the modules to run the DistAlgo programs.
The system is structured in following way:
A startup process (startup.da) reads the configuration file provided as commandline argument and creates Olympus and
Clients as mentioned in the configuration file. The Olympus after starting created the replicas based on the value of
fault tolerance. The clients get their workload form the configuration file. Clients and Replicas depend upon the
Olympus to create the keys for signing. The public keys of all elements are shared on request.
Fault Injection: If failure and triggers are mentioned in the configuration file then the necessary failures are
injected during runtime in replicas when the trigger occurs.

WORKLOAD GENERATION
================================================================================
Based upon the seed value and the number of instructions mentioned in the configuration file, the clients generate
pseudoramdom workload for themselves. Following is an summary of how this is achieved:
A list of words was used from a public repo: https://github.com/first20hours/google-10000-english
This word file has 20000 unique worlds starting with letters in alphabets. The client reads this into a list.
Based upon the number of operations required, the client generates an array of random integer. Each array
element is converted to mod of 4 which results in a value used to take operation from list ['put', 'get', 'append', 'slice'].
A random list of words is chosen from the words.txt file and distributed into key value pair.
These key value pairs are assigned to the commands. This generates a pseudoramdom value of workload.
This value can be reproduce using the same seed value.

BUGS AND LIMITATIONS
================================================================================
Due to lack of programatically checking result for large workloads, results for failure cases cannot be verified.
In failure cases, reconfiguration is not supported hence, on meeting a reconfiguration case, a log for sending
reconfiguration request to the Olympus is generated.
This system doesnot support multihosting. It can be made to run on a multihost system with a small change to the
code however the timeouts have not been handled efficiently.
The failure case : Some combinations of failure trigger cases have not been tested


CONTRIBUTIONS
================================================================================
Neel Paratkar: Programming, readme and testng file generation, testing code and generating logs
Jay Torasakar: Editing the pseudocode to fit phase 2 generation, test case listing, understanding and explaining signing
For further details: https://github.com/bluesage13/Byzantine-Chain-Replication
