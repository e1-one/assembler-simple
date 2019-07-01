## Writing a simple C program
simpleProgram.c source code:
```
int main()
{
 int x = 0;
 do {
  x += 1;
 } while (x <= 10);
 return 0;
}
```
 > gcc simpleProgram.c -o simpleProgram \
 > ./simpleProgram
 
## Disassembly
> objdump -d ./simpleProgram
```
file format elf64-x86-64

. . .
00000000000005fa <main>:
 5fa:   55                      push   %rbp                 # %rbp - stack base pointer. push old(previous) %rbp to the stack
 5fb:   48 89 e5                mov    %rsp,%rbp            # now %rbp points to base frame function main
 5fe:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)      # -4 is an offset relatively to %rbp. // int x = 0;
 605:   83 45 fc 01             addl   $0x1,-0x4(%rbp)      #       // x += 1;
 609:   83 7d fc 0a             cmpl   $0xa,-0x4(%rbp)      # cmpl subtracts 10 from x and modifies flag ZF. when -0x4 is 0xa then sets ZF to 0
 60d:   7e f6                   jle    605 <main+0xb>       # jump if less or equal (ZF = 1 or SF <> OF)
 60f:   b8 00 00 00 00          mov    $0x0,%eax            # function return value stores in %eax. // return 0;
 614:   5d                      pop    %rbp					# epilogue or cleaning. Get previous(old) base pointer and puts to %rbq
 615:   c3                      retq
 616:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
 61d:   00 00 00
. . .
```