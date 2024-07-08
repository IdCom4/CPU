# CPU_design_prototype

I like to know how things work under the hood, and especially the things that i use on a daily basis.
So i learned about how CPUs are made and the concepts behind their design.
This was my take on the subject.

*Incomplete project, and some of the ideas explored are probably flawed.*

## Base concepts

				15     14    13    12   11    10   9    8   7  6  5  4 3 2 1 0
				 s  16384  8192  4096 2048  1024 512  256 128 64 32 16 8 4 2 1  = -32768 -> 32768

				15     14    13    12   11    10   9    8   7  6  5  4 3 2 1 0
				 s  16384  8192  4096 2048  1024 512  256 128 64 32 16 8 4 2 1

FLAGS (7):

	in instruction:
	 INSTRUCTION|		   FLAGS_INDEX|   R_1|  R_0
		    |  7  6  5  4  3  2  1  0 |      |     
	15 14 13 12 | 11 10  9  8  7  6  5  4 | 3  2 | 1  0
	------------|-------------------------|------|-----
	 0  0  0  0 |  0  0  0  0  0  0  0  0 | 0  0 | 0  0

	0: EQUAL_FLAG
	1: GREATER_FLAG
	2: LESSER_FLAG
	3: ZERO_FLAG
	4: SIGN_FLAG
	5: OVERFLOW_FLAG
	6: UNDERFLOW_FLAG
	7: STRICT_MODE
	

instructions (10):

	address based:
	 INSTRUCTION|			          ADDRESS
	15 14 13 12 | 11 10  9  8  7  6  5  4  3  2  1  0
	------------|------------------------------------
	 0  0  0  0 |  0  0  0  0  0  0  0  0  0  0  0  0

	registers based:
	 INSTRUCTION|			      |   R_1|  R_0
	15 14 13 12 | 11 10  9  8  7  6  5  4 | 3  2 | 1  0
	------------|-------------------------|------|-----
	 0  0  0  0 |  0  0  0  0  0  0  0  0 | 0  0 | 0  0

	comparison based:
	 INSTRUCTION|			 FLAGS|   R_1|  R_0
	15 14 13 12 | 11 10  9  8  7  6  5  4 | 3  2 | 1  0
	------------|-------------------------|------|-----
	 0  0  0  0 |  0  0  0  0  0  0  0  0 | 0  0 | 0  0
	
	ADD	0000 > registers based

	SOUS	0001 > registers based

	MULT	0010 > registers based

	DIV	0011 > registers based

	MOD	0100 > registers based

	INCR	0101 > registers based (only 1)
	
	DECR	0110 > registers based (only 1)

	LOAD	0111 > address based

	STORE	1000 > registers based

	SAVE	1001 > address based

	CMP	1010 > comparison based

	JUMP	1011 > address based



REGISTERS (4):

	REGISTER_A	00
	REGISTER_B	01
	REGISTER_C	10
	REGISTER_D	11


RAM ADDRESSES:

	 INSTRUCTION|			      	  ADDRESS
	15 14 13 12 | 11 10  9  8  7  6  5  4  3  2  1  0
	------------|------------------------------------
	 0  0  0  0 |  0  0  0  0  0  0  0  0  0  0  0  0
		      |__________________________________|

	0 -> 111111111111
	0 -> 4095 addresses * 16 bits for each = 65520 bits = 8190 octets = 8.19 ko
