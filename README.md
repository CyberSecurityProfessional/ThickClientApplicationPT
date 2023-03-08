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

* Communication Secirity

    Encrypted communication, Vertification of Transport Layer security and cipher suite strength
    
    Tools: testssl.sh, sslyze

* Installation Traffic

    Is sensitive information transmitted during installation time
    
    Tools: Wireshark, echomirage, MITM-Relay, Burp Suite, HTTP Debugger Pro or Fiddler

* Run Time Interception and Tampering

    Verify the communication by tampering the communication between client and the server (API Tests)
    
    Tools: Wireshark, echomirage, MITM-Relay, Burp Suite, HTTP Debugger Pro or Fiddler
    
