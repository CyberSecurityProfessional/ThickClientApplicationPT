# ThickClientApplicationPT
Thick client application penetration testing methodology research.

## Checklist

### Information Gathering

* Technology, Framework, Libraries used:

    Analyze and identify what technology, framework, library is used in the application. Identify if any known vulnerabilities are associated with the identified components.

  Tools: CFF Explorer, DIE (Detect It Easy)

* Identify associated Files:

  Analyze and Identify what files are used while running the application
  
  Tools: Proc Mon (Process Monitor from Sys Internals suite)
  
* Identify Local ports used for comunication:

  1.Identify which ports the application uses to connect to the server.
  
  2.Identify what protocol is used

  Tools: TCP View (part of sys internals suite), Wireshark, netstat

* Identify remote endpoints and ports:

  1.Identify the remote endpoints to which the application is establishing communication
  
  2.Identify what protocol is used

  Tools: TCP View (part of sys internals suite), Wireshark, netstat

* Application Signing:

  Verify if the exe application and the linked dll files are signed

  Tools:
  
  1.sigcheck (part of sys internals suite)
  
  2.right click -> Properties -> digital signatures"

* Source Code Obfuscation:

  Verify if the source code is obfuscated with effective obfuscation tools

  Tools:
  Browse the installation folder using the tool 'Jetbrains dotPeek'
  
### Communication/Proxy

* Communication Security

	Encrypted communication, Vertification of Transport Layer security and cipher suite strength
 
	Tools: testssl.sh, sslyze

* Installation Traffic

	Is sensitive information transmitted during installation time
    
	Tools: Wireshark, echomirage, MITM-Relay, Burp Suite, HTTP Debugger Pro or Fiddler

* Run Time Interception and Tampering

	Verify the communication by tampering the communication between client and the server (API Tests)
    
	Tools: Wireshark, echomirage, MITM-Relay, Burp Suite, HTTP Debugger Pro or Fiddler
    
### Client Side Attacks

* Client Side File Tampering

	After identifying the associated files, check if it is possible to tamper the files and perform unintended operations

	Method: Manual

* Client Side Windows Registry Tampering

	Analyse the linked registry items and check if:

	* Any Sensitive data is stored in stored in registry

	* Tampering the registry and perform unintended operations

	Tools: Proc Mon (Process Monitor from Sys Internals suite), regshot, registry editor

* Strings

	Check for sensitive data/Hardcoded credentials using Strings command

	Tools: Strings.exe (from Sys Internals suite)\

* DLL Injection

	(Also known as process Injection. Inject DLL's into running applications to see if the DLL/feature is loaded under the application context)

	1.install atomic-red-team and execute respective test case

	Tools: Atomic-red-team (test case number T1218)<AskAuthor>

	https://github.com/redcanaryco/invoke-atomicredteam/wiki/Installing-Invoke-AtomicRedTeam

* DLL Hijacking

	1.Identify linked dll's using process monitor

	2.Create malicious dll's from meterpreter and check if that is executed when running the application

	Tool: Process Monitor (from sys internal suite), meterpreter

* Application Logs

	Verify if the application logs any sensitive information whille exeucting

	Tools: Command: from cmd prompt: ""app.exe > c:\users\Desktop\logs.txt""

	Logs can also be found at C:\Program Data\<applicationName>\"

* Test for Symbolic Link Attacks

	Command: symbolic-link-testing-tools\CreateMountPoint.exe <sourcepath> <to_destination_path>

	Tools: https://github.com/googleprojectzero/symboliclink-testing-tools

### Binary Analysis

* Runtime Analysis

	1.identify if any runtime variables are used while the application is executing

	Tools: DnSpy, Ollydbg

		.Net, -> ILSpy or dnSpy

		Java based application -> Jd-gui or jadx

		C/C++ -> IDA Pro

* Patching and reverse engineering

	Identify if the application can be decompiled, patched and reverse engineered to change the client side logic or execute any malicious commands

	Tools: ILSpy, Ghidra, Immunity Debugger

* Inter process communication

	1.Identify if any IPC mechanisms used in the application

	2.Check if IPC mechanism can be tampered or manipulated to execute unintended features

	Process:

		Process Explorer -> to identify the IPC mechnisms such as named pipes and shares used.

		accesschk.exe from sysInternal suite -> to identify the access contols of names pipes that are being used.

		ioninja pipe monitor -> to monitor the communication in named pipes

		IDA Pro can also be used for analysis and exploitation

* Auditing the binary

	Audit the binary using Microsoft Binscope binary analyzer. Tool to verify if code is built using the compiler/linker protections required by the Microsoft SDL.

	Tools: Microsoft Binscope binary analyzer

* Binary Protections

	check if the binary has protection against recommended controls such as:

	CHECKSUM, DATA-EXEC-PREVENT, RUNS-IN-APP-CONTAINER, CONSIDER-MANIFEST, VERIFY-DIGITAL-CERT, CONTROL-FLOW-GUARD, HANDLES-ADDR-GT-2GB, ASLR, SAFE-SEH

	Tools: Binary-Security-Check: https://github.com/koutheir/binary-security-check

### Client Side Analysis

* Client Side UI Tampering

	Tampering of client side UI to execute unintended feature/functionality

	Tools: WinSpy++, WinManipulate, Windows Enabler

### Memory Analysis

* Sensitive Information in Memory

	Verify if sensitive information is stored in memory using memory analysis tools

	Tools: Process Hacker

* Memory Manipulation

	Verify if data stored in memory can be manipulated.

	Process: <pending>[AskAuthor]
