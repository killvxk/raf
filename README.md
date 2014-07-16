Overview
======

RAF - Ruby ALPC Fuzzer

This is a PoC. It _will_ send real traffic to real ALPC ports and produce lots
of output on screen, but is highly unlikely to find real bugs. You are
encouraged to write an actual fuzzer.

Test cases are generated by using ~3000 verses and notes from the works of
Chaucer and feeding them through radamsa.

```
raf.rb - Ruby ALPC Fuzzer - Friday Afternoon Joke Version

Usage:

1. Extract Chaucer:

tar -zxvf [install dir]/chaucer.tar.bz2

1a. Read Chaucer (optional, but recommended)

awk 'FNR==1{print ""}{print}' chaucer/* | less

2. Run Radamsa as a TCP server:

radamsa chaucer/*.txt -n inf -o :9999

3. Run alpcrest on the target

( see https://github.com/bnagy/alpcgo/tree/master/cmd/alpcrest )

4. Run raf.rb

ruby raf.rb [host] [ALPC Port]

Example:
ruby raf.rb 172.16.216.100 "\\RPC Control\\DNS Resolver"
```

Parus Major - PoC ALPC MitM 
======

Don't get excited! 

- The access you need to fuzz this way is more than you'd get from a bug
- The bugs might be completely unreachable

Parus Major is more of an rBuggery demonstration
(https://github.com/bnagy/rBuggery). It uses a simple breakpoint callback and
then corrupts received ALPC messages in memory using the DebugDataSpaces API
and the eponymous Millerfuzz algorithm. Fuzzing via memory injection this way
is both lame and slow.

Get a tiny, tiny bit excited?

- This is a very quick way to poke interesting processes without extensive
  reverse engineering 
- Most ALPC ports are completely unprotected by DACLs, even ones owned by
  SYSTEM processes

I apologise for the name. I have a mental age of 12.

```
Dependencies: hexdump, rbuggery, bindata
Usage:

> ruby parus_major.rb <pid> <fuzzfactor>
```

BUGS
=======

- Does not find bugs

Contributing
=======

Fork & pullreq

License
=======

BSD Style, See LICENSE file for details



