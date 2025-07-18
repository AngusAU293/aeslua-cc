# AES for lua

This files contain an implementation of AES in lua, that is CC:Tweaked friendly. The only additional library 
needed is bitlib (should already be included with CC:Tweaked).

## Usage

aeslua.lua contains a simple API to encrypt and decrypt lua strings.

To encrypt the string "geheim" with the password "password" use:

```lua
require("aeslua");
cipher = aeslua.encrypt("password", "secret");
```

and to decrypt the string again:

```lua
plain = aeslua.decrypt("password", cipher);
```

You can also specify the key size and the encryption mode. For further examples
look into the file src/testcryptotest.lua.

To use AES directly, have a look at aes.lua and at the example usage in 
testaes.lua.

## Installation

Copy the `src` folder to your libs directory, rename it to something like `aes`, and require it in your script.

```lua
require("libs.aes.aeslua")
```

## Speed

The implementation is rather optimized (it uses tables for most AES operations) 
but still cannot compete with AES written in other languages. Typical AES 
implementations reach several 100 MBit per second, this implementation only 
reaches 400 kBit per second. The most plausible reason is the heavy reliance
of AES on bit operations. As lua numbers are doubles bitlib needs to convert
them to long values for each bit operation.

So if you need to encrypt much data with AES, do yourself a favor and use a 
C-Implementation. But if you only need to encrypt short strings and you have 
no control over the lua environment (like in games :-)) use this library.

Matthias Hilbig <mhilbig@gmail.com>
