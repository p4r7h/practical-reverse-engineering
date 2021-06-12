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

> Line 1 : `MOV EDi, [EBP+8]`

[ebp+8] is a value in stack representing the first function parameter 
This instruction copies the parameter, a pointer to the string, to register EDI. Now EDI references our string:
``asm
pwndbg> x/s $edi
0x804a000 <my_str>:     "The pool on the roof must have a leak."
``

> Line 2 : `mov edx, edi`
This simply makes a copy of EDI. The reason for that will be clear in line 5.
``asm
pwndbg> x/s $edx
0x804a000 <my_str>:     "The pool on the roof must have a leak."
``

> Line 3 : `xor eax, eax`

set eax to zero
``asm
pwndbg> p/x $eax
$3 = 0x0
``

> Line 4 : `or ecx, 0FFFFFFFFh`

This sets the value of ECX to 0xFFFFFFFF

``asm
pwndbg> p/x $ecx
$2 = 0xffffffff

pwndbg> p/d $ecx            ; Print variable as a signed integer.
$3 = -1
``

> Line 5 : `repne scasb`

Line 5 is where a lot of the magic happens. The instruction scasb searches the memory for the byte in EAX, starting at EDI. The instruction decreases the value of ECX after each byte comparison by one, and increases the value of EDI by one.

In our example, we search the null byte (in EAX) in the null terminated string “The pool on the roof must have a leak.” (referenced by EDI). The counter ECX starts from -1. The following image illustrates the registers before and after repne scasb

![image](https://user-images.githubusercontent.com/37813830/121784357-415ab880-cbd1-11eb-8754-9f47060d56fa.png)

So ECX ends up being -40 and also The value of EDI changes too, that’s why in line 2 we made a copy of the value
```asm
pwndbg> p/d $ecx
$6 = -40
pwndbg> p/x $edi
$7 = 0x804a027  ; before 0x80490c0
```

> Line 6 : `add ecx, 2`

add 2 in ecx so now ecx become -38
``asm
pwndbg> p/d $ecx
$9 = -38
``

> Line 7 : `neg ecx`

its negate the ecx so thats become string lenth now
```asm
pwndbg> p/d $ecx
$10 = 38
```

> Line 8 : `mov al, [ebp+0Ch]`

this instruction copy's byte at stack location [EBP+0Ch] to register Al.
```asm
pwndbg> p/c $al
$11 = 120 'x'
```

> Line 9 : `mov edi, edx`

after modifying edi in line 5 we are now restorying it from the backup edx that we create in line 2.
after that edi once again pointing to the string

``asm 
pwndbg>  p/x $edi
$12 = 0x804a000
``

> Line 10 : `rep stosb`

thats copy byte in al ('x') to every byte in the squence 
effectively overwriting the entire string with a single character

![image](https://user-images.githubusercontent.com/37813830/121784846-f7bf9d00-cbd3-11eb-864d-c3dab2bcb808.png)

> Line 11 : `mov eax, edx`
This copies the address of the string to EAX. EAX holds the return value of the function, so the snippet returns a pointer to the modified string.



```asm
SECTION  .data
my_str: 
    db     'The pool on the roof must have a leak.', 0
SECTION  .text
GLOBAL _start
_start: 
    nop
    push byte 'x'      ; second function parameter
    push dword my_str  ; first function parameter
    call black_out     ; call function
    add esp, 8         ; cleaning out the stack
    mov  ebx,0         ; parameter for exit call (return value) 
    mov  eax,1         ; exit system call
    int 080h           ; run system call, see page 79 pal

black_out:
    push ebp           ; function prologue, save stack base pointer
    mov ebp, esp       ; point base pointer to ESP    
    ; ------------ start code from book ---------
    mov edi, [ebp+8]   
    mov edx, edi       
    xor eax, eax       
    or ecx, 0FFFFFFFFh 
    repne scasb        
    add ecx, 2         
    neg ecx            
    mov al, [ebp+0Ch]  
    mov edi, edx       
    rep stosb          
    mov eax, edx       
    ; ------------ end code from book -----------
    mov esp, ebp       ; restore stack pointer
    pop ebp            ; restore stack base pointer
    ret
```


