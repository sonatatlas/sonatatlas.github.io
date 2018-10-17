---
title: Reverse input in command-line
categories: linux
layout: post
---

```C
cat << EOF > hello.c
int main(int argc, char ** argv) {
    printf("Hello, world!\n");
}
EOF
```
