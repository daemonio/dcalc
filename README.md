dcalc
=====

dcalc is a bash script calculator with radix conversion. This script uses the dc calculator as background to do all the math.

Radix Conversion
================

Use 0x for hexadecimal, 0y for binary and 0o for octal. Decimal numbers does not need a prefix.

Examples
========

<pre>
$ dcalc '(0y111 + 3) * (0xA)'
100(10) : 100
100(2)  : 0y1100100
100(8)  : 0o144
100(16) : 0x64
</pre>

remember: 111(bin) = 7(dec) and A(hex) = 10(dec)

Negative numbers are in 2-complement:

<pre>
$ dcalc '-10'
-10(10) : -10
-10(2)  : 0y1111111111111111111111111111111111111111111111111111111111110110
-10(8)  : 0o1777777777777777777766
-10(16) : 0xFFFFFFFFFFFFFFF6
</pre>

You can use the following math library:
- sin(x)  The sine of x, x is in degrees.
- cos(x)  The cosine of x, x is in degrees.
- l(x)  The natural logarithm of x.
- e(x)  The exponential function of raising e to the value x.
- sqrt(x) The square root of x.

<pre>
$ dcalc '0.5 - sin(0y11110)'
0(10) : 0
0(2)  : 0y0
0(8)  : 0o0
0(16) : 0x0
</pre>

since 0y11110 is 30(dec) and sin(30) is 0.5

You might want to calculate more complex expressions, like:

<pre>
$ ./dcalc '20 * ( (0xBFFFFA - 0xBFFFFB) / 5 ) + 0y1001011 - 0o1'
70(10) : 70
70(2)  : 0y1000110
70(8)  : 0o106
70(16) : 0x46
</pre>

using the available functions:

<pre>
$ dcalc 'l(0y10000000000)/l(2)'
10.00010
</pre>
same as log2(2^10). We don't get an exact result because of the round errors.

<pre>
$ dcalc 'e((sqrt(0o32)))'
163.85960
</pre>

calculate exp(sqrt(26))

You can set the scale changing the variable SCALE in the code. The default value is 5.

For SCALE=10 in the above example, we get:

<pre>
$ dcalc 'e((sqrt(0o32)))'
163.8611648498
</pre>

Don't forget the ^ operator:

<pre>
$ dcalc '7^20'
79792266297612001(10) : 79792266297612001
79792266297612001(2)  : 0y100011011011110101010010010111000011111100001011011100001
79792266297612001(8)  : 0o4333652227037413341
79792266297612001(16) : 0x11B7AA4B87E16E1
</pre>

Because I am using printf in the 2-complement conversion, large numbers (above 2^64) can cause
an overflow.

<pre>
$ dcalc '7^23'
27368747340080916343(10) : 27368747340080916343
27368747340080916343(2)  : 0y/bin/dcalc: line 99: printf: warning: 27368747340080916343: Numerical result out of range
1111111111111111111111111111111111111111111111111111111111111111
27368747340080916343(8)  : 0o/bin/dcalc: line 106: printf: warning: 27368747340080916343: Numerical result out of range
1777777777777777777777
27368747340080916343(16) : 0x/bin/dcalc: line 106: printf: warning: 27368747340080916343: Numerical result out of range
FFFFFFFFFFFFFFFF
</pre>

This kind of error will continue if printf still being used.

TODO
====

- Do not use printf. This can avoid overflow
- Create some bc modules and useful functions
- Read expressions from file or stdin
