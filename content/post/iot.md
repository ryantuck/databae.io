+++
date = "2017-03-04T20:57:47-05:00"
title = "iot"

+++

Particle provides a nice web IDE for flashing programs to
your devices but I'd prefer to use the command line and
there were some kinks to work out.

I'm working off my repo for smart home / iot stuff:

https://github.com/ryantuck/asmartment

## installing packages

I wanted to include [FastLED](https://github.com/FastLED/FastLED) in
my `.ino` file, which works fine from the web interface but
not so much on my machine.

```
🔥  ~/src/asmartment/things/strip 🔥  particle compile photon .

Compiling code for photon

Including:
    strip.ino
attempting to compile firmware
Compile failed. Exiting.
strip.cpp:1:29: fatal error: FastLED/FastLED.h: No such file or directory
 #include <FastLED/FastLED.h>
                             ^
compilation terminated.
make[1]: *** [../build/target/user/platform-6strip.o] Error 1
make: *** [user] Error 2
```

So I cloned `FastLED` into that working directory since the
file has:

```cpp
#include "FastLED/FastLED.h"
```

And got that to work, but now it's complaining about not
being able to find `<avr/io.h>`. Turns out this can be
resolved by installing via `brew`:

```
brew tap osx-cross/avr
brew install avr-libc
```

And it takes god damn forever to install.





