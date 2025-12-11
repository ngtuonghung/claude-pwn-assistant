challenge: example_pwn

checksec:
    Arch:     amd64-64-little
    RELRO:    Partial RELRO
    Stack:    No canary found
    NX:       NX enabled
    PIE:      No PIE (0x400000)

file:
ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked

what i found:
main at 0x401234
calls gets() into 64 byte buffer
no size check
buffer overflow

what i tried:
crashed with 100 A's - works
offset is 72 bytes
found win at 0x4011c7

problem:
segfault when calling win
payload: b'A'*72 + p64(0x4011c7)
maybe alignment??

todo:
check stack alignment
try ret gadget before win
verify address
