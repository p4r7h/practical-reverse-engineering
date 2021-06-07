1. This function uses a combination SCAS and STOS to do its work. 
    First, explain what is the type of the [EBP+8] and [EBP+C] in line 1 
    and 8, respectively. Next, explain what this snippet does.
```asm
01: 8B 7D 08 mov edi, [ebp+8] 
02: 8B D7 mov edx, edi 
03: 33 C0 xor eax, eax 
04: 83 C9 FF or ecx, 0FFFFFFFFh 
05: F2 AE repne scasb 
06: 83 C1 02 add ecx, 2 
07: F7 D9 neg ecx 
08: 8A 45 0C mov al, [ebp+0Ch] 
09: 8B FA mov edi, edx 
10: F3 AA rep stosb 
11: 8B C2 mov eax, edx
```
