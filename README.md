dcalc
=====

dcalc is a bash script calculator with radix conversion. This script uses the dc calculator as background to do all the math.

Radix Conversion
================

Use 0x for hexadecimal, 0y for binary and 0o for octal. Decimal numbers does not need a prefix.

Examples
========

$ dcalc '(0y111 + 3) * (0xA)'
100(10) : 100
100(2)  : 0y1100100
100(8)  : 0o144
100(16) : 0x64

remember: 111 = 7(dec) and 0xA = 10(dec)

Negative numbers are in 2-complement:

<pre>
$ dcalc '-10'
-10(10) : -10
-10(2)  : 0y1111111111111111111111111111111111111111111111111111111111110110
-10(8)  : 0o1777777777777777777766
-10(16) : 0xFFFFFFFFFFFFFFF6
</pre>

You can use the following funcions too: sin(), cos() (in degree, not radian), l (natural logarithm)

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
