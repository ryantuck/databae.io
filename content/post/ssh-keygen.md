+++
date = "2017-02-12T18:32:54-05:00"
title = "ssh keygen"

+++

## create an ssh key pair

Here's how to create a key pair on a machine.

```
ssh-keygen -t rsa -b 4096 -C "ryan@tuck.com"
```

To authorize that key as one you want to allow onto the
machine:

```
cat ~/.ssh/new_key.pub >> ~/.ssh/authorized_keys
```

