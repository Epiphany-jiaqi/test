
 
Table B.4 Register names and numbers
 

15 14 13 12	11 10	9 8  7  6  5  4  3  2	1 0
 


CR-Type CI-Type CS-Type CS'-Type CB-Type CB'-Type CJ-Type CSS-Type CIW-Type CL-Type
 
3 bits	3 bits	3 bits	2 bits	3 bits	2 bits
Figure B.2 RISC-V compressed (16-bit) instruction formats Table B.5 RVM: RISC-V multiply and divide instructions








Table B.6 RVC: RISC-V compressed (16-bit) instructions
op	instr15:10	funct2	Type	RVC Instruction	32-Bit Equivalent
00 (0)	000– – –	–	CIW	c.addi4spn rd', sp, imm	addi rd', sp, ZeroExt(imm)*4
00 (0)	001– – –	–	CL	c.fld	fd',	imm(rs1')	fld fd', (ZeroExt(imm)*8)(rs1')
00 (0)	010– – –	–	CL	c.lw	rd',	imm(rs1')	lw	rd', (ZeroExt(imm)*4)(rs1')
00 (0)	011– – –	–	CL	c.flw	fd',	imm(rs1')	flw fd', (ZeroExt(imm)*4)(rs1')
00 (0)	101– – –	–	CS	c.fsd	fs2',	imm(rs1')	fsd fs2', (ZeroExt(imm)*8)(rs1')
00 (0)	110– – –	–	CS	c.sw	rs2',	imm(rs1')	sw	rs2', (ZeroExt(imm)*4)(rs1')
00 (0)	111– – –	–	CS	c.fsw	fs2',	imm(rs1')	fsw fs2', (ZeroExt(imm)*4)(rs1')
01 (1)	000000	–	CI	c.nop	(rs1=0,imm=0)	nop
01 (1)	000– – –	–	CI	c.addi rd,	imm	addi rd,	rd, SignExt(imm)
01 (1)	001– – –	–	CJ	c.jal	label	jal ra,	label
01 (1)	010– – –	–	CI	c.li	rd,	imm	addi rd,	x0, SignExt(imm)
01 (1)	011– – –	–	CI	c.lui	rd,	imm	lui rd,	{14{imm5}, imm}
01 (1)	011– – –	–	CI	c.addi16sp sp, imm	addi sp,	sp, SignExt(imm)*16
01 (1)	100 –00	–	CB'	c.srli rd',	imm	srli rd', rd', imm
01 (1)	100 –01	–	CB'	c.srai rd',	imm	srai rd', rd', imm
01 (1)	100 –10	–	CB'	c.andi rd',	imm	andi rd', rd', SignExt(imm)
01 (1)	100011	00	CS'	c.sub	rd',	rs2'	sub rd', rd', rs2'
01 (1)	100011	01	CS'	c.xor	rd',	rs2'	xor rd', rd', rs2'
01 (1)	100011	10	CS'	c.or	rd',	rs2'	or	rd', rd', rs2'
01 (1)	100011	11	CS'	c.and	rd',	rs2'	and rd', rd', rs2'
01 (1)	101– – –	–	CJ	c.j	label	jal x0,	label
01 (1)	110– – –	–	CB	c.beqz rs1',	label	beq rs1', x0, label
01 (1)	111– – –	–	CB	c.bnez rs1',	label	bne rs1', x0, label
10 (2)	000– – –	–	CI	c.slli rd,	imm	slli rd,	rd, imm
10 (2)	001– – –	–	CI	c.fldsp fd,	imm	fld fd,	(ZeroExt(imm)*8)(sp)
10 (2)	010– – –	–	CI	c.lwsp rd,	imm	lw	rd,	(ZeroExt(imm)*4)(sp)
10 (2)	011– – –	–	CI	c.flwsp fd,	imm	flw fd,	(ZeroExt(imm)*4)(sp)
10 (2)	1000– –	–	CR	c.jr	rs1	(rs1≠0,rs2=0)	jalr x0,	rs1, 0
10 (2)	1000– –	–	CR	c.mv	rd,	rs2	(rd ≠0,rs2≠0)	add rd,	x0, rs2
10 (2)	1001– –	–	CR	c.ebreak	(rs1=0,rs2=0)	ebreak
10 (2)	1001– –	–	CR	c.jalr rs1	(rs1≠0,rs2=0)	jalr ra,	rs1, 0
10 (2)	1001– –	–	CR	c.add	rd,	rs2	(rs1≠0,rs2≠0)	add rd,	rd, rs2
10 (2)	101– – –	–	CSS	c.fsdsp fs2,	imm	fsd fs2, (ZeroExt(imm)*8)(sp)
10 (2)	110– – –	–	CSS	c.swsp rs2,	imm	sw	rs2, (ZeroExt(imm)*4)(sp)
10 (2)	111– – –	–	CSS	c.fswsp fs2,	imm	fsw fs2, (ZeroExt(imm)*4)(sp)
rs1', rs2', rd': 3-bit register designator for registers 8 –15: 0002 = x8 or f8, 0012 = x9 or f9, etc.
 
Table B.7 RISC-V pseudoinstructions
Pseudoinstruction	RISC-V Instructions	Description	Operation
nop	addi x0, x0, 0	no operation	
li	rd, imm11:0	addi rd, x0, imm11:0	load 12-bit immediate	rd = SignExtend(imm11:0)
li	rd, imm31:0	lui	rd, imm	*
31:12
addi rd, rd, imm11:0	load 32-bit immediate	rd = imm31:0
mv	rd, rs1	addi rd, rs1, 0	move (also called “register copy”)	rd = rs1
not rd, rs1	xori rd, rs1, —1	one’s complement	rd = ~rs1
neg rd, rs1	sub	rd, x0, rs1	two’s complement	rd = —rs1
seqz rd, rs1	sltiu rd, rs1, 1	set if = 0	rd = (rs1 == 0)
snez rd, rs1	sltu rd, x0, rs1	set if ≠ 0	rd = (rs1 ≠ 0)
sltz rd, rs1	slt	rd, rs1, x0	set if < 0	rd = (rs1 <  0)
sgtz rd, rs1	slt	rd, x0, rs1	set if > 0	rd = (rs1 >  0)
beqz rs1, label	beq	rs1, x0, label	branch if = 0	if (rs1 == 0)	PC = label
bnez rs1, label	bne	rs1, x0, label	branch if ≠ 0	if (rs1 ≠ 0)	PC = label
blez rs1, label	bge	x0, rs1, label	branch if ≤ 0	if (rs1 ≤  0)	PC = label
bgez rs1, label	bge	rs1, x0, label	branch if ≥ 0	if (rs1 ≥  0)	PC = label
bltz rs1, label	blt	rs1, x0, label	branch if < 0	if (rs1 <  0)	PC = label
bgtz rs1, label	blt	x0, rs1, label	branch if > 0	if (rs1 >  0)	PC = label
ble rs1, rs2, label	bge	rs2, rs1, label	branch if ≤	if (rs1 ≤  rs2) PC = label
bgt rs1, rs2, label	blt	rs2, rs1, label	branch if >	if (rs1 >  rs2) PC = label
bleu rs1, rs2, label	bgeu rs2, rs1, label	branch if ≤ (unsigned)	if (rs1 ≤  rs2) PC = label
bgtu rs1, rs2, label	bltu rs2, rs1, offset	branch if > (unsigned)	if (rs1 >  rs2) PC = label
j	label	jal	x0, label	jump	PC = label
jal label	jal	ra, label	jump and link	PC = label,	ra = PC + 4
jr	rs1	jalr x0, rs1, 0	jump register	PC = rs1
jalr rs1	jalr ra, rs1, 0	jump and link register	PC = rs1,	ra = PC + 4
ret	jalr x0, ra, 0	return from function	PC = ra
call label	jal	ra, label	call nearby function	PC = label,	ra = PC + 4
call label	auipc ra, offset	*
31:12
jalr ra, ra, offset11:0	call far away function	PC = PC + offset, ra = PC + 4
la	rd, symbol	auipc rd, symbol	*
31:12
addi rd, rd, symbol11:0	load address of global variable	rd = PC + symbol
l{b|h|w} rd, symbol	auipc	rd, symbol	*
31:12
l{b|h|w} rd, symbol11:0(rd)	load global variable	rd = [PC + symbol]
s{b|h|w} rs2, symbol, rs1	auipc	rs1, symbol	*
31:12
s{b|h|w} rs2, symbol11:0(rs1)	store global variable	[PC + symbol] = rs2
csrr rd, csr	csrrs rd, csr, x0	read CSR	rd = csr
csrw csr, rs1	csrrw x0, csr, rs1	write CSR	csr = rs1
* If bit 11 of the immediate / offset / symbol is 1, the upper immediate is incremented by 1. symbol and offset are the 32-bit PC-relative addresses of a label and a global variable, respectively.
Table B.8 Privileged / CSR instructions
op	funct3	Type	Instruction	Description		Operation
1110011 (115)	000	I	ecall	transfer control to OS	(imm=0)	
1110011 (115)	000	I	ebreak	transfer control to debugger	(imm=1)	
1110011 (115)	000	I	uret	return from user exception	(rs1=0,rd=0,imm=2)	PC = uepc
1110011 (115)	000	I	sret	return from supervisor exception (rs1=0,rd=0,imm=258)	PC = sepc
1110011 (115)	000	I	mret	return from machine exception	(rs1=0,rd=0,imm=770)	PC = mepc
1110011 (115)	001	I	csrrw	rd,csr,rs1	CSR read/write	(imm=CSR number)	rd = csr,csr = rs1
1110011 (115)	010	I	csrrs	rd,csr,rs1	CSR read/set	(imm=CSR number)	rd = csr,csr = csr | rs1
1110011 (115)	011	I	csrrc	rd,csr,rs1	CSR read/clear	(imm=CSR number)	rd = csr,csr = csr & ~rs1
1110011 (115)	101	I	csrrwi	rd,csr,uimm	CSR read/write immediate	(imm=CSR number)	rd = csr,csr = ZeroExt(uimm)
1110011 (115)	110	I	csrrsi	rd,csr,uimm	CSR read/set immediate	(imm=CSR number)	rd = csr,
csr = csr | ZeroExt(uimm)
1110011 (115)	111	I	csrrci	rd,csr,uimm	CSR read/clear immediate	(imm=CSR number)	rd = csr,
csr = csr & ~ZeroExt(uimm)
For privileged / CSR instructions, the 5-bit unsigned immediate, uimm, is encoded in the rs1 field.
 
In Praise of Digital Design and Computer Architecture
RISC-V Edition

Harris and Harris have shown how to design a RISC-V processor from the gates all the way up through the microarchitecture. Their clear explanations combined with their comprehensive approach give a full picture of both digital design and the RISC-V architecture. With the exciting opportunity that students have to run large digital designs on modern FPGAs, this approach is both informative and enlightening.
David A. Patterson University of California, Berkeley

What broad fields Harris and Harris have distilled into one book! As semiconductor manufacturing matures, the importance of digital design and computer architecture will only increase. Readers will find an approachable and comprehensive treatment of both topics and will walk away with a clear understanding of the RISC-V instruction set architecture.
Andrew Waterman SiFive

There are excellent texts for teaching digital design and there are excellent texts for teaching computer hardware organization - and this textbook does both! It is also unique in its ability to connect the dots. The writing makes the RISC-V architecture understandable by building on the basics, and I have found the exercises to be a great resource across multiple courses.
Roy Kravitz Portland State University

When I first read Harris and Harris’s MIPS textbook back in 2008, I thought that it was one of the best books I had ever read for teaching computer architecture. I started using it in my courses immediately. Thirteen years later, I have had the honor of reviewing this new RISC-V edition, and my opinion of their books has not changed: Digital Design and Computer Architecture: RISC-V Edition is an excellent book, very clear, thorough, with a high educational value, and in line with the courses that we teach in the areas of digital design and computer archi- tecture. I look forward to using this RISC-V textbook in my courses.
Daniel Chaver Martinez University Complutense of Madrid
 








Digital Design and
Computer Architecture
RISC-V Edition
 








Digital Design and
Computer Architecture
RISC-V Edition


Sarah L. Harris David Harris





















AMSTERDAM • BOSTON • HEIDELBERG • LONDON NEW YORK • OXFORD • PARIS • SAN DIEGO
SAN FRANCISCO • SINGAPORE • SYDNEY • TOKYO

Morgan Kaufmann is an imprint of Elsevier
 
Morgan Kaufmann is an imprint of Elsevier
50 Hampshire Street, 5th Floor, Cambridge, MA 02139, United States
Copyright © 2022 Elsevier Inc. All rights reserved.
No part of this publication may be reproduced or transmitted in any form or by any means, electronic or mechanical, including photocopying, recording, or any information storage and retrieval system, without permission in writing from the publisher. Details on how to seek permission, further information about the Publisher’s permissions policies and our arrangements with organizations such as the Copyright Clearance Center and the Copyright Licensing Agency, can be found at our website: www.elsevier.com/permissions.
This book and the individual contributions contained in it are protected under copyright by the Publisher (other than as may be noted herein).
Notices
Knowledge and best practice in this eld are constantly changing. As new research and experience broaden our understanding, changes in research methods, professional practices, or medical treatment may become necessary.
Practitioners and researchers must always rely on their own experience and knowledge in evaluating and using any information, methods, compounds, or experiments described herein. In using such information or methods they should be mindful of their own safety and the safety of others, including parties for whom they have a professional responsibility.
To the fullest extent of the law, neither the Publisher nor the authors, contributors, or editors, assume any liability for any injury and/or damage to persons or property as a matter of products liability, negligence or otherwise, or from any use or operation of any methods, products, instructions, or ideas contained in the material herein.
British Library Cataloguing-in-Publication Data
A catalogue record for this book is available from the British Library.
Library of Congress Cataloging-in-Publication Data
A catalog record for this book is available from the Library of Congress.
ISBN: 978-0-12-820064-3



Publisher: Katey Birtcher
Senior Acquisitions Editor: Steve Merken
Editorial Project Manager: Ruby Gammell/Andrae Akeh Senior Project Manager: Manikandan Chandrasekaran Cover Designer: Victoria Pearson Esser
Typeset by MPS Limited, Chennai, India Printed in the United States of America
Last digit is the print number: 9 8 7 6 5 4 3 2 1
 
Contents





Preface	xix
Features	xx
Online Supplements	xxi
How to Use the Software Tools in a Course	xxii
Labs	xxiii
RVfpga	xxiii
Bugs	xxiv
Acknowledgments	xxiv
About the Authors	xxv
Chapter 1 From Zero to One	1
1.1	The Game Plan	1
1.2	The Art of Managing Complexity	2
1.2.1	Abstraction	2
1.2.2	Discipline	3
1.2.3	The Three -Y’s	4
1.3	The Digital Abstraction	5
1.4	Number Systems	7
1.4.1	Decimal Numbers	7
1.4.2	Binary Numbers	7
1.4.3	Hexadecimal Numbers	9
1.4.4	Bytes, Nibbles, and All That Jazz	11
1.4.5	Binary Addition	12
1.4.6	Signed Binary Numbers	13
1.5	Logic Gates	17
1.5.1	NOT Gate	18
1.5.2	Buffer	18
1.5.3	AND Gate	18
1.5.4	OR Gate	19
1.5.5	Other Two-Input Gates	19
1.5.6	Multiple-Input Gates	19
1.6	Beneath the Digital Abstraction	20
1.6.1	Supply Voltage	20
1.6.2	Logic Levels	20
1.6.3	Noise Margins	21
ix
 
x	CONTENTS	
			
1.6.4	DC Transfer Characteristics	22
			1.6.5	The Static Discipline	22
		1.7	CMOS	Transistors	24
	1.7.1	Semiconductors	25
	1.7.2	Diodes	25
	1.7.3	Capacitors	26
	1.7.4	nMOS and pMOS Transistors	26
	1.7.5	CMOS NOT Gate	29
	1.7.6	Other CMOS Logic Gates	29
	1.7.7	Transmission Gates	31
	1.7.8	Pseudo-nMOS Logic	31
1.8	Power Consumption	32
1.9	Summary and a Look Ahead	34
Exercises	36
Interview Questions	50
Chapter 2 Combinational Logic Design	53
2.1	Introduction	53
2.2	Boolean Equations	56
2.2.1	Terminology	56
2.2.2	Sum-of-Products Form	56
2.2.3	Product-of-Sums Form	58
2.3	Boolean Algebra	58
2.3.1	Axioms	59
2.3.2	Theorems of One Variable	59
2.3.3	Theorems of Several Variables	60
2.3.4	The Truth Behind It All	62
2.3.5	Simplifying Equations	63
2.4	From Logic to Gates	64
2.5	Multilevel Combinational Logic	67
2.5.1	Hardware Reduction	68
2.5.2	Bubble Pushing	69
2.6	X’s and Z’s, Oh My	71
2.6.1	Illegal Value: X	71
2.6.2	Floating Value: Z	72
2.7	Karnaugh Maps	73
2.7.1	Circular Thinking	74
2.7.2	Logic Minimization with K-Maps	75
2.7.3	Don’t Cares	79
2.7.4	The Big Picture	80
2.8	Combinational Building Blocks	81
2.8.1	Multiplexers	81
2.8.2	Decoders	84
 
CONTENTS	xi
2.9	Timing	86
2.9.1	Propagation and Contamination Delay	86
2.9.2	Glitches	90
2.10	Summary	93
Exercises	95
Interview Questions	104
Chapter 3 Sequential Logic Design	107
3.1	Introduction	107
3.2	Latches and Flip-Flops	107
3.2.1	SR Latch	109
3.2.2	D Latch	111
3.2.3	D FIip-Flop	112
3.2.4	Register	112
3.2.5	Enabled Flip-Flop	113
3.2.6	Resettable Flip-Flop	114
3.2.7	Transistor-Level Latch and Flip-Flop
Designs	114
3.2.8	Putting It All Together	116
3.3	Synchronous Logic Design	117
3.3.1	Some Problematic Circuits	117
3.3.2	Synchronous Sequential Circuits	118
3.3.3	Synchronous and Asynchronous
Circuits	120
3.4	Finite State Machines	121
3.4.1	FSM Design Example	121
3.4.2	State Encodings	127
3.4.3	Moore and Mealy Machines	130
3.4.4	Factoring State Machines	132
3.4.5	Deriving an FSM from a Schematic	135
3.4.6	FSM Review	138
3.5	Timing of Sequential Logic	139
3.5.1	The Dynamic Discipline	140
3.5.2	System Timing	140
3.5.3	Clock Skew	146
3.5.4	Metastability	149
3.5.5	Synchronizers	150
3.5.6	Derivation of Resolution Time	152
3.6	Parallelism	155
3.7	Summary	159
Exercises	160
Interview Questions	169
 
xii	CONTENTS
Chapter 4 Hardware Description Languages	171
4.1	Introduction	171
4.1.1	Modules	171
4.1.2	Language Origins	172
4.1.3	Simulation and Synthesis	173
4.2	Combinational Logic	175
4.2.1	Bitwise Operators	175
4.2.2	Comments and White Space	178
4.2.3	Reduction Operators	178
4.2.4	Conditional Assignment	179
4.2.5	Internal Variables	180
4.2.6	Precedence	182
4.2.7	Numbers	183
4.2.8	Z’s and X’s	184
4.2.9	Bit Swizzling	186
4.2.10	Delays	186
4.3	Structural Modeling	188
4.4	Sequential Logic	191
4.4.1	Registers	191
4.4.2	Resettable Registers	192
4.4.3	Enabled Registers	194
4.4.4	Multiple Registers	195
4.4.5	Latches	196
4.5	More Combinational Logic	196
4.5.1	Case Statements	199
4.5.2	If Statements	200
4.5.3	Truth Tables with Don’t Cares	203
4.5.4	Blocking and Nonblocking Assignments	203
4.6	Finite State Machines	207
4.7	Data Types	211
4.7.1	SystemVerilog	212
4.7.2	VHDL	213
4.8	Parameterized Modules	215
4.9	Testbenches	218
4.10	Summary	222
Exercises	224
Interview Questions	235
Chapter 5 Digital Building Blocks	237
5.1	Introduction	237
5.2	Arithmetic Circuits	237
5.2.1	Addition	237
5.2.2	Subtraction	244
 
CONTENTS	xiii
5.2.3	Comparators	245
5.2.4	ALU	247
5.2.5	Shifters and Rotators	251
5.2.6	Multiplication	253
5.2.7	Division	254
5.2.8	Further Reading	255
5.3	Number Systems	256
5.3.1	Fixed-Point Number Systems	256
5.3.2	Floating-Point Number Systems	257
5.4	Sequential Building Blocks	261
5.4.1	Counters	261
5.4.2	Shift Registers	262
5.5	Memory Arrays	265
5.5.1	Overview	265
5.5.2	Dynamic Random Access Memory (DRAM)	267
5.5.3	Static Random Access Memory (SRAM)	268
5.5.4	Area and Delay	268
5.5.5	Register Files	269
5.5.6	Read Only Memory (ROM)	269
5.5.7	Logic Using Memory Arrays	271
5.5.8	Memory HDL	272
5.6	Logic Arrays	272
5.6.1	Programmable Logic Array (PLA).	275
5.6.2	Field Programmable Gate Array (FPGA)	276
5.6.3	Array Implementations	282
5.7	Summary	283
Exercises	285
Interview Questions	297
Chapter 6 Architecture	299
6.1	Introduction	299
6.2	Assembly Language	300
6.2.1	Instructions	301
6.2.2	Operands: Registers, Memory, and Constants	302
6.3	Programming	308
6.3.1	Program Flow	308
6.3.2	Logical, Shift, and Multiply Instructions	308
6.3.3	Branching	311
6.3.4	Conditional Statements	313
6.3.5	Getting Loopy	315
6.3.6	Arrays	317
6.3.7	Function Calls	320
6.3.8	Pseudoinstructions	330
 
xiv	CONTENTS
6.4	Machine Language	332
6.4.1	R-Type Instructions	332
6.4.2	l-Type Instructions	334
6.4.3	S/B-Type Instructions	336
6.4.4	U/J-Type Instructions	338
6.4.5	Immediate Encodings	340
6.4.6	Addressing Modes	341
6.4.7	Interpreting Machine Language Code	342
6.4.8	The Power of the Stored Program	343
6.5	Lights, Camera, Action: Compiling, Assembling,
and Loading	344
6.5.1	The Memory Map	344
6.5.2	Assembler Directives	346
6.5.3	Compiling	348
6.5.4	Assembling	350
6.5.5	Linking	353
6.5.6	Loading	355
6.6	Odds and Ends	355
6.6.1	Endianness	355
6.6.2	Exceptions	356
6.6.3	Signed and Unsigned Instructions	360
6.6.4	Floating-Point Instructions	361
6.6.5	Compressed Instructions	362
6.7	Evolution of the RISC-V Architecture	363
6.7.1	RISC-V Base Instruction Sets and Extensions	364
6.7.2	Comparison of RISC-V and MIPS Architectures	365
6.7.3	Comparison of RISC-V and ARM Architectures	365
6.8	Another Perspective: x86 Architecture	366
6.8.1	x86 Registers	366
6.8.2	x86 Operands	367
6.8.3	Status Flags	369
6.8.4	x86 Instructions	369
6.8.5	x86 Instruction Encoding	371
6.8.6	Other x86 Peculiarities	372
6.8.7	The Big Picture	373
6.9	Summary	374
Exercises	375
Interview Questions	390
Chapter 7 Microarchitecture	393
7.1	Introduction	393
7.1.1	Architectural State and Instruction Set	393
7.1.2	Design Process	394
7.1.3	Microarchitectures	396
 
CONTENTS	xv
7.2	Performance Analysis	397
7.3	Single-Cycle Processor	398
7.3.1	Sample Program	399
7.3.2	Single-Cycle Datapath	399
7.3.3	Single-Cycle Control	407
7.3.4	More Instructions	410
7.3.5	Performance Analysis	412
7.4	Multicycle Processor	415
7.4.1	Multicycle Datapath	416
7.4.2	Multicycle Control	422
7.4.3	More Instructions	432
7.4.4	Performance Analysis	435
7.5	Pipelined Processor	439
7.5.1	Pipelined Datapath	441
7.5.2	Pipelined Control	443
7.5.3	Hazards	443
7.5.4	Performance Analysis	454
7.6	HDL Representation	456
7.6.1	Single-Cycle Processor	457
7.6.2	Generic Building Blocks	461
7.6.3	Testbench	464
7.7	Advanced Microarchitecture	468
7.7.1	Deep Pipelines	468
7.7.2	Micro-Operations	469
7.7.3	Branch Prediction	470
7.7.4	Superscalar Processors	472
7.7.5	Out-of-Order Processor	473
7.7.6	Register Renaming	476
7.7.7	Multithreading	478
7.7.8	Multiprocessors	479
7.8	Real-World Perspective: Evolution of
RISC-V Microarchitecture	482
7.9	Summary	486
Exercises	488
Interview Questions	497
Chapter 8 Memory Systems	499
8.1	Introduction	499
8.2	Memory System Performance Analysis	503
8.3	Caches	505
8.3.1	What Data is Held in the Cache?	505
8.3.2	How is Data Found?	506
8.3.3	What Data is Replaced?	514
8.3.4	Advanced Cache Design	515
 
xvi	CONTENTS
8.4	Virtual Memory	519
8.4.1	Address Translation	522
8.4.2	The Page Table	523
8.4.3	The Translation Lookaside Buffer	525
8.4.4	Memory Protection	526
8.4.5	Replacement Policies	527
8.4.6	Multilevel Page Tables	527
8.5	Summary	530
Epilogue	530
Exercises	532
Interview Questions	541
Chapter 9 Embedded I/O Systems	542
9.1	Introduction	542
Chapter 9 is available as an online supplement	542.e1
9.1	Introduction	542.e1
9.2	Memory-Mapped I/O	542.e1
9.3	Embedded I/O Systems	542.e3
9.3.1	RED-V Board	542.e3
9.3.2	FE310-G002 System-on-Chip	542.e5
9.3.3	General-Purpose Digital I/O	542.e5
9.3.4	Device Drivers	542.e10
9.3.5	Serial I/O	542.e14
9.3.6	Timers	542.e29
9.3.7	Analog I/O	542.e30
9.3.8	Interrupts	542.e39
9.4	Other Microcontroller Peripherals	542.e43
9.4.1	Character LCDs	542.e43
9.4.2	VGA Monitor	542.e45
9.4.3	Bluetooth Wireless Communication	542.e53
9.4.4	Motor Control	542.e54
9.5	Summary	542.e64
Appendix A Digital System Implementation	543
A.1	Introduction	543
Appendix A is available as an online supplement	543.e1
A.1	Introduction	543.e1
A.2	74xx Logic	543.e1
A.2.1	Logic Gates	543.e2
A.2.2	Other Functions	543.e2
 
CONTENTS	xvii
A.3	Programmable Logic	543.e2
A.3.1	PROMs	543.e2
A.3.2	PLAs	543.e6
A.3.3	FPGAs	543.e7
A.4	Application-Speci!c Integrated Circuits	543.e9
A.5	Datasheets	543.e9
A.6	Logic Families	543.e15
A.7	Switches and Light-Emitting Diodes	543.e17
A.7.1	Switches	543.e17
A.7.2	LEDs	543.e18
A.8	Packaging and Assembly	543.e19
A.8.1	Packages	543.e19
A.8.2	Breadboards	543.e20
A.8.3	Printed Circuit Boards	543.e20
A.8.4	Putting It All Together	543.e23
A.9	Transmission Lines	543.e23
A.9.1	Matched Termination	543.e24
A.9.2	Open Termination	543.e26
A.9.3	Short Termination	543.e27
A.9.4	Mismatched Termination	543.e27
A.9.5	When to Use Transmission Line Models	543.e30
A.9.6	Proper Transmission Line Terminations	543.e30
A.9.7	Derivation of Z0	543.e32
A.9.8	Derivation of the Re ection Coef cient	543.e33
A.9.9	Putting It All Together	543.e34
A.10	Economics	543.e35
Appendix B RISC-V Instruction Set Summary	544
Appendix C C Programming	545
C.1	Introduction	545
Appendix C is available as an online supplement	545.e1
C.1	Introduction	545.e1
C.2	Welcome to C	545.e3
C.2.1	C Program Dissection	545.e3
C.2.2	Running a C Program	545.e4
C.3	Compilation	545.e5
C.3.1	Comments	545.e5
C.3.2	#define	545.e5
C.3.3	#include	545.e6
 
xviii	CONTENTS


C.4	Variables	545.e7
C.4.1	Primitive Data Types	545.e8
C.4.2	Global and Local Variables	545.e9
C.4.3	Initializing Variables	545.e11
C.5	Operators	545.e11
C.6	Function Calls	545.e15
C.7	Control-Flow Statements	545.e16
C.7.1	Conditional Statements	545.e17
C.7.2	Loops	545.e19
C.8	More Data Types	545.e21
C.8.1	Pointers	545.e21
C.8.2	Arrays	545.e23
C.8.3	Characters	545.e27
C.8.4	Strings	545.e27
C.8.5	Structures	545.e29
C.8.6	typedef	545.e31
C.8.7	Dynamic Memory Allocation	545.e32
C.8.8	Linked Lists	545.e33
C.9	Standard Libraries	545.e35
C.9.1	stdio	545.e35
C.9.2	stdlib	545.e40
C.9.3	math	545.e42
C.9.4	string	545.e42
C.10	Compiler and Command Line Options	545.e43
C.10.1	Compiling Multiple C Source Files	545.e43
C.10.2	Compiler Options	545.e43
C.10.3	Command Line Arguments	545.e44
C.11	Common Mistakes	545.e44

Further Reading	547

Index	549
 
Preface



This book is unique in its treatment in that it presents digital logic design from the perspective of computer architecture, starting at the beginning with 1’s and 0’s and leading through to the design of a microprocessor.
We believe that building a microprocessor is a special rite of passage for engineering and computer science students. The inner workings of a processor seem almost magical to the uninitiated yet prove to be straightforward when carefully explained. Digital design in and of itself is a powerful and exciting subject. Assembly language programming unveils the inner language spoken by the processor. Microarchitecture is the link that brings it all together.
The first two versions of this increasingly popular text cover the MIPS and ARM architectures. As one of the original Reduced Instruction Set Computing architectures, MIPS is clean and excep- tionally easy to understand and build. MIPS remains an important architecture, as it has inspired many of the subsequent architectures, including RISC-V. The ARM architecture has exploded in popu- larity over the past several decades because of its efficiency and rich ecosystem. More than 50 billion ARM processors have been shipped, and more than 75% of humans on the planet use products with ARM processors.
Over the past decade, RISC-V has emerged as an increasingly important architecture, both pedagogically and commercially. As the first widely used open-source computer architecture, RISC-V offers the simplicity of MIPS with the flexibility and features of modern processors.
Pedagogically, the learning objectives of the MIPS, ARM, and RISC-V editions are identical. The RISC-V architecture has a number of features, including extendibility and compressed instructions, that con- tribute to its efficiency but add a small amount of complexity. The three microarchitectures are also similar, with MIPS and RISC-V architectures sharing many similarities. We expect to offer MIPS, ARM, and RISC-V editions as long as the market demands.




xix
 
xx	PREFACE


FEATURES
Side-by-Side Coverage of SystemVerilog and VHDL
Hardware description languages (HDLs) are at the center of modern digital design practices. Unfortunately, designers are evenly split between the two dominant languages, SystemVerilog and VHDL. This book introduces HDLs in Chapter 4 as soon as combinational and sequential logic design has been covered. HDLs are then used in Chapters 5 and 7 to design larger building blocks and entire processors. Nevertheless, Chapter 4 can be skipped and the later chapters are still accessible for courses that choose not to cover HDLs.
This book is unique in its side-by-side presentation of SystemVerilog and VHDL, enabling the reader to learn the two languages. Chapter 4 describes principles that apply to both HDLs, and then provides language- specific syntax and examples in adjacent columns. This side-by-side treatment makes it easy for an instructor to choose either HDL and for the reader to transition from one to the other, either in a class or in professional practice.

RISC-V Architecture and Microarchitecture
Chapters 6 and 7 offer in-depth coverage of the RISC-V architecture and microarchitecture. RISC-V is an ideal architecture because it is a real architecture shipped in an increasing number of commercial products, yet it is streamlined and easy to learn. Moreover, because of its popularity in the commercial and hobbyist worlds, simulation and development tools exist for the RISC-V architecture.

Real-World Perspectives
In addition to the real-world perspective in discussing the RISC-V architecture, Chapter 6 illustrates the architecture of Intel x86 pro- cessors to offer another perspective. Chapter 9 (available as an online supplement) also describes peripherals in the context of SparkFun’s RED-V RedBoard, a popular development board that centers on SiFive’s Freedom E310 RISC-V processor. These real-world perspective chapters show how the concepts in the chapters relate to the chips found in many PCs and consumer electronics.

Accessible Overview of Advanced Microarchitecture
Chapter 7 includes an overview of modern high-performance micro- architectural features, including branch prediction, superscalar, and out-of-order operation, multithreading, and multicore processors. The
 
PREFACE	xxi


treatment is accessible to a student in a first course and shows how the microarchitectures in the book can be extended to modern processors.
End-of-Chapter Exercises and Interview Questions
The best way to learn digital design is to do it. Each chapter ends with numerous exercises to practice the material. The exercises are followed by a set of interview questions that our industrial colleagues have asked students who are applying for work in the field. These questions pro- vide a helpful glimpse into the types of problems that job applicants will typically encounter during the interview process. Exercise solutions are available via the book’s companion and instructor websites.

ONLINE SUPPLEMENTS
Supplementary materials are available online at ddcabook.com or the publisher’s website: https://www.elsevier.com/books-and-journals/ book-companion/9780128200643. These companion sites (accessible to all readers) include the following:
	Links to video lectures
	Solutions to odd-numbered exercises
	Figures from the text in PDF and PPTX formats
  Links to professional-strength computer-aided design (CAD) tools from Intel®
 Instructions on how to use PlatformIO (an extension of Visual Studio Code) to compile, assemble, and simulate C and assembly code for RISC-V processors
	Hardware description language (HDL) code for the RISC-V processor
	Intel’s Quartus helpful hints
	Lecture slides in PowerPoint (PPTX) format
	Sample course and laboratory materials
	List of errata
The instructor site (accessible to instructors who register at https:// inspectioncopy.elsevier.com) includes the following:
	Solutions to all exercises
	Laboratory solutions

EdX MOOC
This book also has a companion Massive Open Online Course (MOOC) through EdX. The course includes video lectures, interactive practice
 
xxii	PREFACE


problems, and interactive problem sets and labs. The MOOC is divided into two parts: Digital Design (ENGR 85A) and Computer Architecture (ENGR85B) offered by HarveyMuddX (on EdX, search for “Digital Design HarveyMuddX” and “Computer Architecture HarveyMuddX”). EdX does not charge for access to the videos but does charge for the inter- active exercises and certificate. EdX offers discounts for students with financial need.

HOW TO USE THE SOFTWARE TOOLS IN A COURSE
Intel’s Quartus Software
The Quartus software, either Web or Lite Edition, is a free version of Intel’s professional-strength Quartus™ FPGA design tools. It allows students to enter their digital designs in schematic or using either the SystemVerilog or the VHDL hardware description language (HDL). After entering the design, students can simulate their circuits using the ModelSim™-Intel FPGA Edition or Starter Edition, which is available with Intel’s Quartus software. Quartus also includes a built-in logic synthesis tool that supports both SystemVerilog and VHDL.
The difference between the Web or Lite Edition and the Pro Edition is that the Web or Lite Edition supports a subset of the most common Altera FPGAs. The free versions of ModelSim degrade performance for simulations with more than 10,000 lines of HDL, whereas the professional version of ModelSim does not.

PlatformIO
PlatformIO, which is an extension of Visual Studio Code, serves as a soft- ware development kit (SDK) for RISC-V. With the explosion of SDKs for each new platform, PlatformIO has streamlined the process of program- ming and using various processors by providing a unified interface for a large number of platforms and devices. It is available as a free download and can be used with SparkFun’s RED-V RedBoard, as described in the labs provided on the companion website. PlatformIO provides access to a commercial RISC-V compiler and allows students to write both C and assembly programs, compile them, and then run and debug them on SparkFun’s RED-V RedBoard (see Chapter 9 and the accompanying labs).

Venus RISC-V Assembly Simulator
The Venus Simulator (available at: https://www.kvakil.me/venus/) is a web-based RISC-V assembly simulator. Programs are written (or copy/ pasted) in the Editor tab and then simulated and run in the Simulator tab. Registers and memory contents can be viewed as the program runs.
 
PREFACE	xxiii


LABS
The companion site includes links to a series of labs that cover topics from digital design through computer architecture. The labs teach stu- dents how to use the Quartus tools to enter, simulate, synthesize, and implement their designs. The labs also include topics on C and assem- bly language programming using PlatformIO and SparkFun’s RED-V RedBoard.
After synthesis, students can implement their designs using the Altera DE2, DE2-115, DE0, or other FPGA board. The labs are written to target the DE2 or DE-115 boards. These powerful and competitively priced boards are available from de2-115.terasic.com. The board con- tains an FPGA that can be programmed to implement student designs. We provide labs that describe how to implement a selection of designs on the DE2-115 board using the Quartus software.
To run the labs, students will need to download and install Intel’s Quartus Web or Lite Edition and Visual Studio Code with the PlatformIO extension. Instructors may also choose to install the tools on lab machines. The labs include instructions on how to implement the projects on the DE2/DE2-115 board. The implementation step may be skipped, but we have found it of great value. We have tested the labs on Windows, but the tools are also available for Linux.

RVfpga
RISC-V FPGA, also referred to as RVfpga, is a free two-course sequence that can be completed after learning the material in this book. The first course shows how to target a commercial RISC-V core to an FPGA, pro- gram it using RISC-V assembly or C, add peripherals to it, and analyze and modify the core and memory system, including adding instructions to the core. This course uses the open-source SweRVolf system-on-chip (SoC) (https://github.com/chipsalliance/Cores-SweRVolf), which is based on Western Digital’s open-source commercial SweRV EH1 core (https:// www.westerndigital.com/company/innovations/risc-v). The course also shows how to use Verilator, an open-source HDL simulator, and Western Digital’s Whisper, an open-source RISC-V instruction set simulator (ISS). RVfpga-SoC, the second course, shows how to build an SoC based on SweRVolf using building blocks such as the SweRV EH1 core, inter- connect, and memories. The course then guides the user in loading and running the Zephyr operating system on the RISC-V SoC. All neces- sary software and system source code (Verilog/SystemVerilog files) are free, and the courses may be completed in simulation, so no hardware is required. RVfpga materials are freely available with registration from the Imagination Technologies University Programme: https://university. imgtec.com/rvfpga/.
 
xxiv	PREFACE

BUGS
As all experienced programmers know, any program of significant com- plexity undoubtedly contains bugs. So, too, do books. We have taken great care to find and squash the bugs in this book. However, some errors undoubtedly do remain. We will maintain a list of errata on the book’s webpage.
Please send your bug reports to ddcabugs@gmail.com. The first person to report a substantive bug with a fix that we use in a future printing will be rewarded with a $1 bounty!

ACKNOWLEDGMENTS
We appreciate the hard work of Steve Merken, Nate McFadden, Ruby Gammell, Andrae Akeh, Manikandan Chandrasekaran, and the rest of the team at Morgan Kaufmann who made this book happen. We love the art of Duane Bibby, whose cartoons enliven the chapters.
We thank Matthew Watkins, who contributed the section on Heterogeneous Multiprocessors in Chapter 7, and Josh Brake, who contributed to Chapter 9 on Embedded I/O Systems. We greatly appre- ciate the work of Mateo Markovic and Geordie Ryder, who reviewed the book and contributed to the exercise solutions. Numerous other reviewers also substantially improved the book. They include Daniel Chaver Martinez, Roy Kravitz, Zvonimir Bandic, Giuseppe Di Luna, Steffen Paul, Ravi Mittal, Jennifer Winikus, Hesham Omran, Angel Solis, Reiner Dizon, and Olof Kindgren. We also appreciate the students in our courses at Harvey Mudd College and UNLV who have given us help- ful feedback on drafts of this textbook. And last, but not least, we both thank our families for their love and support.
 
About the Authors



Sarah L. Harris is an Associate Professor of Electrical and Computer Engineering at the University of Nevada, Las Vegas. She received her Ph.D. and M.S. in Electrical Engineering from Stanford University. Sarah has also worked with Hewlett-Packard, the San Diego Supercomputer Center, and NVIDIA. Sarah loves teaching, exploring and developing new technologies, traveling, playing the guitar and various other instru- ments, and spending time with her family. Her recent research includes designing bio-inspired prosthetics and implementing machine-learning algorithms in hardware.

David Harris is the Harvey S. Mudd Professor of Engineering Design and Associate Department Chair at Harvey Mudd College. He received his Ph.D. in electrical engineering from Stanford University and his M.Eng. in electrical engineering and computer science from MIT. Before attending Stanford, he worked at Intel as a logic and circuit designer on the Itanium and Pentium II processors. Since then, he has consulted at Broadcom, Sun Microsystems, Hewlett-Packard, Evans & Sutherland, and other design companies. David’s passions include teaching, build- ing chips and airplanes, and exploring the outdoors. When he is not at work, he can usually be found hiking, flying, and spending time with his family. David holds about a dozen patents and is the author of three other textbooks on chip design, as well as seven guidebooks to the Southern California mountains.














xxv
 
 
 
From Zero to One	1
 






1.1 THE GAME PLAN
Microprocessors have revolutionized our world during the past three decades. A laptop computer today has far more capability than a room-sized mainframe of yesteryear. A luxury automobile contains about 100 microprocessors. Advances in microprocessors have made cell phones and the Internet possible, have vastly improved medicine, and have transformed how war is waged. Worldwide semiconductor industry sales have grown from US $21 billion in 1985 to $400 billion in 2020, and microprocessors are a major segment of these sales. We believe that microprocessors are not only technically, economi- cally, and socially important, but are also an intrinsically fascinating human invention. By the time you finish reading this book, you will know how to design and build your own microprocessor. The skills you learn along the way will prepare you to design many other digital systems.
We assume that you have a basic familiarity with electricity, some prior programming experience, and a genuine interest in understanding what goes on under the hood of a computer. This book focuses on the design of digital systems, which operate on 1’s and 0’s. We begin with digital logic gates that accept 1’s and 0’s as inputs and produce 1’s and 0’s as outputs. We then explore how to combine logic gates into more complicated modules, such as adders and memories. Then, we shift gears to programming in assembly language, the native tongue of the micro- processor. Finally, we put gates together to build a microprocessor that runs these assembly language programs.
A great advantage of digital systems is that the building blocks are quite simple: just 1’s and 0’s. They do not require grungy mathematics or a profound knowledge of physics. Instead, the designer’s challenge is to combine these simple blocks into complicated systems. A microprocessor may be the first system that you build that is too complex to fit in your

Digital Design and Computer Architecture, RISC-V Edition. DOI: 10.1016/B978-0-12-820064-3.00001-5
Copyright © 2022 Elsevier Inc. All rights reserved.
 

1.1	The Game Plan
1.2	The Art of Managing Complexity
1.3	The Digital Abstraction
1.4	Number Systems
1.5	Logic Gates
1.6	Beneath the Digital Abstraction
1.7	CMOS Transistors*
1.8	Power Consumption*
1.9	Summary and a Look Ahead Exercises
Interview Questions



Application  >”hello
Software  world!”
Operating Systems

Architecture
Micro- architecture
Logic	
Digital Circuits
Analog	
Circuits
Devices	 

Physics

1
 
2	CHAPTER ONE
 
From Zero to One
 


head all at once. One of the major themes woven through this book is how to manage complexity.

1.2 THE ART OF MANAGING COMPLEXITY
One of the characteristics that separates an engineer or computer scien- tist from a layperson is a systematic approach to managing complexity. Modern digital systems are built from millions or billions of transistors. No human being could understand these systems by writing equations describing the movement of electrons in each transistor and solving all of the equations simultaneously. You will need to learn to manage com- plexity to understand how to build a microprocessor without getting mired in a morass of detail.

 











Programs

Device Drivers

Instructions Registers

Datapaths Controllers

Adders Memories

AND Gates NOT Gates

Amplifiers Filters

Transistors Diodes

Electrons

Figure 1.1 Levels of abstraction for an electronic computing system
 
1.2.1	Abstraction
The critical technique for managing complexity is abstraction: hid- ing details when they are not important. A system can be viewed from many different levels of abstraction. For example, American politicians abstract the world into cities, counties, states, and countries. A county contains multiple cities and a state contains many counties. When a politician is running for president, the politician is mostly interested in how the state as a whole will vote rather than how each county votes, so the state is the most useful level of abstraction. On the other hand, the Census Bureau measures the population of every city, so the agency must consider the details of a lower level of abstraction.
Figure 1.1 illustrates levels of abstraction for an electronic computer system, along with typical building blocks at each level. At the lowest level of abstraction is the physics, the motion of electrons. The behav- ior of electrons is described by quantum mechanics and Maxwell’s equations. Our system is constructed from electronic devices such as transistors (or vacuum tubes, once upon a time). These devices have well-defined connection points called terminals and can be modeled by the relationship between voltage and current as measured at each termi- nal. By abstracting to this device level, we can ignore the individual elec- trons. The next level of abstraction is analog circuits, in which devices are assembled to create components such as amplifiers. Analog circuits input and output a continuous range of voltages. Digital circuits, such as logic gates, restrict the voltages to discrete ranges, which we will use to indicate 0 and 1. In logic design, we build more complex structures, such as adders or memories, from digital circuits.
Microarchitecture links the logic and architecture levels of abstrac- tion. The architecture level of abstraction describes a computer from the programmer’s perspective. For example, the Intel x86 architecture
 
1.2	The Art of Managing Complexity	3


used by microprocessors in most personal computers (PCs) is defined by a set of instructions and registers (memory for temporarily storing variables) that the programmer is allowed to use. Microarchitecture involves combining logic elements to execute the instructions defined by the architecture. A particular architecture can be implemented by one of many different microarchitectures with different price/perfor- mance/power trade-offs. For example, the Intel Core i7, the Intel 80486, and the AMD Athlon all implement the x86 architecture with different microarchitectures.
Moving into the software realm, the operating system handles low-level details, such as accessing a hard drive or managing memory. Finally, the application software uses these facilities provided by the operating system to solve a problem for the user. Thanks to the power of abstraction, your grandmother can surf the Web without any regard for the quantum vibrations of electrons or the organization of the memory in her computer.
This book focuses on the levels of abstraction from digital circuits through computer architecture. When you are working at one level of abstraction, it is good to know something about the levels of abstraction immediately above and below where you are working. For example, a computer scientist cannot fully optimize code without understanding the architecture for which the program is being written. A device engineer cannot make wise trade-offs in transistor design without understanding the circuits in which the transistors will be used. We hope that by the time you finish reading this book, you can pick the level of abstraction appropriate to solving your problem and evaluate the impact of your design choices on other levels of abstraction.

1.2.2	Discipline
Discipline is the act of intentionally restricting your design choices so that you can work more productively at a higher level of abstraction. Using interchangeable parts is a familiar application of discipline. One of the famous early examples of interchangeable parts was in automo- bile manufacturing. Although the modern gas-powered car dates back to the German Benz Patent-Motorwagen of 1886, early cars were hand- crafted by skilled tradesmen, a time-consuming and expensive process. Henry Ford made a key advance in 1908 by focusing on mass produc- tion with interchangeable parts and moving assembly lines.
The discipline of interchangeable parts revolutionized the indus- try. By limiting the components to a standardized set with well-defined tolerances, cars could be assembled and repaired much faster and with less skill. The car builder no longer concerned himself with lower lev- els of abstraction, such as fitting a door to a nonstandardized opening.
 
4	CHAPTER ONE
 
From Zero to One
 


The Model T Ford became the most-produced car of its era, selling over 15 million units. Another example of discipline was Ford’s famous say- ing: “Any customer can have a car painted any color that he wants so long as it is black.”
In the context of this book, the digital discipline will be very import- ant. Digital circuits use discrete voltages, whereas analog circuits use continuous voltages. Therefore, digital circuits are a subset of analog cir- cuits and in some sense must be capable of less than the broader class of analog circuits. However, digital circuits are much simpler to design. By limiting ourselves to digital circuits, we can easily combine compo- nents into sophisticated systems that ultimately outperform those built from analog components in many applications. For example, digital tele- visions, compact disks (CDs), and cell phones are replacing their analog predecessors.

1.2.3	The Three -Y’s
In addition to abstraction and discipline, designers use the three “-y’s” to manage complexity: hierarchy, modularity, and regularity. These princi- ples apply to both software and hardware systems.
  Hierarchy involves dividing a system into modules, then fur- ther subdividing each of these modules until the pieces are easy to understand.
 Modularity states that modules have well-defined functions and interfaces so that they connect easily without unanticipated side effects.
 Regularity seeks uniformity among modules. Common modules are reused many times, reducing the number of distinct modules that must be designed.

To illustrate these “-y’s,” we return to the example of automobile manufacturing. A car was one of the most intricate objects in common use in the early 20th century. Using the principle of hierarchy, we can break the Model T Ford into components, such as the chassis, engine, and seats. The engine, in turn, contained four cylinders, a carburetor, a magneto, and a cooling system. The carburetor contained fuel and air intakes, a choke and throttle, a needle valve, and so forth, as shown in Figure 1.2. The fuel intake was made from a threaded elbow and a cou- pling nut. Thus, the complex system is recursively broken down into simple interchangeable components that can be mass produced.
Modularity teaches that each component should have a well-defined function and interface. For example, the coupling nut has a function of holding the fuel feed line to the intake elbow in a way that does not
 
1.3	The Digital Abstraction	5
 


 


leak yet can be easily removed when the feed line needs replacement. It is of a standardized diameter and thread pitch, tightened to a stan- dardized torque by a standardized wrench. A car maker can buy the nut from many different suppliers, as long as the correct size is specified. Modularity dictates that there should be no side effects: the coupling nut should not deform the elbow and should preferably be located where it can be tightened or removed without taking off other equipment in the engine.
Regularity teaches that interchangeable parts are a good idea. With regularity, a leaking carburetor can be replaced by an identical part. The carburetors can be efficiently built on an assembly line instead of being painstakingly handcrafted.
We will return to these principles of hierarchy, modularity, and regu- larity throughout the book.

1.3	THE DIGITAL ABSTRACTION
Most physical variables are continuous. For example, the voltage on a wire, the frequency of an oscillation, or the position of a mass are all continuous quantities. Digital systems, on the other hand, represent information with discrete-valued variables—that is, variables with a finite number of distinct values.
An early digital system using variables with ten discrete values was Charles Babbage’s Analytical Engine. Babbage labored from 1834 to 1871, designing and attempting to build this mechanical computer. The Analytical Engine used gears with ten positions labeled 0 through 9, much like a mechanical odometer in a car. Figure 1.3 shows a prototype of the Analytical Engine, in which each row processes one digit. Babbage chose 25 rows of gears, so the machine has 25-digit precision.
Unlike Babbage’s machine, most electronic computers use a binary (two-valued) representation in which a high voltage indicates a “1” and
 





Figure 1.2 Cutaway view of Model T fuel system, showing fuel supply on left and carburetor on right. (https://en.wikipedia.org/ wiki/Ford_Model_T_engine#/ media/File:Pagé_1917_Model_T_ Ford_Car_Figure_14.png)













 
6	CHAPTER ONE
 
From Zero to One
 






 

Figure 1.3 Babbage’s Analytical Engine, under construction at the time of his death in 1871 (image courtesy of Science Museum/ Science and Society Picture Library)
 











a low voltage indicates a “0,” because it is easier to distinguish between two voltages than ten.
The amount of information D in a discrete valued variable with N
distinct states is measured in units of bits as
 
D = log2 N bits
 
(1.1)
 
A binary variable conveys log22 = 1 bit of information. Indeed, the word bit is short for binary digit. Each of Babbage’s gears carried log210 =
3.322 bits of information because it could be in one of 23.322 = 10 unique positions. A continuous signal theoretically contains an infinite amount of information because it can take on an infinite number of values. In practice, noise and measurement error limit the information to only 10 to 16 bits for most continuous signals. If the measurement must be made rapidly, the information content is lower (e.g., 8 bits).
This book focuses on digital circuits using binary variables: 1’s and 0’s. George Boole developed a system of logic operating on binary vari- ables that is now known as Boolean logic. Each of Boole’s variables could be TRUE or FALSE. Electronic computers commonly use a pos- itive voltage to represent “1” and zero volts to represent “0.” In this book, we will use the terms “1,” “TRUE,” and “HIGH” synonymously. Similarly, we will use “0”, “FALSE,” and “LOW” interchangeably.
The beauty of the digital abstraction is that digital designers can focus on 1’s and 0’s, ignoring whether the Boolean variables are physically represented with specific voltages, rotating gears, or even hydraulic fluid levels. A computer programmer can work without needing to know the intimate details of the computer hardware. On the other hand, under- standing the details of the hardware allows the programmer to optimize the software better for that specific computer.
 
1.4 Number Systems	7


An individual bit doesn’t carry much information. In the next sec- tion, we examine how groups of bits can be used to represent numbers. In later chapters, we will also use groups of bits to represent letters and programs.

1.4	NUMBER SYSTEMS
You are accustomed to working with decimal numbers. In digital sys- tems consisting of 1’s and 0’s, binary or hexadecimal numbers are often more convenient. This section introduces the various number systems that will be used throughout the rest of the book.

1.4.1	Decimal Numbers
In elementary school, you learned to count and do arithmetic in decimal. Just as you (probably) have ten fingers, there are ten decimal digits: 0, 1, 2, …, 9. Decimal digits are joined together to form longer decimal numbers. Each column of a decimal number has ten times the weight of the previous column. From right to left, the column weights are 1, 10, 100, 1000, and so on. Decimal numbers are referred to as base 10. The base is indicated by a subscript after the number to pre- vent confusion when working in more than one base. For example, Figure 1.4 shows how the decimal number 974210 is written as the sum of each of its digits multiplied by the weight of the correspond- ing column.
An N-digit decimal number represents one of 10N possibilities: 0, 1, 2, 3, …, 10N − 1. This is called the range of the number. For example, a three-digit decimal number represents one of 1000 possibilities in the
range of 0 to 999.

1.4.2	Binary Numbers
Bits represent one of two values, 0 or 1, and are joined together to form binary numbers. Each column of a binary number has twice the weight of the previous column, so binary numbers are base 2. In binary, the col- umn weights (again, from right to left) are 1, 2, 4, 8, 16, 32, 64, 128,



Figure 1.4 Representation of a decimal number
974210 = 9 × 103 + 7 × 102 + 4 × 101 + 2 × 100
 
nine thousands
 
seven hundreds
 
four tens
 
two ones
 
8	CHAPTER ONE
 
From Zero to One
 


256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 65536, and so on. If
you work with binary numbers often, you’ll save time if you remember these powers of two up to 216.
An N-bit binary number represents one of 2N possibilities: 0, 1, 2, 3, …, 2N − 1. Table 1.1 shows 1-, 2-, 3-, and 4-bit binary numbers and their decimal equivalents.


Example 1.1 BINARY TO DECIMAL CONVERSION
Convert the binary number 101102 to decimal.
Solution Figure 1.5 shows the conversion.



Table 1.1 Binary numbers and their decimal equivalent

1-Bit Binary Numbers	2-Bit Binary Numbers	3-Bit Binary Numbers	4-Bit Binary Numbers	
Decimal Equivalents
0	00	000	0000	0
1	01	001	0001	1
	10	010	0010	2
	11	011	0011	3
		100	0100	4
		101	0101	5
		110	0110	6
		111	0111	7
			1000	8
			1001	9
			1010	10
			1011	11
			1100	12
			1101	13
			1110	14
			1111	15
 
1.4 Number Systems	9
 




101102
 




= 1 × 24 + 0 × 23 + 1 × 22 + 1 × 21+ 0 × 20 = 2210
 





Figure 1.5 Conversion of a binary number to decimal
 
one sixteen
 
no eight
 
one four
 
one two
 
no one
 

 
Example 1.2 DECIMAL TO BINARY CONVERSION
Convert the decimal number 8410 to binary.
Solution Determine whether each column of the binary result has a 1 or a 0. We can do this starting at either the left or the right column.
Working from the left, start with the largest power of 2 less than or equal to the number (in this case, 64). 84 64, so there is a 1 in the 64’s column, leaving 84 − 64 = 20. 20 < 32, so there is a 0 in the 32’s column. 20 16, so there is a 1 in the 16’s column, leaving 20 − 16 = 4. 4 < 8, so there is a 0 in the 8’s column. 4 4, so there is a 1 in the 4’s column, leaving 4 − 4 = 0. Thus, there must be 0 s in the 2’s and 1’s column. Putting this all together, 8410 = 10101002.
Working from the right, repeatedly divide the number by 2. The remainder goes in each column. 84/2 = 42, so 0 goes in the 1’s column. 42/2 = 21, so 0 goes in the 2’s column. 21/2 = 10 with the remainder of 1 going in the 4’s column. 10/2 = 5, so 0 goes in the 8’s column. 5/2 = 2 with the remainder of 1 going in the 16’s column. 2/2 = 1, so 0 goes in the 32’s column. Finally, 1/2 = 0 with the remain- der of 1 going in the 64’s column. Again, 8410 = 10101002.

1.4.3	Hexadecimal Numbers
Writing long binary numbers becomes tedious and prone to error. A group of four bits represents one of 24 = 16 possibilities. Hence, it is sometimes more convenient to work in base 16, called hexadecimal. Hexadecimal numbers use the digits 0 to 9 along with the letters A to F, as shown in Table 1.2. Columns in base 16 have weights of 1, 16, 162 (or 256), 163 (or 4096), and so on.

Example 1.3 HEXADECIMAL TO BINARY AND DECIMAL CONVERSION
Convert the hexadecimal number 2ED16 to binary and to decimal.
Solution Conversion between hexadecimal and binary is easy because each hexa- decimal digit directly corresponds to four binary digits. 216 = 00102, E16 = 11102 and D16 = 11012, so 2ED16 = 0010111011012. Conversion to decimal requires the arithmetic shown in Figure 1.6.
 
10	CHAPTER ONE
 
From Zero to One
 


	Table 1.2 Hexadecimal number system	
Hexadecimal Digit	Decimal Equivalent	Binary Equivalent
0	0	0000
1	1	0001
2	2	0010
3	3	0011
4	4	0100
5	5	0101
6	6	0110
7	7	0111
8	8	1000
9	9	1001
A	10	1010
B	11	1011
C	12	1100
D	13	1101
E	14	1110
F	15	1111




Figure 1.6 Conversion of a
hexadecimal number to decimal	2ED16 = 2 × 162 + E × 161 + D × 160 = 74910
 
two
two hundred
fifty six's
 
fourteen sixteens
 
thirteen ones
 


 
Example 1.4 BINARY TO HEXADECIMAL CONVERSION
Convert the binary number 11110102 to hexadecimal.
Solution Again, conversion is easy. Start reading from the right. The four least signifi- cant bits are 10102 = A16. The next bits are 1112 = 716. Hence, 11110102 = 7A16.
 
1.4 Number Systems	11


Example 1.5 DECIMAL TO HEXADECIMAL AND BINARY CONVERSION
Convert the decimal number 33310 to hexadecimal and binary.
Solution Like decimal to binary conversion, decimal to hexadecimal conversion can be done from the left or the right.
Working from the left, start with the largest power of 16 less than or equal to the number (in this case, 256). 256 goes into 333 once, so there is a 1 in the 256’s column, leaving 333 − 256 = 77. 16 goes into 77 four times, so there is a 4 in the 16’s column, leaving 77 − 16 × 4 = 13. 1310 = D16, so there is a D in the 1’s column. In summary, 33310 = 14D16. Now it is easy to convert from hexadec- imal to binary, as in Example 1.3. 14D16 = 1010011012.
Working from the right, repeatedly divide the number by 16. The remainder goes in each column. 333/16 = 20, with the remainder of 1310 = D16 going in the 1’s column. 20/16 = 1, with the remainder of 4 going in the 16’s column. 1/16 = 0, with the remainder of 1 going in the 256’s column. Again, the result is 14D16.


1.4.4	Bytes, Nibbles, and All That Jazz
A group of eight bits is called a byte. It represents one of 28 = 256 pos- sibilities. The size of objects stored in computer memories is customarily measured in bytes rather than bits.
A group of four bits, or half a byte, is called a nibble. It represents one of 24 = 16 possibilities. One hexadecimal digit stores one nibble and two hexadecimal digits store one full byte. Nibbles are no longer a com- monly used unit, but the term is cute.
Microprocessors handle data in chunks called words. The size of a word depends on the architecture of the microprocessor. When this chapter was written in 2021, most computers had 64-bit proces-
sors, indicating that they operate on 64-bit words. At the time, older computers handling 32-bit words were also widely available. Simpler microprocessors, especially those used in gadgets such as toasters, use 8- or 16-bit words.
Within a group of bits, the bit in the 1’s column is called the least significant bit (lsb), and the bit at the other end is called the most significant bit (msb), as shown in Figure 1.7(a) for a 6-bit binary number. Similarly, within a word, the bytes are identified as least significant byte (LSB) through most significant byte (MSB), as shown in Figure 1.7(b) for a 4-byte number written with eight hexa- decimal digits.
By handy coincidence, 210 = 1024  103. Hence, the term kilo
(Greek for thousand) indicates 210. For example, 210 bytes is one
 
12	CHAPTER ONE
 
From Zero to One
 


101100	DEAFDAD8
 
Figure 1.7 Least and most
 
most
 
least
 
most
 
least
 
significant bits and bytes
 
significant significant
 
significant
 
significant
 
bit
 
bit
 
byte
 
byte
 
(a)	(b)


kilobyte (1 KB). Similarly, mega (million) indicates 220 106, and giga (billion) indicates 230  109. If you know 210  1 thousand, 220  1 mil- lion, 230  1 billion, and remember the powers of two up to 29, it is easy to estimate any power of two in your head.

Example 1.6 ESTIMATING POWERS OF TWO
Find the approximate value of 224 without using a calculator.
Solution Split the exponent into a multiple of ten and the remainder.
224 = 220 × 24. 220  1 million. 24 = 16. So, 224  16 million. Technically, 224 =
16,777,216, but 16 million is close enough for marketing purposes.


1024 bytes is called a kilobyte (KB) or kibibyte (KiB). 1024 bits is called a kilobit (Kb or Kbit) or kibibit (Kib or Kibit). Similarly, MB/MiB, Mb/Mib, GB/GiB, and Gb/Gib are used for millions and billions of bytes and bits. Memory capacity is usually measured in bytes. Communication speed is usually measured in powers of ten bits/second. For example, the maximum speed of a dial-up modem is usually 56 kbits/sec, which is 56,000 bits/sec.

1.4.5	Binary Addition
Binary addition is much like decimal addition but easier, as shown in Figure 1.8. As in decimal addition, if the sum of two numbers is greater than what fits in a single digit, we carry a 1 into the next column. Figure
1.8 compares addition of decimal and binary numbers. In the rightmost column of Figure 1.8(a), 7 + 9 = 16, which cannot fit in a single digit because it is greater than 9. So, we record the 1’s digit, 6, and carry the 10’s digit, 1, over to the next column. Likewise, in binary, if the sum of two numbers is greater than 1, we carry the 2’s digit over to the next column. For example, in the rightmost column of Figure 1.8(b), the sum

11	carries	11
 
1.4 Number Systems	13
1 + 1 = 210 = 102 cannot fit in a single binary digit. So, we record the 1’s digit (0) and carry the 2’s digit (1) of the result to the next column. In the second column, the sum is 1 + 1 + 1 = 310 = 112. Again, we record the 1’s digit (1) and carry the 2’s digit (1) to the next column. For obvi- ous reasons, the bit that is carried over to the neighboring column is called the carry bit.
 

 
Example 1.7 BINARY ADDITION
Compute 01112 + 01012.
Solution Figure 1.9 shows that the sum is 11002. The carries are indicated in blue. We can check our work by repeating the computation in decimal. 01112 = 710. 01012 = 510. The sum is 1210 = 11002.
 


111
0111
 + 0101 
1100
Figure 1.9 Binary addition example
 

 

Digital systems usually operate on a fixed number of digits. Addition is said to overflow if the result is too big to fit in the available digits. A 4-bit number, for example, has the range [0, 15]. 4-bit binary addition overflows if the result exceeds 15. The fifth bit of the sum is discarded, producing an incorrect result in the remaining four bits. Overflow can be detected by checking for a carry out of the most significant column.


 
Example 1.8 ADDITION WITH OVERFLOW
Compute 11012 + 01012. Does overflow occur?
Solution Figure 1.10 shows that the sum is 100102. This result overflows the range of a 4-bit binary number. If it must be stored as four bits, the most signif- icant bit is discarded, leaving the incorrect result of 00102. If the computation had been done using numbers with five or more bits, the result 100102 would have been correct.
 


11 1
1101
 + 0101 
10010
Figure 1.10 Binary addition example with overflow
 

 

1.4.6	Signed Binary Numbers
So far, we have considered only unsigned binary numbers that represent positive quantities. We will often want to represent both positive and negative numbers, requiring a different binary number system. Several schemes exist to represent signed binary numbers. The two most widely employed are called sign/magnitude and two’s complement.

Sign/Magnitude Numbers
Sign/magnitude numbers are intuitively appealing because they match our custom of writing negative numbers with a minus sign followed by the magnitude. An N-bit sign/magnitude number uses the most
 
14	CHAPTER ONE
 
From Zero to One
 


significant bit as the sign and the remaining N − 1 bits as the magnitude (absolute value). A sign bit of 0 indicates positive and a sign bit of 1 indicates negative.

Example 1.9 SIGN/MAGNITUDE NUMBERS
Write 5 and −5 as 4-bit sign/magnitude numbers.
Solution Both numbers have a magnitude of 510 = 1012. Thus, 510 = 01012 and
−510 = 11012.

Unfortunately, ordinary binary addition does not work for sign/ magnitude numbers. For example, using ordinary addition on −510 + 510 gives 11012 + 01012 = 100102, which is nonsense.
An N-bit sign/magnitude number spans the range [−2N−1 + 1, 2N−1 − 1]. Sign/magnitude numbers are slightly odd in that both +0 and −0 exist. Both indicate zero. As you may expect, it can be troublesome to have
two different representations for the same number.

Two’s Complement Numbers
Two’s complement numbers are identical to unsigned binary num- bers except that the most significant bit position has a weight of −2N−1 instead of 2N−1. They overcome the shortcomings of sign/magnitude numbers: zero has a single representation, and ordinary addition works.
In two’s complement representation, zero is written as all zeros: 00…0002. The most positive number has a 0 in the most significant position and 1’s elsewhere: 01…1112 = 2N−1 − 1. The most negative number has a 1 in the most significant position and 0’s elsewhere: 10…0002 = −2N−1. And −1 is written as all ones: 11…1112.
Notice that positive numbers have a 0 in the most significant posi-
tion and negative numbers have a 1 in this position, so the most signif- icant bit can be viewed as the sign bit. However, the overall number is interpreted differently for two’s complement numbers and sign/magni- tude numbers.
The sign of a two’s complement number is reversed (e.g., from +5 to
−5 or from −17 to +17) by inverting the bits in the number and then adding 1 to the least significant bit position. This process is called the reversing the sign method. It is useful in finding the representation of a negative number or determining the magnitude of a negative number.

Example 1.10 TWO’S COMPLEMENT REPRESENTATION OF A NEGATIVE NUMBER
 
Find the representation of −210
 
as a 4-bit two’s complement number.
 
1.4	Number Systems	15
Solution Start by representing the magnitude: +210 = 00102. To get −210, reverse the sign by inverting the bits and adding 1. Inverting 00102 produces 11012. 11012 + 1 = 11102. So, −210 is 11102.

Example 1.11 VALUE OF NEGATIVE TWO’S COMPLEMENT NUMBERS
Find the decimal value of the 4-bit two’s complement number 0x9 (i.e., 10012).
Solution 10012 has a leading 1, so it must be negative. To find its magnitude, reverse the sign by inverting the bits and adding 1. Inverting 10012 = 01102. 01102 + 1 = 01112 = 710. Hence, 10012 = −710.

Two’s complement numbers have the compelling advantage that addition works properly for both positive and negative numbers. Recall that when adding N-bit numbers, the carry out of the Nth bit (i.e., the N + 1th result bit) is discarded.

Example 1.12 ADDING TWO’S COMPLEMENT NUMBERS
Compute (a) −210 + 110 and (b) −710 + 710 using two’s complement numbers.
Solution (a) −210 + 110 = 11102 + 00012 = 11112 = −110. (b) −710 + 710 = 10012 +
01112 = 100002. The fifth bit is discarded, leaving the correct 4-bit result 00002.

Subtraction is performed by taking the two’s complement of the sec- ond number, then adding.

Example 1.13 SUBTRACTING TWO’S COMPLEMENT NUMBERS
Compute (a) 510 − 310 and (b) 310 − 510 using 4-bit two’s complement numbers.
Solution (a) 3	= 0011 . Take its two’s complement to obtain −3	= 1101 .
Now, add 510 + (−310) = 01012 + 11012 = 00102 = 210. Note that the carry out of the most significant position is discarded because the result is stored in four bits. (b) Take the two’s complement of 510 to obtain −510 = 1011. Now, add 310 + (−510) = 00112 + 10112 = 11102 = −210.

The two’s complement of 0 is found by inverting all the bits (producing 11…1112) and adding 1, which produces all 0’s, disregarding the carry out of the most significant bit position. Hence, zero is always represented with all 0’s. Unlike the sign/magnitude system, the two’s complement system has no separate −0. Zero is considered positive
because its sign bit is 0.
 
16	CHAPTER ONE
 
From Zero to One
 


Like unsigned numbers, N-bit two’s complement numbers represent one of 2N possible values. However, the values are split between positive and negative numbers. For example, a 4-bit unsigned number represents 16 values: 0 to 15. A 4-bit two’s complement number also represents 16 values: −8 to 7. In general, the range of an N-bit two’s complement
number spans [−2N−1, 2N−1 − 1]. It should make sense that there is one
more negative number than positive number because there is no −0. The most negative number 10…0002 = −2N−1 is sometimes called the weird number. Its two’s complement is found by inverting the bits (producing 01…1112) and adding 1, which produces 10…0002, the weird number,
again. Hence, this negative number has no positive counterpart.
Adding two N-bit positive numbers or negative numbers may cause overflow if the result is greater than 2N−1 − 1 or less than −2N−1. Adding a positive number to a negative number never causes overflow. Unlike
unsigned numbers, a carry out of the most significant column does not indicate overflow. Instead, overflow occurs if the two numbers being added have the same sign bit and the result has the opposite sign bit.


Example 1.14 ADDING TWO’S COMPLEMENT NUMBERS WITH OVERFLOW
Compute 410 + 510 using 4-bit two’s complement numbers. Does the result overflow?
Solution 410 + 510 = 01002 + 01012 = 10012 = −710. The result overflows the range of 4-bit positive two’s complement numbers, producing an incorrect neg- ative result. If the computation had been done using five or more bits, the result 010012 = 910 would have been correct.


When a two’s complement number is extended to more bits, the sign bit must be copied into the most significant bit positions. This process is called sign extension. For example, the numbers 3 and −3 are written as 4-bit two’s complement numbers 0011 and 1101, respectively. They are sign-extended to seven bits by copying the sign bit into the three new
upper bits to form 0000011 and 1111101, respectively, which are 7-bit representations of 3 and –3.

Comparison of Number Systems
The three most commonly used binary number systems are unsigned, two’s complement, and sign/magnitude. Table 1.3 compares the range of N-bit numbers in each of these three systems. Two’s complement numbers are convenient because they represent both positive and neg- ative integers and because ordinary addition works for all numbers. Subtraction is performed by negating the second number (i.e., reversing
 
1.5	Logic Gates	17
Table 1.3 Range of N-bit numbers
Unsigned	[0, 2N – 1]
Sign/Magnitude	[–2N–1 + 1, 2N–1 – 1]
–8  –7  –6  –5  –4  –3  –2  –1	0	1	2	3	4	5	6	7	8	9	10  11  12  13  14  15
 
Unsigned
 
0000 0001 0010 0011 0100 0101 0110 0111 1000 1001 1010 1011 1100 1101 1110 1111
 
1000 1001 1010 1011 1100 1101 1110 1111 0000 0001 0010 0011 0100 0101 0110 0111	Two's Complement
 

1111 1110 1101 1100 1011 1010 1001 0000 0001 0010 0011 0100 0101 0110 0111
1000

Figure 1.11 Number line and 4-bit binary encodings
 

Sign/Magnitude
 


the sign), and then adding. Unless stated otherwise, assume that all signed binary numbers use two’s complement representation.
Figure 1.11 shows a number line indicating the values of 4-bit num- bers in each system. Unsigned numbers span the range [0, 15] in reg- ular binary order. Two’s complement numbers span the range [−8, 7]. The nonnegative numbers [0, 7] share the same encodings as unsigned
numbers. The negative numbers [−8, −1] are encoded such that a larger unsigned binary value represents a number closer to 0. Notice that the weird number, 1000, represents −8 and has no positive counterpart. Sign/magnitude numbers span the range [−7, 7]. The most significant bit is the sign bit. The positive numbers [1, 7] share the same encodings
as unsigned numbers. The negative numbers are symmetric but have the sign bit set. 0 is represented by both 0000 and 1000. Thus, N-bit sign/ magnitude numbers represent only 2N − 1 integers because of the two representations for 0. N-bit unsigned binary or two's complement num- bers represent 2N integers.

1.5 LOGIC GATES
Now that we know how to use binary variables to represent information, we explore digital systems that perform operations on these binary vari- ables. Logic gates are simple digital circuits that take one or more binary inputs and produce a binary output. Logic gates are drawn with a symbol showing the input (or inputs) and the output. Inputs are usually drawn
 
18	CHAPTER ONE
 
From Zero to One
 


 






NOT
A   Y

Y = A

Figure 1.12 NOT gate

BUF
A	Y

Y = A

Figure 1.13 Buffer

AND
B   Y
Y = AB
 
Figure 1.14 AND gate
 
on the left (or top) and outputs on the right (or bottom). Digital design- ers typically use letters near the beginning of the alphabet for gate inputs and the letter Y for the gate output. The relationship between the inputs and the output can be described with a truth table or a Boolean equation. A truth table lists inputs on the left and the corresponding output on the right. It has one row for each possible combination of inputs. A Boolean equation is a mathematical expression using binary variables.

1.5.1	NOT Gate
A NOT gate has one input, A, and one output, Y, as shown in Figure 1.12. The NOT gate’s output is the inverse of its input. If A is FALSE, then Y is TRUE. If A is TRUE, then Y is FALSE. This relationship is summarized by the truth table and Boolean equation in the figure. The line over A in
the Boolean equation is pronounced NOT, so Y = A is read “Y equals
NOT A.” The NOT gate is also called an inverter.
Y = ¬A, Y = !A, or Y = ~A. We will use Y = A exclusively, but don’t be Other texts use a variety of notations for NOT, including Y = A , puzzled if you encounter another notation elsewhere.

1.5.2	Buffer
The other one-input logic gate is called a buffer and is shown in Figure 1.13. It simply copies the input to the output.
From the logical point of view, a buffer is no different from a wire, so it might seem useless. However, from the analog point of view, the buffer might have desirable characteristics, such as the ability to deliver large amounts of current to a motor or the ability to quickly send its output to many gates. This is an example of why we need to consider multiple levels of abstraction to fully understand a system; the digital abstraction hides the real purpose of a buffer.
The triangle symbol indicates a buffer. A circle on the output is called a bubble and indicates inversion, as was seen in the NOT gate symbol of Figure 1.12.

1.5.3	AND Gate
Two-input logic gates are more interesting. The AND gate shown in Figure 1.14 produces a TRUE output, Y, if and only if both A and B are TRUE. Otherwise, the output is FALSE. By convention, the inputs are listed in the order 00, 01, 10, 11, as if you were counting in binary. The Boolean equation for an AND gate can be written in several ways: Y = A • B, Y = AB, or Y = A ( B. The ( symbol is pronounced “intersec-
tion” and is preferred by logicians. We prefer Y = AB, read “Y equals
A and B,” because we are lazy.
 
1.5	Logic Gates	19

1.5.4	OR Gate	OR
The OR gate shown in Figure 1.15 produces a TRUE output, Y, if either	A
A or B (or both) are TRUE. The Boolean equation for an OR gate is	B
 
written as Y = A + B or Y = A ) B. The ) symbol is pronounced union and is preferred by logicians. Digital designers normally use the + nota- tion, Y = A + B is pronounced “Y equals A or B.”

1.5.5	Other Two-Input Gates
Figure 1.16 shows other common two-input logic gates. XOR (exclusive OR, pronounced “ex-OR”) is TRUE if A or B, but not both, are TRUE. The XOR operation is indicated by , a plus sign with a circle around it. Any gate can be followed by a bubble to invert its operation. The NAND gate performs NOT AND. Its output is TRUE unless both inputs are TRUE. The NOR gate performs NOT OR. Its output is TRUE if nei- ther A nor B is TRUE. An N-input XOR gate is sometimes called a par- ity gate and produces a TRUE output if an odd number of inputs are TRUE. As with two-input gates, the input combinations in the truth table are listed in counting order.
 
Y = A + B
 
Figure 1.15 OR gate
 

 
XOR
B	Y
 
NAND
B	Y
 
NOR
B	Y
 
Y = A + B
 

 
Y = AB
 

 
Y = A + B
 

A	B	Y		A	B	Y		A	B	Y
0	0	0		0	0	1		0	0	1
0	1
1	0
1	1	1
1
0	0	1
1	0
1	1	1
1
0	0	1
1	0
1	1	0
0
0

Figure 1.16 More two-input logic gates



 
Example 1.15 XNOR GATE
Figure 1.17 shows the symbol and Boolean equation for a two-input XNOR (pro- nounced ex-NOR) gate that performs the inverse of an XOR. Complete the truth table.
Solution Figure 1.18 shows the truth table. The XNOR output is TRUE if both inputs are FALSE or both inputs are TRUE. The two-input XNOR gate is some- times called an equality gate because its output is TRUE when the inputs are equal.
 


XNOR
B	Y

 

 

1.5.6	Multiple-Input Gates
Many Boolean functions of three or more inputs exist. The most com-
mon are AND, OR, XOR, NAND, NOR, and XNOR. An N-input AND	Figure 1.17 XNOR gate
 
20	CHAPTER ONE
 
From Zero to One
 


gate produces a TRUE output when all N inputs are TRUE. An N-input OR gate produces a TRUE output when at least one input is TRUE.


 

Figure 1.18 XNOR truth table

NOR3
 
Example 1.16 THREE-INPUT NOR GATE
Figure 1.19 shows the symbol and Boolean equation for a three-input NOR gate. Complete the truth table.
Solution Figure 1.20 shows the truth table. The output is TRUE only if none of
 
A
B	Y	the inputs are TRUE.
 
 

 
Y = A + B + C
A	B	C	Y
 

 
Example 1.17 FOUR-INPUT AND GATE
Figure 1.21 shows the symbol and Boolean equation for a four-input AND gate. Create a truth table.
Solution Figure 1.22 shows the truth table. The output is TRUE only if all of the
 


 
Figure 1.19 Three-input NOR gate


A	B	C	Y
0	0	0	1
0	0	1	0
0	1	0	0
0	1	1	0
1	0	0	0
1	0	1	0
1	1	0	0
1	1	1	0
Figure 1.20 Three-input NOR truth table


AND4
A B C D
Y = ABCD

Figure 1.21 Four-input AND gate
 
1.6	BENEATH THE DIGITAL ABSTRACTION
A digital system uses discrete-valued variables. However, the variables are represented by continuous physical quantities, such as the voltage on a wire, the position of a gear, or the level of fluid in a cylinder. Hence, the designer must choose a way to relate the continuous value to the discrete value.
For example, consider representing a binary signal A with a voltage on a wire. Let 0 volts (V) indicate A = 0 and 5V indicate A = 1. Any real system must tolerate some noise, so 4.97V probably ought to be inter- preted as A = 1 as well. But what about 4.3 V? Or 2.8 V? Or 2.500000 V?

1.6.1	Supply Voltage
Suppose the lowest voltage in the system is 0 V, also called ground or GND. The highest voltage in the system comes from the power supply and is usually called VDD. In 1970’s and 1980’s technology, VDD was generally 5V. As chips have progressed to smaller transistors, VDD has dropped to 3.3V, 2.5V, 1.8V, 1.5V, 1.2V, or even lower to save power and avoid overloading the transistors.

1.6.2	Logic Levels
The mapping of a continuous variable onto a discrete binary variable is done by defining logic levels, as shown in Figure 1.23. The first gate is called the driver and the second gate is called the receiver. The output of
 
1.6 Beneath the Digital Abstraction	21
the driver is connected to the input of the receiver. The driver produces a LOW (0) output in the range of 0 to VOL or a HIGH (1) output in the range of VOH to VDD. If the receiver gets an input in the range of 0 to
V , it will consider the input to be LOW. If the receiver gets an input
 
IL
in the range of VIH to VDD, it will consider the input to be HIGH. If, for some reason such as noise or faulty components, the receiver’s input should fall in the forbidden zone between VIL and VIH, the behavior of the gate is unpredictable. VOH, VOL, VIH, and VIL are called the output and input high and low logic levels.
1.6.3	Noise Margins
If the output of the driver is to be correctly interpreted at the input of the receiver, we must choose VOL < VIL and VOH > VIH. Thus, even if the output of the driver is contaminated by some noise, the input of the receiver will still detect the correct logic level. The noise margin (NM) is the amount of noise that could be added to a worst-case output such that the signal can still be interpreted as a valid input. As can be seen in Figure 1.23, the low and high noise margins are, respectively,
 











Figure 1.22 Four-input AND truth table
 
NML NMH
 
= VIL − VOL
= VOH − VIH
 
(1.2)

(1.3)
 
Driver	Receiver
 
 

Logic High Output Range
 
Output Characteristics
VDD
 
Input Characteristics
 

Logic High Input Range
 



Logic Low
 
VOH


VOL
 
NMH


NML
 
VIH VIL
Logic Low
 
Output Range
 

GND
Figure 1.23 Logic levels and noise margins
 
Input Range
 

 
Example 1.18 CALCULATING NOISE MARGINS
Consider the inverter circuit of Figure 1.24. VO1 is the output voltage of inverter I1, and VI2 is the input voltage of inverter I2. Both inverters have the following characteristics: VDD = 5 V, VIL = 1.35 V, VIH = 3.15 V, VOL = 0.33 V, and VOH =
3.84 V. What are the inverter low and high noise margins? Can the circuit toler- ate 1 V of noise between VO1 and VI2?
 
22	CHAPTER ONE
 
From Zero to One
 


 

Figure 1.24 Inverter circuit
 
Noise
 


Solution The inverter noise margins are: NML = VIL – VOL = (1.35 V − 0.33 V) =
1.02 V, NMH = VOH − VIH = (3.84 V − 3.15 V) = 0.69 V. The circuit can tolerate 1 V of noise when the output is LOW (NML = 1.02 V) but not when the output
is HIGH (NMH = 0.69 V). For example, suppose the driver, I1, outputs its worst- case HIGH value, VO1 = VOH = 3.84 V. If noise causes the voltage to droop by 1 V before reaching the input of the receiver, VI2 = (3.84 V − 1 V) = 2.84 V. This is less than the acceptable input HIGH value, VIH = 3.15 V, so the receiver may not sense a proper HIGH input.


1.6.4	DC Transfer Characteristics
To understand the limits of the digital abstraction, we must delve into the analog behavior of a gate. The DC transfer characteristics of a gate describe the output voltage as a function of the input voltage when the input is changed slowly enough that the output can keep up. They are called transfer characteristics because they describe the relationship between input and output voltages.
An ideal inverter would have an abrupt switching threshold at VDD/2, as shown in Figure 1.25(a). For V(A) < VDD/2, V(Y) = VDD. For V(A) > VDD/2, V(Y) = 0. In such a case, VIH = VIL = VDD/2. VOH = VDD and VOL = 0.
A real inverter changes more gradually between the extremes, as shown in Figure 1.25(b). When the input voltage V(A) is 0, the output voltage V(Y) = VDD. When V(A) = VDD, V(Y) = 0. However, the tran- sition between these endpoints is smooth and may not be centered at exactly VDD/2. This raises the question of how to define the logic levels.
A reasonable place to choose the logic levels is where the slope of the transfer characteristic dV(Y)/dV(A) is −1. These two points are called the unity gain points. Choosing logic levels at the unity gain points usually maximizes the noise margins. If VIL were reduced, VOH would only increase by a small amount. But if VIL were increased, VOH would drop precipitously.

1.6.5	The Static Discipline
To avoid inputs falling into the forbidden zone, digital logic gates are designed to conform to the static discipline. The static discipline requires that, given logically valid inputs, every circuit element will produce logi- cally valid outputs.
By conforming to the static discipline, digital designers sacrifice the freedom of using arbitrary analog circuit elements in return for
 
1.6	Beneath the Digital Abstraction	23
 
V(Y) VOH VDD
 
A	Y		V(Y) VDD VOH
 
Unity Gain Points Slope = –1
 








(a)
 





VOL 0
 






VDD/ 2 VIL, VIH
 






VDD
 






V(A)
 





VOL
0

(b)	
 






VIL  VIH
 






VDD
 






V(A)
 
Figure 1.25 DC transfer characteristics and logic levels

the simplicity and robustness of digital circuits. They raise the level of abstraction from analog to digital, increasing design productivity by hiding needless detail.
The choice of VDD and logic levels is arbitrary, but all gates that communicate must have compatible logic levels. Therefore, gates are grouped into logic families such that all gates in a logic family obey the static discipline when used with other gates in the family. Logic gates in the same logic family snap together like Legos in that they use consistent power supply voltages and logic levels.
Four major logic families that predominated from the 1970’s through the 1990’s are Transistor-Transistor Logic (TTL), Complementary Metal- Oxide-Semiconductor Logic (CMOS, pronounced sea-moss), Low Voltage TTL Logic (LVTTL), and Low Voltage CMOS Logic (LVCMOS). Their logic levels are compared in Table 1.4. Since then, logic fami- lies have balkanized with a proliferation of even lower power supply voltages. Appendix A.6 revisits popular logic families in more detail.

Table 1.4 Logic levels of 5 V and 3.3 V logic families

Logic Family	VDD	VIL	VIH	VOL	VOH
TTL	5 (4.75−5.25)	0.8	2.0	0.4	2.4
CMOS	5 (4.5−6)	1.35	3.15	0.33	3.84
LVTTL	3.3 (3−3.6)	0.8	2.0	0.4	2.4
LVCMOS	3.3 (3−3.6)	0.9	1.8	0.36	2.7
 
24	CHAPTER ONE
 
From Zero to One
 


Table 1.5 Compatibility of logic families


Driver	
TTL	Receiver
CMOS	LVTTL	
LVCMOS
TTL	OK	NO: VOH < VIH	MAYBEa
MAYBEa

CMOS	OK	OK	MAYBEa
MAYBEa

LVTTL	OK	NO: VOH < VIH	OK	OK
LVCMOS	OK	NO: VOH < VIH	OK	OK
aAs long as a 5 V HIGH level does not damage the receiver input

Example 1.19 LOGIC FAMILY COMPATIBILITY
Which of the logic families in Table 1.4 can communicate with each other reliably?
Solution Table 1.5 lists which logic families have compatible logic levels. Note that a 5V logic family such as TTL or CMOS may produce an output voltage as HIGH as 5V. If this 5V signal drives the input of a 3.3V logic family such as LVTTL or LVCMOS, it can damage the receiver unless the receiver is specially designed to be “5-volt compatible.”

1.7	CMOS TRANSISTORS*
This section and other sections marked with a * are optional and are not necessary to understand the main flow of the book.
Babbage’s Analytical Engine was built from gears, and early elec- trical computers used relays or vacuum tubes. Modern computers use transistors because they are cheap, small, and reliable. Transistors are electrically controlled switches that turn ON or OFF when a voltage or
current is applied to a control terminal. The two main types of transis- tors are bipolar junction transistors and metal-oxide-semiconductor field effect transistors (MOSFETs or MOS transistors, pronounced “moss- fets” or “M-O-S”, respectively).
In 1958, Jack Kilby at Texas Instruments built the first integrated circuit containing two transistors. In 1959, Robert Noyce at Fairchild Semiconductor patented a method of interconnecting multiple transis- tors on a single silicon chip. At the time, transistors cost about $10 each. Thanks to more than three decades of unprecedented manufacturing advances, engineers can now pack roughly one billion MOSFETs onto a 1-cm2 chip of silicon, and these transistors cost less than 10 microcents apiece. The capacity and cost continue to improve by an order of mag- nitude every 8 years or so. MOSFETs are now the building blocks of
 
1.7 CMOS Transistors	25


almost all digital systems. In this section, we will peer beneath the digital abstraction to see how logic gates are built from MOSFETs.

1.7.1	Semiconductors
MOS transistors are built from silicon, the predominant atom in rock and sand. Silicon (Si) is a group IV atom, so it has four electrons in its valence shell and forms bonds with four adjacent atoms, resulting in a crystalline lattice. Figure 1.26(a) shows the lattice in two dimensions for ease of drawing, but remember that the lattice actually forms a cubic crystal. In the figure, a line represents a covalent bond. By itself, sili- con is a poor conductor because all the electrons are tied up in covalent bonds. However, it becomes a better conductor when small amounts of impurities, called dopant atoms, are carefully added. If a group V dop- ant such as arsenic (As) is added, the dopant atoms have an extra elec- tron that is not involved in the bonds. That electron can easily move about the lattice, leaving an ionized dopant atom (As+) behind, as shown in Figure 1.26(b). The electron carries a negative charge, so we call arse- nic an n-type dopant. On the other hand, if a group III dopant such as boron (B) is added, the dopant atoms are missing an electron, as shown in Figure 1.26(c). This missing electron is called a hole. An electron from a neighboring silicon atom may move over to fill the missing bond,
forming an ionized dopant atom (B−) and leaving a hole at the neighbor- ing silicon atom. In a similar fashion, the hole can migrate around the lattice. The hole is a lack of negative charge, so it acts like a positively
charged particle. Hence, we call boron a p-type dopant. Because the con- ductivity of silicon changes over many orders of magnitude depending on the concentration of dopants, silicon is called a semiconductor.

1.7.2	Diodes
The junction between p-type and n-type silicon is called a diode. The p-type region is called the anode and the n-type region is called the cath- ode, as illustrated in Figure 1.27. When the voltage on the anode rises

Free electron	Free hole
 	 	 	 	 	 	 	 	 
 
Si	Si	Si

 	 	 
Si	Si	Si
 
Si	Si-	Si
Si	+	Si
 
Si	Si	Si
+
Si	B-	Si
 

 
Figure 1.26 Silicon lattice and dopant atoms
 

Si	Si	Si
 

Si	Si	Si
 

Si	Si	Si
 

 	 	 	 	 	 	 	 	 
 
(a)
 
(b)
 
(c)	
 
26	CHAPTER ONE
 
From Zero to One
 


 

 
anode	cathode


Figure 1.27 The p-n junction diode structure and symbol

C

Figure 1.28 Capacitor symbol
 
above the voltage on the cathode, the diode is forward biased, and cur- rent flows through the diode from the anode to the cathode. But when the anode voltage is lower than the voltage on the cathode, the diode is reverse biased, and no current flows. The diode symbol intuitively shows that current only flows in one direction.

1.7.3	Capacitors
A capacitor consists of two conductors separated by an insulator. When a voltage V is applied to one of the conductors, the conductor accumu- lates electric charge Q and the other conductor accumulates the opposite charge −Q. The capacitance C of the capacitor is the ratio of charge to voltage: C = Q/V. The capacitance is proportional to the size of the con- ductors and inversely proportional to the distance between them. The symbol for a capacitor is shown in Figure 1.28.
Capacitance is important because charging or discharging a conduc- tor takes time and energy. More capacitance means that a circuit will be slower and require more energy to operate. Speed and energy will be discussed throughout this book.

1.7.4	nMOS and pMOS Transistors
A MOSFET is a sandwich of several layers of conducting and insulating materials. MOSFETs are built on thin, flat wafers of silicon of about 15 to 30 cm in diameter. The manufacturing process begins with a bare wafer. The process involves a sequence of steps in which dopants are implanted into the silicon, thin films of silicon dioxide and silicon are grown, and metal is deposited. Between each step, the wafer is patterned so that the materials appear only where they are desired. Because tran- sistors are a fraction of a micron1 in length and the entire wafer is pro- cessed at once, it is inexpensive to manufacture billions of transistors at a time. Once processing is complete, the wafer is cut into rectangles called chips or dice that contain thousands, millions, or even billions of transistors. The chip is tested, then placed in a plastic or ceramic pack- age with metal pins to connect it to a circuit board.
The MOSFET sandwich consists of a conducting layer called the
gate on top of an insulating layer of silicon dioxide (SiO2) on top of the silicon wafer, called the substrate. Historically, the gate was constructed from metal, hence the name metal-oxide-semiconductor. Modern manufacturing processes use polycrystalline silicon for the gate because it does not melt during subsequent high-temperature processing steps. Silicon dioxide is better known as glass and is often simply called oxide
 

 
1 1 +m = 1 micron = 10−6 m.
 
1.7 CMOS Transistors	27
 
source
 
gate
 
drain
 
Polysilicon SiO2
 
source
 
gate
 
drain
 

 

 

gate

source	drain
 

 	 
   

gate

source	drain
 

(a)	nMOS	(b) pMOS
Figure 1.29 nMOS and pMOS transistors

in the semiconductor industry. The metal-oxide-semiconductor sandwich forms a capacitor, in which a thin layer of insulating oxide called a dielectric separates the metal and semiconductor plates.
There are two flavors of MOSFETs: nMOS and pMOS (pronounced “n-moss” and “p-moss”). Figure 1.29 shows cross-sections of each type, made by sawing through a wafer and looking at it from the side. The n-type transistors, called nMOS, have regions of n-type dopants adja- cent to the gate called the source and the drain and are built on a p-type semiconductor substrate. The pMOS transistors are just the opposite, consisting of p-type source and drain regions in an n-type substrate.
A MOSFET behaves as a voltage-controlled switch in which the gate voltage creates an electric field that turns ON or OFF a connection between the source and drain. The term field effect transistor comes from this principle of operation. Let us start by exploring the operation of an nMOS transistor.
The substrate of an nMOS transistor is normally tied to GND, the lowest voltage in the system. First, consider the situation when the gate is also at 0V, as shown in Figure 1.30(a). The diodes between the source or drain and the substrate are reverse biased because the source or drain voltage is nonnegative. Hence, there is no path for current to flow between the source and drain, so the transistor is OFF. Now, consider when the gate is raised to VDD, as shown in Figure 1.30(b). When a posi- tive voltage is applied to the top plate of a capacitor, it establishes an elec- tric field that attracts positive charge on the top plate and negative charge to the bottom plate. If the voltage is sufficiently large, so much negative charge is attracted to the underside of the gate that the region inverts from p-type to effectively become n-type. This inverted region is called the channel. Now the transistor has a continuous path from the n-type source through the n-type channel to the n-type drain, so electrons can flow from
 
28	CHAPTER ONE
 
From Zero to One
 


 
source
 
gate
 
drain
 

 
(a)	(b)

Figure 1.30 nMOS transistor operation

source to drain. The transistor is ON. The gate voltage required to turn on a transistor is called the threshold voltage, Vt, and is typically 0.3 to 0.7 V.
pMOS transistors work in just the opposite fashion, as might be guessed from the bubble on their symbol shown in Figure 1.31. The sub- strate is tied to VDD. When the gate is also at VDD, the pMOS transistor is OFF. When the gate is at GND, the channel inverts to p-type and the pMOS transistor is ON.
Unfortunately, MOSFETs are not perfect switches. In particular, nMOS transistors pass 0’s well but pass 1’s poorly. Specifically, when the gate of an nMOS transistor is at VDD, the source will only swing
between 0 and VDD − Vt when its drain ranges from 0 to VDD. Similarly, pMOS transistors pass 1’s well but 0’s poorly. However, we will see that it
is possible to build logic gates that use transistors only in their good mode. nMOS transistors need a p-type substrate, and pMOS transistors need an n-type substrate. To build both flavors of transistors on the same chip, manufacturing processes typically start with a p-type wafer, then implant n-type regions called wells where the pMOS transistors should go. These processes that provide both flavors of transistors are called Complementary MOS or CMOS. CMOS processes are used to
build the vast majority of all transistors fabricated today.
In summary, CMOS processes give us two types of electri- cally controlled switches, as shown in Figure 1.31. The voltage at the
 


d
nMOS	g
s

s
pMOS	g
d
 
g = 0
d
OFF
s s
ON
d
 
g = 1
d
ON
s

s
  OFF
d
 
Figure 1.31 Switch models of MOSFETs
 
1.7 CMOS Transistors


gate (g) regulates the flow of current between the source (s) and drain (d). nMOS transistors are OFF when the gate is 0 and ON when the gate is 1. pMOS transistors are just the opposite: ON when the gate is 0 and OFF when the gate is 1.

1.7.5	CMOS NOT Gate
Figure 1.32 shows a schematic of a NOT gate built with CMOS transis- tors. The triangle indicates GND, and the flat bar indicates VDD; these labels will be omitted from future schematics. The nMOS transistor, N1, is connected between GND and the Y output. The pMOS transistor, P1, is connected between VDD and the Y output. Both transistor gates are controlled by the input, A.
If A = 0, N1 is OFF and P1 is ON. Hence, Y is connected to VDD but not to GND, and is pulled up to a logic 1. P1 passes a good 1. If A = 1, N1 is ON and P1 is OFF, and Y is pulled down to a logic 0. N1 passes a good 0. Checking against the truth table in Figure 1.12, we see that the circuit is indeed a NOT gate.

1.7.6	Other CMOS Logic Gates
Figure 1.33 shows a schematic of a two-input NAND gate. In sche- matic diagrams, wires are always joined at three-way junctions. They are joined at four-way junctions only if a dot is shown. The nMOS transis- tors N1 and N2 are connected in series; both nMOS transistors must be ON to pull the output down to GND. The pMOS transistors P1 and P2 are in parallel; only one pMOS transistor must be ON to pull the output up to VDD. Table 1.6 lists the operation of the pull-down and pull-up networks and the state of the output, demonstrating that the gate does function as a NAND. For example, when A = 1 and B = 0, N1 is ON, but N2 is OFF, blocking the path from Y to GND. P1 is OFF, but P2 is ON, creating a path from VDD to Y. Therefore, Y is pulled up to 1.
Figure 1.34 shows the general form used to construct any inverting logic gate, such as NOT, NAND, or NOR. nMOS transistors are good at passing 0’s, so a pull-down network of nMOS transistors is placed
 
29









VDD

 
GND
Figure 1.32 NOT gate schematic



Y




Figure 1.33 Two-input NAND gate schematic





output





Figure 1.34 General form of an inverting logic gate
 

Table 1.6 NAND gate operation

A	B	Pull-Down Network	Pull-Up Network	Y
0	0	OFF	ON	1
0	1	OFF	ON	1
1	0	OFF	ON	1
1	1	ON	OFF	0
 
30	CHAPTER ONE
 
From Zero to One
 


between the output and GND to pull the output down to 0. pMOS tran- sistors are good at passing 1’s, so a pull-up network of pMOS transistors is placed between the output and VDD to pull the output up to 1. The networks may consist of transistors in series or in parallel. When transis- tors are in parallel, the network is ON if either transistor is ON. When transistors are in series, the network is ON only if both transistors are ON. The slash across the input wire indicates that the gate may receive multiple inputs.
If both the pull-up and pull-down networks were ON simul- taneously, a short circuit would exist between VDD and GND. The output of the gate might be in the forbidden zone and the transis- tors would consume large amounts of power, possibly enough to burn out. On the other hand, if both the pull-up and pull-down net- works were OFF simultaneously, the output would be connected to neither VDD nor GND. We say that the output floats. Its value is again undefined. Floating outputs are usually undesirable, but in Section 2.6 we will see how they can occasionally be used to the designer’s advantage.
In a properly functioning logic gate, one of the networks should be ON and the other OFF at any given time, so that the output is pulled HIGH or LOW but not shorted or floating. We can guarantee this by using the rule of conduction complements. When nMOS transistors are in series, the pMOS transistors must be in parallel. When nMOS transis- tors are in parallel, the pMOS transistors must be in series.


Y	Example 1.20 THREE-INPUT NAND SCHEMATIC
A
B	Draw a schematic for a three-input NAND gate using CMOS transistors.
C	Solution The NAND gate should produce a 0 output only when all three inputs are 1. Hence, the pull-down network should have three nMOS transistors in
 
Figure 1.35 Three-input NAND gate schematic
 
series. By the conduction complements rule, the pMOS transistors must be in parallel. Such a gate is shown in Figure 1.35; you can verify the function by checking that it has the correct truth table.
 

 

A	Example 1.21 TWO-INPUT NOR SCHEMATIC
B
Y	Draw a schematic for a two-input NOR gate using CMOS transistors.
Solution The NOR gate should produce a 0 output if either input is 1. Hence, the
 

Figure 1.36 Two-input NOR gate schematic
 
pull-down network should have two nMOS transistors in parallel. By the con- duction complements rule, the pMOS transistors must be in series. Such a gate is shown in Figure 1.36.
 

 
 
1.7	CMOS Transistors	31
Example 1.22 TWO-INPUT AND SCHEMATIC
Draw a schematic for a two-input AND gate.	A
 
Solution It is impossible to build an AND gate with a single CMOS gate. However, building NAND and NOT gates is easy. Thus, the best way to build an AND gate using CMOS transistors is to use a NAND followed by a NOT, as shown in Figure 1.37.

 

1.7.7	Transmission Gates
At times, designers find it convenient to use an ideal switch that can pass both 0 and 1 well. Recall that nMOS transistors are good at passing 0 and pMOS transistors are good at passing 1, so the parallel combina- tion of the two passes both values well. Figure 1.38 shows such a circuit, called a transmission gate or pass gate. The two sides of the switch are called A and B because a switch is bidirectional and has no preferred input or output side. The control signals are called enables, EN and EN. When EN = 0 and EN = 1, both transistors are OFF. Hence, the trans- mission gate is OFF or disabled, so A and B are not connected. When EN = 1 and EN = 0, the transmission gate is ON or enabled, and any logic value can flow between A and B.

1.7.8	Pseudo-nMOS Logic
An N-input CMOS NOR gate uses N nMOS transistors in parallel and N pMOS transistors in series. Transistors in series are slower than tran- sistors in parallel, just as resistors in series have more resistance than resistors in parallel. Moreover, pMOS transistors are slower than nMOS transistors because holes cannot move around the silicon lattice as fast as electrons. Therefore, the parallel nMOS transistors are fast and the series pMOS transistors are slow, especially when many are in series.
Pseudo-nMOS logic replaces the slow stack of pMOS transistors with a single weak pMOS transistor that is always ON, as shown in Figure 1.39. This pMOS transistor is often called a weak pull-up. The physical dimensions of the pMOS transistor are selected so that the pMOS transistor will pull the output Y HIGH weakly—that is, only if none of the nMOS transistors are ON. But if any nMOS transistor is ON, it overpowers the weak pull-up and pulls Y down close enough to GND to produce a logic 0.
The advantage of pseudo-nMOS logic is that it can be used to build fast NOR gates with many inputs. For example, Figure 1.40 shows a pseudo-nMOS four-input NOR. Pseudo-nMOS gates are useful for certain memory and logic arrays discussed in Chapter 5. The disadvantage is that
 

Figure 1.37 Two-input AND gate schematic







EN

A	B

EN

Figure 1.38 Transmission gate










Y





Figure 1.39 Generic pseudo-nMOS gate





Y
A


Figure 1.40 Pseudo-nMOS four- input NOR gate
 
32	CHAPTER ONE
 
From Zero to One
 


a short circuit exists between VDD and GND when the output is LOW; the weak pMOS and nMOS transistors are both ON. The short circuit draws continuous power, so pseudo-nMOS logic must be used sparingly.
Pseudo-nMOS gates got their name from the 1970’s, when manufac- turing processes only had nMOS transistors. A weak nMOS transistor was used to pull the output HIGH because pMOS transistors were not available.

1.8	POWER CONSUMPTION*
Power consumption is the amount of energy used per unit time. Power consumption is of great importance in digital systems. The battery life of portable systems such as cell phones and laptop computers is limited by power consumption. For example, a cell phone battery holds about 10 watt-hours (W-hr) of energy, meaning that it could deliver 1 watt (W) for 10 hours or 2W for 5 hours, and so forth. For your phone battery to last a full day, its average consumption should be under 1W. Laptops typ- ically have 50 to 100W-hr batteries and consume under 10W in normal operation, of which the screen is a large fraction. Power is also significant for systems that are plugged in because electricity costs money and emis- sions and because the system will overheat if it draws too much power. A desktop computer consuming 200W for 8 hours each day would use approximately 600 kilowatt-hours (kW-hr) of electricity per year. At an average cost of 12 cents and one pound of CO2 emission per kW-hr, this is $72 of electricity each year as well as 600 pounds of CO2 emissions.
Digital systems draw both dynamic and static power. Dynamic power is the power used to charge capacitance as signals change between 0 and 1. Static power is the power used even when signals do not change and the system is idle.
Logic gates and the wires that connect them have capacitance. The energy drawn from the power supply to charge a capacitance C to volt-
age VDD is CV	2. If the system operates at frequency f and the fraction
DD
of the cycles on which the capacitor charges and discharges is (called the activity factor), the dynamic power consumption is
 
Pdynamic = αCVDD2 f
 
(1.4)
 
Figure 1.41 illustrates activity factors. Figure 1.41(a) shows a clock signal, which rises and falls once every cycle and, thus, has an activity factor of 1. The clock period from one rising edge to the next is called Tc (the cycle time), and is the reciprocal of the clock frequency f. Figure 1.41(b) shows a data signal that switches once every clock cycle. The paral- lel lines on the timing diagram indicate that the signal might be high or might be low; we aren’t concerned with its value. The crossover indicates that the signal changes once, early in each clock cycle. Hence, the activity
 
1.8	Power Consumption	33
 



(a)

(b)	

(c)	
Time
 




 = 1

 = 0.5

 = 0.25
 






Figure 1.41 Illustration of activity factors
 

factor is 0.5 (rising half the cycles and falling half the cycles). Figure 1.41(c) shows a random data signal that switches in half the cycles and remains constant in the other half of the cycles. Therefore, it has an activity factor of 0.25. Real digital systems often have idle components that are not switching, so an activity factor of 0.1 is more typical.
Electrical systems draw some current even when they are idle. When transistors are OFF, they leak a small amount of current. Some circuits, such as the pseudo-nMOS gate discussed in Section 1.7.8, have a path from VDD to GND through which current flows continuously. The total static current, IDD, is also called the leakage current or the quiescent supply current flowing between VDD and GND. The static power consumption is proportional to this static current:
 
Pstatic = IDDVDD
 
(1.5)
 
Example 1.23 POWER CONSUMPTION
A particular cell phone has an 8W-hr battery and operates at 0.707V. Suppose that, when it is in use, the cell phone operates at 2 GHz. The total capacitance of the circuitry is 10 nF (10−8 Farads), and the activity factor is 0.05. When voice or data are active (10% of its time in use), it also broadcasts 3W of power out of its antenna. When the phone is not in use, the dynamic power drops to almost zero because the signal processing is turned off. But the phone also draws 100 mA of quiescent current whether it is in use or not. Determine the battery life of the phone (a) if it is not being used and (b) if it is being used continuously.
Solution The static power is Pstatic = (0.100 A)(0.707 V) = 71 milliwatts (mW).
(a) If the phone is not being used, this is the only power consumption, so the battery life is (8W-hr)/(0.071 W) = 113 hours (about 5 days). (b) If the phone is being used, the dynamic power is Pdynamic = (0.05)(10−8 F)(0.707 V)2(2 × 109 Hz)
= 0.5 W. The average broadcast power is (3 W)(0.1) = 0.3 W.
Together with the static and broadcast power, the total active power is 0.5 W +
0.071 W + 0.3 W = 0.871W, so the battery life is 8W-hr/0.0871 W = 9.2 hours. This example somewhat oversimplifies the actual operation of a cell phone, but it illustrates the key ideas of power consumption.
 
34	CHAPTER ONE
 
From Zero to One
 


1.9	SUMMARY AND A LOOK AHEAD
There are 10 kinds of people in this world: those who can count in binary and those who can’t.

This chapter has introduced principles for understanding and designing complex systems. Although the real world is analog, digital designers discipline themselves to use a discrete subset of possible sig- nals. In particular, binary variables have just two states: 0 and 1, also called FALSE and TRUE or LOW and HIGH. Logic gates compute a binary output from one or more binary inputs. Some of the common logic gates are:

 	NOT:	Output is TRUE when input is FALSE
 	AND:	Output is TRUE when all inputs are TRUE
 	OR:	Output is TRUE when any inputs are TRUE
 	XOR:	Output is TRUE when an odd number of inputs are TRUE
Logic gates are commonly built from CMOS transistors, which behave as electrically controlled switches. nMOS transistors turn ON when the gate is 1. pMOS transistors turn ON when the gate is 0.
In Chapters 2 through 5, we continue the study of digital logic. Chapter 2 addresses combinational logic, in which the outputs depend only on the current inputs. The logic gates introduced already are exam- ples of combinational logic. You will learn to design circuits involving multiple gates to implement a relationship between inputs and outputs specified by a truth table or Boolean equation. Chapter 3 addresses sequential logic, in which the outputs depend on both current and past inputs. Registers are common sequential elements that remember their previous input. Finite state machines, built from registers and combina- tional logic, are a powerful way to build complicated systems in a sys- tematic fashion. We also study timing of digital systems to analyze how fast a system can operate. Chapter 4 describes hardware description languages (HDLs). HDLs are related to conventional programming lan- guages but are used to simulate and build hardware rather than software. Most digital systems today are designed with HDLs. SystemVerilog and VHDL are the two prevalent languages; they are covered side-by-side in this book. Chapter 5 studies other combinational and sequential building blocks, such as adders, multipliers, and memories.
Chapter 6 shifts to computer architecture. It describes the RISC-V pro- cessor, a recently developed open-source microprocessor beginning to see wide development across industry and academia. The RISC-V architecture is defined by its registers and assembly language instruction set. You will
 
1.9 Summary and a Look Ahead	35
learn to write programs in assembly language for the RISC-V processor so that you can communicate with the processor in its native language.
Chapters 7 and 8 bridge the gap between digital logic and computer architecture. Chapter 7 investigates microarchitecture, the arrangement of digital building blocks, such as adders and registers, needed to con- struct a processor. In that chapter, you learn to build your own RISC-V processor. Indeed, you learn three microarchitectures illustrating dif- ferent trade-offs of performance and cost. Processor performance has increased exponentially, requiring ever more sophisticated memory sys- tems to feed the insatiable demand for data. Chapter 8 delves into mem- ory system architecture. Chapter 9 (available as a web supplement—see Preface) describes how computers communicate with peripheral devices, such as monitors, Bluetooth radios, and motors.
 
36	CHAPTER ONE
 
From Zero to One
 

Exercises
Exercise 1.1 Explain in one paragraph at least three levels of abstraction that are used by
(a)	biologists studying the operation of cells.
(b)	chemists studying the composition of matter.

Exercise 1.2 Explain in one paragraph how the techniques of hierarchy, modularity, and regularity may be used by
(a)	automobile designers.
(b)	businesses to manage their operations.

Exercise 1.3 Ben Bitdiddle is building a house. Explain how he can use the principles of hierarchy, modularity, and regularity to save time and money during construction.
Exercise 1.4 An analog voltage is in the range of 0–5 V. If it can be measured with an accuracy of ±50 mV, at most how many bits of information does it convey?
Exercise 1.5 A classroom has an old clock on the wall whose minute hand broke off.
(a)	If you can read the hour hand to the nearest 15 minutes, how many bits of information does the clock convey about the time?
(b)	If you know whether it is before or after noon, how many additional bits of information do you know about the time?
Exercise 1.6 The Babylonians developed the sexagesimal (base 60) number system about 4000 years ago. How many bits of information is conveyed with one sexagesimal digit? How do you write the number 400010 in sexagesimal?
Exercise 1.7 How many different numbers can be represented with 16 bits?
Exercise 1.8 What is the largest unsigned 32-bit binary number?

Exercise 1.9 What is the largest 16-bit binary number that can be represented with
(a)	unsigned numbers?
(b)	two’s complement numbers?
(c)	sign/magnitude numbers?
 


Exercises	37


Exercise 1.10 What is the largest 32-bit binary number that can be represented with
(a)	unsigned numbers?
(b)	two’s complement numbers?
(c)	sign/magnitude numbers?

Exercise 1.11 What is the smallest (most negative) 16-bit binary number that can be represented with
(a)	unsigned numbers?
(b)	two’s complement numbers?
(c)	sign/magnitude numbers?

Exercise 1.12 What is the smallest (most negative) 32-bit binary number that can be represented with
(a)	unsigned numbers?
(b)	two’s complement numbers?
(c)	sign/magnitude numbers?

Exercise 1.13 Convert the following unsigned binary numbers to decimal. Show your work.
(a) 10102
(b) 1101102
(c)  111100002
(d) 0001000101001112

Exercise 1.14 Convert the following unsigned binary numbers to decimal. Show your work.
(a) 11102
(b) 1001002
(c)  110101112
(d) 0111010101001002

Exercise 1.15 Repeat Exercise 1.13, but convert to hexadecimal.

Exercise 1.16 Repeat Exercise 1.14, but convert to hexadecimal.
 


 

38	CHAPTER ONE
 

From Zero to One
 


Exercise 1.17 Convert the following hexadecimal numbers to decimal. Show your work.
(a)	A516
(b)	3B16
(c)	FFFF16
(d) D000000016

Exercise 1.18 Convert the following hexadecimal numbers to decimal. Show your work.
(a)	4E16
(b)	7C16
(c)	ED3A16
(d) 403FB00116
Exercise 1.19 Repeat Exercise 1.17, but convert to unsigned binary.
Exercise 1.20 Repeat Exercise 1.18, but convert to unsigned binary.
Exercise 1.21 Convert the following two’s complement binary numbers to decimal.
(a) 10102
(b) 1101102
(c)  011100002
(d) 100111112
Exercise 1.22 Convert the following two’s complement binary numbers to decimal.
(a) 11102
(b) 1000112
(c)  010011102
(d) 101101012

Exercise 1.23 Repeat Exercise 1.21, assuming that the binary numbers are in sign/magnitude form rather than two’s complement representation.
Exercise 1.24 Repeat Exercise 1.22, assuming that the binary numbers are in sign/magnitude form rather than two’s complement representation.
 


Exercises	39


Exercise 1.25 Convert the following decimal numbers to unsigned binary numbers.
(a) 4210
(b) 6310
(c)  22910
(d) 84510
Exercise 1.26 Convert the following decimal numbers to unsigned binary numbers.
(a) 1410
(b) 5210
(c)  33910
(d) 71110
Exercise 1.27 Repeat Exercise 1.25, but convert to hexadecimal.
Exercise 1.28 Repeat Exercise 1.26, but convert to hexadecimal.
Exercise 1.29 Convert the following decimal numbers to 8-bit two’s complement numbers or indicate that the decimal number would overflow the range.
(a) 4210
(b) −6310
(c)  12410
(d) −12810
(e) 13310
Exercise 1.30 Convert the following decimal numbers to 8-bit two’s complement numbers or indicate that the decimal number would overflow the range.
(a) 2410
(b) −5910
(c)  12810
(d) −15010
(e) 12710
Exercise 1.31 Repeat Exercise 1.29, but convert to 8-bit sign/magnitude numbers.
 


 

40	CHAPTER ONE
 

From Zero to One
 


Exercise 1.32 Repeat Exercise 1.30, but convert to 8-bit sign/magnitude numbers.
Exercise 1.33 Convert the following 4-bit two’s complement numbers to 8-bit two’s complement numbers.
(a) 01012
(b) 10102
Exercise 1.34 Convert the following 4-bit two’s complement numbers to 8-bit two’s complement numbers.
(a) 01112
(b) 10012
Exercise 1.35 Repeat Exercise 1.33 if the numbers are unsigned rather than two’s complement.
Exercise 1.36 Repeat Exercise 1.34 if the numbers are unsigned rather than two’s complement.
Exercise 1.37 Base 8 is referred to as octal. Convert each of the numbers from Exercise 1.25 to octal.
Exercise 1.38 Base 8 is referred to as octal. Convert each of the numbers from Exercise 1.26 to octal.
Exercise 1.39 Convert each of the following octal numbers to binary, hexadecimal, and decimal.
(a) 428
(b) 638
(c)  2558
(d) 30478
Exercise 1.40 Convert each of the following octal numbers to binary, hexadecimal, and decimal.
(a) 238
(b) 458
(c)  3718
(d) 25608
Exercise 1.41 How many 5-bit two’s complement numbers are greater than 0? How many are less than 0? How would your answers differ for sign/magnitude numbers?
 


Exercises	41


Exercise 1.42 How many 7-bit two’s complement numbers are greater than 0? How many are less than 0? How would your answers differ for sign/magnitude numbers?
Exercise 1.43 How many bytes are in a 32-bit word? How many nibbles are in the 32-bit word?
Exercise 1.44 How many bytes are in a 64-bit word?

Exercise 1.45 A particular DSL modem operates at 768 kbits/sec. How many bytes can it receive in 1 minute?
Exercise 1.46 USB 3.0 can send data at 5 Gbits/sec. How many bytes can it send in 1 minute?
Exercise 1.47 Hard drive manufacturers use the term “megabyte” to mean 106 bytes and “gigabyte” to mean 109 bytes. How many real GBs (i.e., GiBs) of music can you store on a 50 GB hard drive?
Exercise 1.48 Estimate the value of 231 without using a calculator.
Exercise 1.49 A memory on the Pentium II microprocessor is organized as a rectangular array of bits with 28 rows and 29 columns. Estimate how many bits it has without using a calculator.
Exercise 1.50 Draw a number line analogous to Figure 1.11 for 3-bit unsigned, two’s complement, and sign/magnitude numbers.
Exercise 1.51 Draw a number line analogous to Figure 1.11 for 2-bit unsigned, two’s complement, and sign/magnitude numbers.
Exercise 1.52 Perform the following additions of unsigned binary numbers. Indicate whether the sum overflows a 4-bit result.
(a) 10012 + 01002
(b) 11012 + 10112

Exercise 1.53 Perform the following additions of unsigned binary numbers. Indicate whether the sum overflows an 8-bit result.
(a) 100110012 + 010001002
(b) 110100102 + 101101102
Exercise 1.54 Repeat Exercise 1.52, assuming that the binary numbers are in two’s complement form.
Exercise 1.55 Repeat Exercise 1.53, assuming that the binary numbers are in two’s complement form.
 


 

42	CHAPTER ONE
 

From Zero to One
 


Exercise 1.56 Convert the following decimal numbers to 6-bit two’s complement binary numbers and add them. Indicate whether the sum overflows a 6-bit result.
(a) 1610 + 910
(b) 2710 + 3110
(c)  −410 + 1910
(d)  310 + −3210
(e) −1610 + −910
(f)  −2710 + −3110
Exercise 1.57 Repeat Exercise 1.56 for the following numbers. (a) 710 + 1310
(b) 1710 + 2510
(c)  −2610 + 810
(d) 3110 + −1410
(e) −1910 + −2210
(f)  −210 + −2910
Exercise 1.58 Perform the following additions of unsigned hexadecimal numbers. Indicate whether the sum overflows an 8-bit (two hex digit) result.
(a) 716 + 916
(b) 1316 + 2816
(c)  AB16 + 3E16
(d) 8F16 + AD16
Exercise 1.59 Perform the following additions of unsigned hexadecimal numbers. Indicate whether the sum overflows an 8-bit (two hex digit) result.
(a) 2216 + 816 (b) 7316 + 2C16 (c) 7F16 + 7F16 (d) C216 + A416
Exercise 1.60 Convert the following decimal numbers to 5-bit two’s complement binary numbers and subtract them. Indicate whether the difference overflows a 5-bit result.
(a) 910 − 710
(b) 1210 − 1510
 


Exercises	43

(c) −610 − 1110
(d) 410 − −810
Exercise 1.61 Convert the following decimal numbers to 6-bit two’s complement binary numbers and subtract them. Indicate whether the difference overflows a 6-bit result.
(a) 1810 − 1210
(b) 3010 − 910
(c) −2810 − 310
(d) −1610 −2110
Exercise 1.62 In a biased N-bit binary number system with bias B, positive and negative numbers are represented as their value plus the bias B. For example, for 5-bit numbers with a bias of 15, the number 0 is represented as 01111, 1 as 10000, and so forth. Biased number systems are sometimes used in floating-
point mathematics, which will be discussed in Chapter 5. Consider a biased 8-bit binary number system with a bias of 12710.
(a)	What decimal value does the binary number 100000102 represent?
(b)	What binary number represents the value 0?
(c)	What is the representation and value of the most negative number?
(d)	What is the representation and value of the most positive number?

Exercise 1.63 Draw a number line analogous to Figure 1.11 for 3-bit biased numbers with a bias of 3 (see Exercise 1.62 for a definition of biased numbers).
Exercise 1.64 In a binary coded decimal (BCD) system, 4 bits are used to represent a decimal digit from 0 to 9. For example, 3710 is written as 00110111BCD.
(a)	Write 28910 in BCD.
(b)	Convert 100101010001BCD to decimal.
(c)	Convert 01101001BCD to binary.
(d)	Explain why BCD might be a useful way to represent numbers.
Exercise 1.65 Answer the following questions related to BCD systems (see Exercise 1.64 for the definition of BCD).
(a)	Write 37110 in BCD.
(b)	Convert 000110000111BCD to decimal.
(c)	Convert 10010101BCD to binary.
(d)	Explain the disadvantages of BCD when compared with binary representations of numbers.
 


 

44	CHAPTER ONE
 

From Zero to One
 


Exercise 1.66 A flying saucer crashes in a Nebraska cornfield. The FBI investigates the wreckage and finds an engineering manual containing an equation in the Martian number system: 325 + 42 = 411. If this equation is correct, how many fingers would you expect Martians to have?
Exercise 1.67 Ben Bitdiddle and Alyssa P. Hacker are having an argument. Ben says, “All integers greater than zero and exactly divisible by six have exactly two 1’s in their binary representation.” Alyssa disagrees. She says, “No, but all such numbers have an even number of 1’s in their representation.” Do you agree with Ben or Alyssa or both or neither? Explain.
Exercise 1.68 Ben Bitdiddle and Alyssa P. Hacker are having another argument. Ben says, “I can get the two’s complement of a number by subtracting 1, then inverting all the bits of the result.” Alyssa says, “No, I can do it by examining each bit of the number, starting with the least significant bit. When the first 1 is found, invert each subsequent bit.” Do you agree with Ben or Alyssa or both or neither? Explain.
Exercise 1.69 Write a program in your favorite language (e.g., C, Java, Perl) to convert numbers from binary to decimal. The user should type in an unsigned binary number. The program should print the decimal equivalent.
Exercise 1.70 Repeat Exercise 1.69 but convert from an arbitrary base b1 to another base b2, as specified by the user. Support bases up to 16, using the letters of the alphabet for digits greater than 9. The user should enter b1, b2, and then the number to convert in base b1. The program should print the equivalent number in base b2.
Exercise 1.71 Draw the symbol, Boolean equation, and truth table for
(a)	a three-input OR gate
(b)	a three-input exclusive OR (XOR) gate
(c)	a four-input XNOR gate

Exercise 1.72 Draw the symbol, Boolean equation, and truth table for
(a)	a four-input OR gate
(b)	a three-input XNOR gate
(c)	a five-input NAND gate

Exercise 1.73 A majority gate produces a TRUE output if and only if more than half of its inputs are TRUE. Complete a truth table for the three-input majority gate shown in Figure 1.42.
A
B	Y
C
Figure 1.42 Three-input majority gate
 


Exercises	45
Exercise 1.74 A three-input AND-OR (AO) gate shown in Figure 1.43 produces a TRUE output if both A and B are TRUE or if C is TRUE. Complete a truth table for the gate.
A B C
Figure 1.43 Three-input AND-OR gate
Exercise 1.75 A three-input OR-AND-INVERT (OAI) gate shown in Figure 1.44 produces a FALSE output if C is TRUE and A or B is TRUE. Otherwise, it produces a TRUE output. Complete a truth table for the gate.


A
B	Y
C

Figure 1.44 Three-input OR-AND-INVERT gate

Exercise 1.76 There are 16 different truth tables for Boolean functions of two variables. List each truth table. Give each one a short descriptive name (such as OR, NAND, and so on).

Exercise 1.77 How many different truth tables exist for Boolean functions of N
variables?

Exercise 1.78 Is it possible to assign logic levels so that a device with the transfer characteristics shown in Figure 1.45 would serve as an inverter? If so, what are the input and output low and high levels (VIL, VOL, VIH, and VOH) and noise margins (NML and NH)? If not, explain why not.


Vout

 
5

4

3

2

1

0
0	1	2	3	4	5
 







Vin
 
Figure 1.45 DC transfer characteristics
 


 

46	CHAPTER ONE
 

From Zero to One
 


Exercise 1.79 Repeat Exercise 1.78 for the transfer characteristics shown in Figure 1.46.

Vout

 
5

4

3

2

1

0
0	1	2	3	4	5
 







Vin
 
Figure 1.46 DC transfer characteristics


Exercise 1.80 Is it possible to assign logic levels so that a device with the transfer characteristics shown in Figure 1.47 would serve as a buffer? If so, what are
the input and output low and high levels (VIL, VOL, VIH, and VOH) and noise margins (NML and NMH)? If not, explain why not.


Vout

 
5

4

3

2

1

0
0	1	2	3	4	5
 







Vin
 
Figure 1.47 DC transfer characteristics


Exercise 1.81 Ben Bitdiddle has invented a circuit with the transfer characteristics shown in Figure 1.48 that he would like to use as a buffer.
Will it work? Why or why not? He would like to advertise that it is compatible with LVCMOS and LVTTL logic. Can Ben’s buffer correctly receive inputs from those logic families? Can its output properly drive those logic families?
Explain.
 


Exercises	47
 




3.3
3.0

2.4

1.8

1.2

0.6

0
 


Vout









0
 














0.6 1.2 1.8 2.4 3.0 3.3
 











Vin
 







Figure 1.48 Ben’s buffer DC transfer characteristics
 
Exercise 1.82 While walking down a dark alley, Ben Bitdiddle encounters a two- input gate with the transfer function shown in Figure 1.49. The inputs are A and B and the output is Y.


3

2
Y	Figure 1.49 Two-input DC transfer
1	characteristics
0
3
3


(a)	What kind of logic gate did he find?
(b)	What are the approximate high and low logic levels?

Exercise 1.83 Repeat Exercise 1.82 for Figure 1.50.


3

2
Y	Figure 1.50 Two-input DC transfer
1	characteristics

0
3
3
 


 

48	CHAPTER ONE
 

From Zero to One
 


Exercise 1.84 Sketch a transistor-level circuit for the following CMOS gates. Use a minimum number of transistors.
(a)	four-input NAND gate
(b)	three-input OR-AND-INVERT gate (see Exercise 1.75)
(c)	three-input AND-OR gate (see Exercise 1.74)

Exercise 1.85 Sketch a transistor-level circuit for the following CMOS gates. Use a minimum number of transistors.
(a)	three-input NOR gate
(b)	three-input AND gate
(c)	two-input OR gate

Exercise 1.86 A minority gate produces a TRUE output if and only if fewer than half of its inputs are TRUE. Otherwise, it produces a FALSE output. Sketch a transistor-level circuit for a three-input CMOS minority gate. Use a minimum number of transistors.
Exercise 1.87 Write a truth table for the function performed by the gate in Figure 1.51. The truth table should have two inputs, A and B. What is the name of this function?




Y



Figure 1.51 Mystery schematic


Exercise 1.88 Write a truth table for the function performed by the gate in Figure 1.52. The truth table should have three inputs, A, B, and C.


A

Y
A
B

Figure 1.52 Mystery schematic
 


Exercises	49


Exercise 1.89 Implement the following three-input gates using only pseudo- nMOS logic gates. Your gates receive three inputs, A, B, and C. Use a minimum number of transistors.
(a)	three-input NOR gate
(b)	three-input NAND gate
(c)	three-input AND gate

Exercise 1.90 Resistor-Transistor Logic (RTL) uses nMOS transistors to pull the gate output LOW and a weak resistor to pull the output HIGH when none of the paths to ground are active. A NOT gate built using RTL is shown in Figure 1.53. Sketch a three-input RTL NOR gate. Use a minimum number of transistors.


Y


Figure 1.53 RTL NOT gate
 


 

50	CHAPTER ONE
 

From Zero to One
 

Interview Questions
These questions have been asked at interviews for digital design jobs.

Question 1.1 Sketch a transistor-level circuit for a CMOS four-input NOR gate.

Question 1.2 The king receives 64 gold coins in taxes but has reason to believe that one is counterfeit. He summons you to identify the fake coin. You have a balance that can hold coins on each side. How many times do you need to use the balance to find the lighter, fake coin?

Question 1.3 The professor, the teaching assistant, the digital design student, and the freshman track star need to cross a rickety bridge on a dark night. The bridge is so shaky that only two people can cross at a time. They have only one flashlight among them and the span is too long to throw the flashlight, so somebody must carry it back to the other people. The freshman track star can cross the bridge in 1 minute. The digital design student can cross the bridge in
2 minutes. The teaching assistant can cross the bridge in 5 minutes. The professor always gets distracted and takes 10 minutes to cross the bridge. What is the fastest time to get everyone across the bridge?
 
 
 
Combinational Logic Design	2
 





2.1 INTRODUCTION
In digital electronics, a circuit is a network that processes discrete-valued variables. A circuit can be viewed as a black box, shown in Figure 2.1, with
	one or more discrete-valued input terminals
	one or more discrete-valued output terminals
	a functional specification describing the relationship between inputs and outputs
	a timing specification describing the delay between inputs changing and outputs responding.
Peering inside the black box, circuits are composed of nodes and ele- ments. An element is itself a circuit with inputs, outputs, and a specifica- tion. A node is a wire, whose voltage conveys a discrete-valued variable. Nodes are classified as input, output, or internal. Inputs receive values from the external world. Outputs deliver values to the external world.
Wires that are not inputs or outputs are called internal nodes. Figure 2.2


inputs	outputs


Figure 2.1 Circuit as a black box with inputs, outputs, and specifications
 


2.1	Introduction
2.2	Boolean Equations
2.3	Boolean Algebra
2.4	From Logic to Gates
2.5	Multilevel Combinational Logic
2.6	X’s and Z’s, Oh My
2.7	Karnaugh Maps
2.8	Combinational Building Blocks
2.9	Timing
2.10	Summary
Exercises
Interview Questions




 


A
B	Y
C	Z

Figure 2.2 Elements and nodes
Digital Design and Computer Architecture, RISC-V Edition. DOI: 10.1016/B978-0-12-820064-3.00002-7	53
Copyright © 2022 Elsevier Inc. All rights reserved.
 
54	CHAPTER TWO
 
Combinational Logic Design
 


illustrates a circuit with three elements, E1, E2, and E3, and six nodes. Nodes A, B, and C are inputs. Y and Z are outputs. n1 is an internal node between E1 and E3.
Digital circuits are classified as combinational or sequential. A com- binational circuit’s outputs depend only on the current values of the inputs; in other words, it combines the current input values to compute the output. For example, a logic gate is a combinational circuit. A sequen- tial circuit’s outputs depend on both current and previous values of the inputs; in other words, it depends on the input sequence. A combina-
A	tional circuit is memoryless, but a sequential circuit has memory. This
B	chapter focuses on combinational circuits, and Chapter 3 examines
 
Y = F(A, B) = A + B
Figure 2.3 Combinational logic circuit


B   Y
(a)

A	Y
B
(b)
 
sequential circuits.
The functional specification of a combinational circuit expresses the output values in terms of the current input values. The timing specifica- tion of a combinational circuit consists of lower and upper bounds on the delay from input to output. We will initially concentrate on the func- tional specification, then return to the timing specification later in this chapter.
Figure 2.3 shows a combinational circuit with two inputs and one output. On the left of the figure are the inputs, A and B, and on the right is the output, Y. The symbol   inside the box indicates that it is imple- mented using only combinational logic. In this example, the function F is specified to be OR: Y = F(A, B) = A + B. In words, we say that the output
 
Figure 2.4 Two OR implementations


A B
Cin
S = A ⊕ B ⊕ Cin
 





S
Cout
 
Y is a function of the two inputs, A and B—namely, Y = A OR B.
Figure 2.4 shows two possible implementations for the combina- tional logic circuit in Figure 2.3. As we will see repeatedly throughout the book, there are often many implementations for a single function. You choose which to use given the building blocks at your disposal and your design constraints. These constraints often include area, speed, power, and design time.
Figure 2.5 shows a combinational circuit with multiple outputs.
 
Cout = AB + ACin + BCin
Figure 2.5 Multiple-output combinational circuit

(a)

(b)
Figure 2.6 Slash notation for multiple signals
 
This particular combinational circuit is called a full adder, which we will revisit in Section 5.2.1. The two equations specify the function of the outputs, S and Cout, in terms of the inputs, A, B, and Cin.
To simplify drawings, we often use a single line with a slash through it and a number next to it to indicate a bus, a bundle of multiple signals. The number specifies how many signals are in the bus. For example, Figure 2.6(a) represents a block of combinational logic with three inputs and two outputs. If the number of bits is unimportant or obvious from the context, the slash may be shown without a number. Figure 2.6(b) indicates two blocks of combinational logic with an arbitrary number of outputs from one block serving as inputs to the second block.
The rules of combinational composition tell us how we can build a large combinational circuit from smaller combinational circuit elements.
 
2.1	Introduction	55


A circuit is combinational if it consists of interconnected circuit elements such that
	Every circuit element is itself combinational.
	Every node of the circuit is either designated as an input to the circuit or connects to exactly one output terminal of a circuit element.
	The circuit contains no cyclic paths: every path through the circuit visits each circuit node at most once.

Example 2.1 COMBINATIONAL CIRCUITS
Which of the circuits in Figure 2.7 are combinational circuits according to the rules of combinational composition?
Solution Circuit (a) is combinational. It is constructed from two combinational circuit elements (inverters I1 and I2). It has three nodes: n1, n2, and n3. n1 is an input to the circuit and to I1; n2 is an internal node, which is the output of I1 and the input to I2; n3 is the output of the circuit and of I2. (b) is not com- binational, because there is a cyclic path: the output of the XOR feeds back to one of its inputs. Hence, a cyclic path starting at n4 passes through the XOR to n5, which returns to n4. (c) is combinational. (d) is not combinational, because node n6 connects to the output terminals of both I3 and I4. (e) is combinational, illustrating two combinational circuits connected to form a larger combinational circuit. (f) does not obey the rules of combinational composition because it has a cyclic path through the two elements. Depending on the functions of the ele- ments, it may or may not be a combinational circuit.
Large circuits such as microprocessors can be very complicated, so we use the principles from Chapter 1 to manage the complexity. Viewing a circuit as a black box with a well-defined interface and function is an application of abstraction and modularity. Building the circuit out of smaller circuit elements is an application of hierarchy. The rules of com- binational composition are an application of discipline.



 
n1 I1
(a)
 
n2 I2
 
n3	n4
(b)
 



(c)
 



Figure 2.7 Example circuits
 

 	 	 
 
(d)	
 
(e)	
 
(f)	
 
56	CHAPTER TWO
 
Combinational Logic Design
 


The functional specification of a combinational circuit is usually expressed as a truth table or a Boolean equation. In the next sections, we describe how to derive a Boolean equation from any truth table and how to use Boolean algebra and Karnaugh maps to simplify equations. We show how to implement these equations using logic gates and how to analyze the speed of these circuits.

2.2	BOOLEAN EQUATIONS
Boolean equations deal with variables that are either TRUE or FALSE, so they are perfect for describing digital logic. This section defines some terminology commonly used in Boolean equations and then shows how to write a Boolean equation for any logic function, given its truth table.

 

























 




Figure 2.8 Truth table and minterms
 
2.2.1	Terminology

The complement of a variable A is its inverse A. The variable or its com- plement is called a literal. For example, A, A, B, and B are literals. We call A the true form of the variable and A the complementary form; “true form” does not mean that A is TRUE but merely that A does not have a line over it.
The AND of one or more literals is called a product or an implicant. AB, ABC, and B are all implicants for a function of three variables. A minterm is a product involving all of the inputs to the function. ABC is a minterm for a function of the three variables A, B, and C, but AB is not because it does not involve C. Similarly, the OR of one or more literals is called a sum. A maxterm is a sum involving all of the inputs to the function. A + B + C is a maxterm for a function of the three variables A, B, and C.
The order of operations is important when interpreting Boolean equations. Does Y = A + BC mean Y = (A OR B) AND C or Y = A OR (B AND C)? In Boolean equations, NOT has the highest precedence, followed by AND, then OR. Just as in ordinary equations, products are performed before sums. Therefore, the equation is read as Y = A OR (B AND C). Equation 2.1 gives another example of order of operations.
AB + BCD = ((A)B) + (BC(D))	(2.1)
2.2.2	Sum-of-Products Form
A truth table of N inputs contains 2N rows, one for each possible value of the inputs. Each row in a truth table is associated with a minterm that is TRUE for that row. Figure 2.8 shows a truth table of two inputs, A and B. Each row shows its corresponding minterm. For example, the minterm for the first row is AB because AB is TRUE when A = 0, B = 0. The minterms are numbered starting with 0; the top row corresponds to minterm 0, m0, the next row to minterm 1, m1, and so on.
 
2.2	Boolean Equations	57
 


We can write a Boolean equation for any truth table by summing each of the minterms for which the output, Y, is TRUE. For example, in Figure 2.8, there is only one row (or minterm) for which the output Y is TRUE, shown circled in blue. Thus, Y = AB. Figure 2.9 shows a truth table with more than one row in which the output is TRUE. Taking
the sum of each of the circled minterms gives Y = AB + AB.
This is called the sum-of-products (SOP) canonical form of a function
there are many ways to write the same function, such as Y = BA + BA, because it is the sum (OR) of products (ANDs forming minterms). Although we will sort the minterms in the same order that they appear in the truth
table so that we always write the same Boolean expression for the same truth table.
The sum-of-products canonical form can also be written in sigma notation using the summation symbol, . With this notation, the func- tion from Figure 2.9 would be written as:
 



A	
B	
Y	
minterm	minterm name
0	0	0	AB 	m0
0	1	1	A B 	m1	
1	0	0	AB 	m2
1	1	1	AB 	m3	

Figure 2.9 Truth table with multiple TRUE minterms


 

 
F(A, B) = Σ(m1, m3)
or
F(A, B) = Σ(1,3)
 

(2.2)
 
 
Example 2.2 SUM-OF-PRODUCTS (SOP) FORM
Ben Bitdiddle is having a picnic. He won’t enjoy it if it rains or if there are ants. Design a circuit that will output TRUE only if Ben enjoys the picnic.
Solution First, define the inputs and outputs. The inputs are A and R, which indi- cate if there are ants and if it rains. A is TRUE when there are ants and FALSE when there are no ants. Likewise, R is TRUE when it rains and FALSE when the sun smiles on Ben. The output is E, Ben’s enjoyment of the picnic. E is TRUE if Ben enjoys the picnic and FALSE if he suffers. Figure 2.10 shows the truth table for Ben’s picnic experience.
Using sum-of-products form, we write the equation as: E = AR or E = Σ(0). We can build the equation using two inverters and a two-input AND gate, shown in
1.5.5: E = A NOR R = A + R. Figure 2.11(b) shows the NOR implementation. Figure 2.11(a). You may recognize this truth table as the NOR function from Section In Section 2.3, we show that the two equations, AR and A + R, are equivalent.

The sum-of-products form provides a Boolean equation for any truth table with any number of variables. Figure 2.12 shows a random three-input truth table. The sum-of-products form of the logic function is
Y = ABC + ABC + ABC
 
or
Y = Σ(0, 4,5)
 
(2.3)
 
Figure 2.10 Ben’s truth table
 
58	CHAPTER TWO
 
Combinational Logic Design
 


 

A
E
R
(a)

R   E
(b)
Figure 2.11 Ben’s circuit



A	B	C	Y
0	0	0	1
0	0	1	0
0	1	0	0
0	1	1	0
1	0	0	1
1	0	1	1
1	1	0	0
1	1	1	0
Figure 2.12 Random three-input truth table







Figure 2.13 Truth table with multiple FALSE maxterms
 
Unfortunately, sum-of-products canonical form does not necessarily generate the simplest equation. In Section 2.3, we show how to write the same function using fewer terms.

2.2.3	Product-of-Sums Form
An alternative way of expressing Boolean functions is the product-of- sums (POS) canonical form. Each row of a truth table corresponds to a maxterm that is FALSE for that row. For example, the maxterm for the first row of a two-input truth table is (A + B) because (A + B) is FALSE when A = 0, B = 0. We can write a Boolean equation for any circuit directly from the truth table as the AND of each of the maxterms for which the output is FALSE. The product-of-sums canonical form can also be written in pi notation using the product symbol, .

Example 2.3 PRODUCT-OF-SUMS (POS) FORM
Write an equation in product-of-sums form for the truth table in Figure 2.13.

function can be written in product-of-sums form as Y = (A + B)(A + B) or, using Solution The truth table has two rows in which the output is FALSE. Hence, the pi notation, Y = Π(M0, M2) or Y = Π(0, 2). The first maxterm, (A + B), guaran-
second maxterm, (A + B), guarantees that Y = 0 for A = 1, B = 0. Figure 2.13 tees that Y = 0 for A = 0, B = 0, because any value AND 0 is 0. Likewise, the is the same truth table as Figure 2.9, showing that the same function can be
written in more than one way.
 	
Similarly, a Boolean equation for Ben’s picnic from Figure 2.10 can
obtain E = (A + R)(A + R)(A + R) or E = Π(1, 2,3). This is uglier than be written in product-of-sums form by circling the three rows of 0’s to the sum-of-products equation, E = AR, but the two equations are logically
equivalent.
Sum-of-products produces a shorter equation when the output is TRUE on only a few rows of a truth table; product-of-sums is simpler when the output is FALSE on only a few rows of a truth table.

2.3	BOOLEAN ALGEBRA
In the previous section, we learned how to write a Boolean expression given a truth table. However, that expression does not necessarily lead to the sim- plest set of logic gates. Just as you use algebra to simplify mathematical equations, you can use Boolean algebra to simplify Boolean equations. The rules of Boolean algebra are much like those of ordinary algebra but are in some cases simpler because variables have only two possible values: 0 or 1.
Boolean algebra is based on a set of axioms that we assume are correct. Axioms are unprovable in the sense that a definition cannot be
 
2.3 Boolean Algebra	59


Table 2.1 Axioms of Boolean algebra

	Axiom		Dual	Name
A1	B = 0 if B  1	A1 	B = 1 if B  0	Binary field
A2	
 
0 = 1	A2 	
 
1 = 0	NOT
A3	0 • 0 = 0	A3 	1 + 1 = 1	AND/OR
A4	1 • 1 = 1	A4 	0 + 0 = 0	AND/OR
A5	0 • 1 = 1 • 0 = 0	A5 	1 + 0 = 0 + 1 = 1	AND/OR

proved. From these axioms, we prove all the theorems of Boolean alge- bra. These theorems have great practical significance because they teach us how to simplify logic to produce smaller and less costly circuits.
Axioms and theorems of Boolean algebra obey the principle of dual- ity. If the symbols 0 and 1 and the operators • (AND) and + (OR) are interchanged, the statement will still be correct. We use the prime sym- bol ( ) to denote the dual of a statement.

 
2.3.1	Axioms
Table 2.1 states the axioms of Boolean algebra. These five axioms and their duals define Boolean variables and the meanings of NOT, AND, and OR. Axiom A1 states that a Boolean variable B is 0 if it is not 1. The axiom’s dual, A1 , states that the variable is 1 if it is not 0. Together, A1 and A1 tell us that we are working in a Boolean or binary field of 0’s and 1’s. Axioms A2 and A2 define the NOT operation. Axioms A3 to A5 define AND; their duals, A3 to A5 define OR.

2.3.2	Theorems of One Variable
Theorems T1 to T5 in Table 2.2 describe how to simplify equations involving one variable.
The identity theorem, T1, states that for any Boolean variable B, B AND 1 = B. Its dual states that B OR 0 = B. In hardware, as shown in Figure 2.14, T1 means that if one input of a two-input AND gate is always 1, we can remove the AND gate and replace it with a wire con- nected to the variable input (B). Likewise, T1 means that if one input of a two-input OR gate is always 0, we can replace the OR gate with a wire connected to B. In general, gates cost money, power, and delay, so replacing a gate with a wire is beneficial.
The null element theorem, T2, says that B AND 0 is always equal to
0. Therefore, 0 is called the null element for the AND operation, because it nullifies the effect of any other input. The dual states that B OR 1 is always equal to 1. Hence, 1 is the null element for the OR operation. In
 



1   = B
(a)

B	B
0
(b)
Figure 2.14 Identity theorem in hardware: (a) T1, (b) T1 

 
60	CHAPTER TWO
 
Combinational Logic Design
 


 
0   =  0
(a)
B	1
1
(b)
 
Table 2.2 Boolean theorems of one variable
 
Figure 2.15 Null element theorem in hardware: (a) T2, (b) T2 
 

B   = B
(a)

B	B
B
(b)
Figure 2.16 Idempotency theorem in hardware: (a) T3, (b) T3 


B	= B

Figure 2.17 Involution theorem in hardware: T4


B
B	=  0
(a)

B	=  1
B
(b)
Figure 2.18 Complement theorem in hardware: (a) T5, (b) T5 
 

 	 


hardware, as shown in Figure 2.15, if one input of an AND gate is 0, we can replace the AND gate with a wire that is tied LOW (to 0). Likewise, if one input of an OR gate is 1, we can replace the OR gate with a wire that is tied HIGH (to 1).
Idempotency, T3, says that a variable AND itself is equal to just itself. Likewise, a variable OR itself is equal to itself. The theorem gets its name from the Latin roots: idem (same) and potent (power). The operations return the same thing you put into them. Figure 2.16 shows that idempotency again permits replacing a gate with a wire.
Involution, T4, is a fancy way of saying that complementing a vari- able twice results in the original variable. In digital electronics, two wrongs make a right. Two inverters in series logically cancel each other out and are logically equivalent to a wire, as shown in Figure 2.17. The dual of T4 is itself.
The complement theorem, T5 (Figure 2.18), states that a variable AND its complement is 0 (because one of them has to be 0). And, by dual- ity, a variable OR its complement is 1 (because one of them has to be 1).
2.3.3	Theorems of Several Variables
Theorems T6 to T12 in Table 2.3 describe how to simplify equations involving more than one Boolean variable.
Commutativity and associativity, T6 and T7, work the same as in traditional algebra. By commutativity, the order of inputs for an AND or OR function does not affect the value of the output. By associativity, the specific groupings of inputs in AND or OR operations do not affect the value of the output.
The distributivity theorem, T8, is the same as in traditional algebra, but its dual, T8 , is not. By T8, AND distributes over OR, and by T8 , OR distributes over AND. In traditional algebra, multiplication distrib- utes over addition but addition does not distribute over multiplication so that (B + C) × (B + D)  B + (C × D).
The covering, combining, and consensus theorems, T9 to T11, per-
mit us to eliminate redundant variables. With some thought, you should be able to convince yourself that these theorems are correct.
 
2.3 Boolean Algebra	61


Table 2.3 Boolean theorems of several variables












= (B + C) • (B + D)




De Morgan’s Theorem, T12, is a particularly powerful tool in digital design. The theorem explains that the complement of the product of all the terms is equal to the sum of the complement of each term. Likewise, the complement of the sum of all the terms is equal to the product of the complement of each term.
According to De Morgan’s theorem, a NAND gate is equivalent to an OR gate with inverted inputs. Similarly, a NOR gate is equivalent to an AND gate with inverted inputs. Figure 2.19 shows these De Morgan equivalent gates for NAND and NOR gates. The two symbols shown for each function are called duals. They are logically equivalent and can be used interchangeably.
The inversion circle is called a bubble. Intuitively, you can imagine that “pushing” a bubble through the gate causes it to come out at the other

 
NAND
B   Y
A
 
NOR
B   Y
A	Y
 
B	Y

     
Y = AB = A + B
 
B

Y = A + B = A B A	B	Y
 



Figure 2.19 De Morgan equivalent gates
 
62	CHAPTER TWO
 
Combinational Logic Design
 


side and flips the body of the gate from AND to OR or vice versa. For example, the NAND gate in Figure 2.19 consists of an AND body with a bubble on the output. Pushing the bubble to the left results in an OR body with bubbles on the inputs. The underlying rules for bubble pushing are
	Pushing bubbles backward (from the output) or forward (from the inputs) changes the body of the gate from AND to OR or vice versa.
	Pushing a bubble from the output back to the inputs puts bubbles on all gate inputs.
	Pushing bubbles on all gate inputs forward toward the output puts a bubble on the output.

Section 2.5.2 uses bubble pushing to help analyze circuits.


 







Figur
 







wing
 
Example 2.4 DERIVE THE PRODUCT-OF-SUMS FORM

Figure 2.20 shows the truth table for a Boolean function Y and its complement Y. Using De Morgan’s Theorem, derive the product-of-sums canonical form of Y from the sum-of-products form of Y.

Solution Figure 2.21 shows the minterms (circled) contained in Y. The sum-of- products canonical form of Y is
 

 
Y and Y
 
Y = AB + AB
 
(2.4)
 
Taking the complement of both sides and applying De Morgan’s Theorem twice,
m	we get
Y = Y = AB + AB = (AB)(AB) = (A + B)(A + B)	(2.5)
 

Figure 2.21 Truth table showing minterms for Y
 
2.3.4	The Truth Behind It All
The curious reader might wonder how to prove that a theorem is true. In Boolean algebra, proofs of theorems with a finite number of variables are easy: just show that the theorem holds for all possible values of these variables. This method is called perfect induction and can be done with a truth table.

Example 2.5 PROVING THE CONSENSUS THEOREM USING PERFECT INDUCTION
Prove the consensus theorem, T11, from Table 2.3.
Solution Check both sides of the equation for all eight combinations of B, C, and D. The truth table in Figure 2.22 illustrates these combinations. Because
BC + BD + CD = BC + BD for all cases, the theorem is proved.
 
2.3	Boolean Algebra	63
 



B	C	D	
 
BC + BD + CD	
 
BC + BD
0	0	0	0	0
0	0	1	1	1
0	1	0	0	0
0	1	1	1	1
1	0	0	0	0
1	0	1	0	0
1	1	0	1	1
1	1	1	1	1

2.3.5	Simplifying Equations
The theorems of Boolean algebra help us simplify Boolean equations. For example, consider the sum-of-products expression from the truth table of
Figure 2.9: Y = AB + AB. By the combining theorem (T10), the equation simplifies to Y = B. This may have been obvious looking at the truth table. In
general, multiple steps may be necessary to simplify more complex equations. The basic principle of simplifying sum-of-products equations is to
combine terms using the relationship PA + PA = P, where P may be any
term. How far can an equation be simplified? We define an equation in
sum-of-products form to be minimized if it uses the fewest possible implicants. If there are several equations with the same number of impli- cants, the minimal one is the one with the fewest literals.
An implicant is called a prime implicant if it cannot be combined with any other implicants in the equation to form a new implicant with fewer literals. The implicants in a minimal equation must all be prime impli- cants. Otherwise, they could be combined to reduce the number of literals.

Example 2.6 EQUATION MINIMIZATION
Minimize Equation 2.3: ABC + ABC + ABC.
Solution We start with the original equation and apply Boolean theorems step by
step, as shown in Table 2.4.
Have we simplified the equation completely at this point? Let’s take a closer look. From the original equation, the minterms ABC and ABC differ only in the variable A. So we combined the minterms to form BC. However, if we look at the original equation, we note that the last two minterms ABC and ABC also differ by a single literal (C and C). Thus, using the same method, we could have combined these two minterms to form the minterm AB We say that implicants BC and AB share the minterm ABC.
So, are we stuck with simplifying only one of the minterm pairs, or can we sim- plify both? Using the idempotency theorem, we can duplicate terms as many times as we want: B = B + B + B + B … . Using this principle, we simplify the equation
 	 
completely to its two prime implicants, BC + AB, as shown in Table 2.5.
 






Figure 2.22 Truth table proving T11










 
64	CHAPTER TWO
 
Combinational Logic Design
 


Table 2.4 Equation minimization

Step	Equation	Justification
	
 	 	 

	ABC + ABC + ABC	
1	
 	T8: Distributivity
	
 	 

2	BC(1) + ABC	T5: Complements
		
3	 
T1: Identity
	
Table 2.5 Improved equation minimization	
Step	Equation	Justification
	
 	 	 

	ABC + ABC + ABC	
		
1	 	 	 	 	T3: Idempotency
	
 	 

2	BC(A + A) + AB(C + C)	T8: Distributivity
	
 	 

3	 
T5: Complements
	
 	 

4	BC + AB	T1: Identity

Although it is a bit counterintuitive, expanding an implicant (e.g., turning AB into ABC + ABC) is sometimes useful in minimizing equa- tions. By doing this, you can repeat one of the expanded minterms to be combined (shared) with another minterm.
You may have noticed that completely simplifying a Boolean equa- tion with the theorems of Boolean algebra can take some trial and error. Section 2.7 describes a methodical technique called Karnaugh maps that makes the process easier.
Why bother simplifying a Boolean equation if it remains logically equivalent? Simplifying reduces the number of gates used to physically implement the function, thus making it smaller, cheaper, and possibly faster. The next section describes how to implement Boolean equations with logic gates.

2.4	FROM LOGIC TO GATES
A schematic is a diagram of a digital circuit showing the elements and the wires that connect them. For example, the schematic in Figure 2.23 shows a possible hardware implementation of our favorite logic func- tion, Equation 2.3:

Y = ABC + ABC + ABC	(2.3)
 
2.4	From Logic to Gates	65
A	B	C
 
minterm: ABC minterm: ABC minterm: ABC
 




Figure 2.23 Schematic of
Y = ABC + ABC + ABC
 

wires connect
Y	at a T junction

 
By drawing schematics in a consistent fashion, we make them easier to read and debug. We will generally obey the following guidelines:
	Inputs are on the left (or top) side of a schematic.
	Outputs are on the right (or bottom) side of a schematic.
	Whenever possible, gates should flow from left to right.
 Straight wires are better to use than wires with multiple corners (jagged wires waste mental effort following the wire rather than thinking about what the circuit does).
	Wires always connect at a T junction.
	A dot where wires cross indicates a connection between the wires.
	Wires crossing without a dot make no connection.
The last three guidelines are illustrated in Figure 2.24.
Any Boolean equation in sum-of-products form can be drawn as a schematic in a systematic way similar to Figure 2.23. First, draw columns for the inputs. Place inverters in adjacent columns to provide the com- plementary inputs if necessary. Draw rows of AND gates for each of the minterms. Then, for each output, draw an OR gate connected to the min- terms related to that output. This style is called a programmable logic array (PLA) because the inverters, AND gates, and OR gates are arrayed in a systematic fashion. PLAs will be discussed further in Section 5.6.
Figure 2.25 shows an implementation of the simplified equation we found using Boolean algebra in Example 2.6. Notice that the simplified circuit has significantly less hardware than that of Figure 2.23. It may also be faster because it uses gates with fewer inputs.
We can reduce the number of gates even further (albeit by a sin- gle inverter) by taking advantage of inverting gates. Observe that BC is an AND with inverted inputs. Figure 2.26 shows a schematic using this optimization to eliminate the inverter on C. Recall that by De Morgan’s
 


wires connect at a dot

 
wires crossing without a dot do not connect

 
Figure 2.24 Wire connections





A	B  C
 
Y
Figure 2.25 Schematic of
Y = BC + AB
 
66	CHAPTER TWO
 
Combinational Logic Design
 


 
A	B	C











Y
Figure 2.26 Schematic using fewer gates
 
theorem, the AND with inverted inputs is equivalent to a NOR gate. Depending on the implementation technology, it may be cheaper to use the fewest gates or to use certain types of gates in preference to others. For example, NANDs and NORs are preferred over ANDs and ORs in CMOS implementations.
Many circuits have multiple outputs, each of which computes a sep- arate Boolean function of the inputs. We can write a separate truth table for each output, but it is often convenient to write all of the outputs on a single truth table and sketch one schematic with all of the outputs.

Example 2.7 MULTIPLE-OUTPUT CIRCUITS
The dean, the department chair, the teaching assistant, and the dorm social chair each use the auditorium from time to time. Unfortunately, they occasionally con- flict, leading to disasters such as the one that occurred when the dean’s fundraising meeting with crusty trustees happened at the same time as the dorm’s BTB1 party. Alyssa P. Hacker has been called in to design a room reservation system.
The system has four inputs, A3, …, A0, and four outputs, Y3, …, Y0. These sig- nals can also be written as A3:0 and Y3:0. Each user asserts her input when she requests the auditorium for the next day. The system asserts at most one output, granting the auditorium to the highest priority user. The dean, who is paying for the system, demands highest priority (3). The department chair, teaching assis- tant, and dorm social chair have decreasing priority.
Write a truth table and Boolean equations for the system. Sketch a circuit that performs this function.
Solution This function is called a four-input priority circuit. Its symbol and truth table are shown in Figure 2.27.
We could write each output in sum-of-products form and reduce the equations using Boolean algebra. However, the simplified equations are clear by inspection from the functional description (and the truth table): Y3 is TRUE whenever A3 is asserted, so Y3 = A3. Y2 is TRUE if A2 is asserted and A3 is not asserted, so
 
Y2 = A3 A2. Y is TRUE if A1 is asserted and neither of the higher-priority inputs is asserted: Y1 = A3 A2 A1 And Y0 is TRUE whenever A0 and no other input is asserted: Y0 = A3 A2 A1 A0 The schematic is shown in Figure 2.28. An experi-
enced designer can often implement a logic circuit by inspection. Given a clear
specification, simply turn the words into equations and the equations into gates.


Notice that if A3 is asserted in the priority circuit, the outputs don’t care what the other inputs are. We use the symbol X to describe inputs
 

 
1Black light, twinkies, and beer.
 
2.5	Multilevel Combinational Logic	67





Figure 2.27 Priority circuit











 
A3A2A1A0
Y3
Y
 

A3  A2
 

A1  A0  Y3  Y2
 

Y1  Y0
 


 

Y0

Figure 2.28 Priority circuit schematic
 


Figure 2.29 Priority circuit truth table with don’t cares (X’s)
 


that the output doesn’t care about. Figure 2.29 shows that the four-input priority circuit truth table becomes much smaller with don’t cares. From this truth table, we can easily read the Boolean equations in sum-of- products form by ignoring inputs with X’s. Don’t cares can also appear in truth table outputs, as we will see in Section 2.7.3.

2.5	MULTILEVEL COMBINATIONAL LOGIC
Logic in sum-of-products form is called two-level logic because it con- sists of literals connected to a level of AND gates connected to a level of OR gates. Designers often build circuits with more than two levels of
 
68	CHAPTER TWO
 
Combinational Logic Design
 


logic gates. These multilevel combinational circuits may use less hard- ware than their two-level counterparts. Bubble pushing is especially helpful in analyzing and designing multilevel circuits.

2.5.1	Hardware Reduction
Some logic functions require an enormous amount of hardware when built using two-level logic. A notable example is the XOR function of multiple variables. For example, consider building a three-input XOR using the two-level techniques we have studied so far.
Recall that an N-input XOR produces a TRUE output when an odd number of inputs are TRUE. Figure 2.30 shows the truth table for a three-input XOR with the rows circled that produce TRUE outputs. From the truth table, we read off a Boolean equation in sum-of-products form in Equation 2.6. Unfortunately, there is no way to simplify this equation into fewer implicants.
 
Y = ABC + ABC + ABC + ABC
 
(2.6)
 
On the other hand, A ⊕ B ⊕ C = (A ⊕ B) ⊕ C (prove this to your-
self by perfect induction if you are in doubt). Therefore, the three-input
XOR can be built out of a cascade of two-input XORs, as shown in Figure 2.31.
Similarly, an eight-input XOR would require 128 eight-input AND gates and one 128-input OR gate for a two-level sum-of-products imple- mentation. A much better option is to use a tree of two-input XOR gates, as shown in Figure 2.32.



A	B	C

XOR3
A
 


Figure 2.30 Three-input XOR:
(a)	functional specification and
(b)	two-level logic implementation
 
B	Y
C
Y = A  B  C

A	B	C	Y
0	0	0	0
0	0	1	1
0	1	0	1
0	1	1	0
1	0	0	1
1	0	1	0
1	1	0	0
1	1	1	1
(a)			
 











Y
(b)
 
2.5	Multilevel Combinational Logic	69


Selecting the best multilevel implementation of a specific logic	A
function is not a simple process. Moreover, “best” has many meanings:	B
fewest gates, fastest, shortest design time, least cost, least power con-	C	Y
 
sumption. In Chapter 5, you will see that the “best” circuit in one tech- nology is not necessarily the best in another. For example, we have been using ANDs and ORs, but in CMOS, NANDs and NORs are more effi- cient. With some experience, you will find that you can create a good multilevel design by inspection for most circuits. You will develop some of this experience as you study circuit examples through the rest of this book. As you are learning, explore various design options and think about the trade-offs. Computer-aided design (CAD) tools are also avail- able to search a vast space of possible multilevel designs and seek the one that best fits your constraints given the available building blocks.

2.5.2	Bubble Pushing
You may recall from Section 1.7.6 that CMOS circuits prefer NANDs and NORs over ANDs and ORs. But reading the equation by inspection from a multilevel circuit with NANDs and NORs can get pretty hairy. Figure 2.33 shows a multilevel circuit whose function is not immediately clear by inspection. Bubble pushing is a helpful way to redraw these cir- cuits so that the bubbles cancel out and the function can be more easily determined. Building on the principles from Section 2.3.3, the guidelines for bubble pushing are as follows:
•	Begin at the output of the circuit and work toward the inputs.
•	Push any bubbles on the final output back toward the inputs so that you can read an equation in terms of the output (e.g., Y) instead of the complement of the output (Y).
•	Working backward, draw each gate in a form so that bubbles can- cel. If the current gate has an input bubble, draw the preceding gate with an output bubble. If the current gate does not have an input bubble, draw the preceding gate without an output bubble.

Figure 2.34 shows how to redraw Figure 2.33 according to the bubble pushing guidelines. Starting at the output Y, the NAND gate has a bubble on the output that we wish to eliminate. We push the output bubble back to form an OR with inverted inputs, shown in
 
Figure 2.31 Three-input XOR using two-input XORs

Figure 2.32 Eight-input XOR using seven two-input XORs
 

A
B	Figure 2.33 Multilevel circuit
C	Y	using NANDs and NORs
D
 
70	CHAPTER TWO
 
Combinational Logic Design
 



A B

C	Y
D
(a)

 



Figure 2.34 Bubble-pushed circuit
 
A B

C	Y
D
(b)
 


 
A B

C D

(c)	
 



Y

Y = ABC + D
 


Figure 2.34(a). Working to the left, the rightmost gate has an input bub- ble that cancels with the output bubble of the middle NAND gate, so no change is necessary, as shown in Figure 2.34(b). The middle gate has no input bubble, so we transform the leftmost gate to have no output bubble, as shown in Figure 2.34(c). Now, all of the bubbles in the cir- cuit cancel except at the inputs, so the function can be read by inspec- tion in terms of ANDs and ORs of true or complementary inputs:
Y = ABC + D.
For emphasis of this last point, Figure 2.35 shows a circuit logically
equivalent to the one in Figure 2.34. The functions of internal nodes are labeled in blue. Because bubbles in series cancel, we can ignore the bub- bles on the output of the middle gate and on one input of the rightmost gate to produce the logically equivalent circuit of Figure 2.35.


 


Figure 2.35 Logically equivalent bubble-pushed circuit
 
A B

C	Y
D

Y = ABC + D
 
2.6	X’s and Z’s, Oh My	71
 


 
Example 2.8 BUBBLE PUSHING FOR CMOS LOGIC
Most designers think in terms of AND and OR gates, but suppose you would like to implement the circuit in Figure 2.36 in CMOS logic, which favors NAND and NOR gates. Use bubble pushing to convert the circuit to NANDs, NORs, and inverters.
Solution A brute force solution is to just replace each AND gate with a NAND and an inverter, and each OR gate with a NOR and an inverter, as shown in Figure 2.37. This requires eight gates. Notice that the inverter is drawn with the bubble on the front rather than back, to emphasize how the bubble can cancel with the preceding inverting gate.
For a better solution, observe that bubbles can be added to the output of a gate and the input of the next gate without changing the function, as shown in Figure 2.38(a). The final AND is converted to a NAND and an inverter, as shown in Figure 2.38(b). This solution requires only five gates.
 



Figure 2.36 Circuit using ANDs and ORs
 

 



Figure 2.37 Poor circuit using NANDs and NORs






Figure 2.38 Better circuit using NANDs and NORs

(a)	(b)


 
2.6	X’S AND Z’S, OH MY
Boolean algebra is limited to 0’s and 1’s. However, real circuits can also have illegal and floating values, represented symbolically by X and Z.

2.6.1	Illegal Value: X
The symbol X indicates that the circuit node has an unknown or illegal
value. This commonly happens if it is being driven to both 0 and 1 at the
 



A = 1 B = 0
 





Y = X
 
same time. Figure 2.39 shows a case where node Y is driven both HIGH and LOW. This situation, called contention, is considered to be an error
 
Figure 2.39 Circuit with contention
 
72	CHAPTER TWO
 
Combinational Logic Design
 


and must be avoided. The actual voltage on a node with contention may be somewhere between 0 and VDD, depending on the relative strengths of the gates driving HIGH and LOW. It is often, but not always, in the forbidden zone. Contention also can cause large amounts of power to flow between the fighting gates, resulting in the circuit getting hot and possibly damaged.
X values are also sometimes used by circuit simulators to indicate an uninitialized value. For example, if you forget to specify the value of an input, the simulator may assume that it is an X to warn you of the problem.
As mentioned in Section 2.4, digital designers also use the symbol X to indicate “don’t care” values in truth tables. Be sure not to mix up the two meanings. When X appears in a truth table, it indicates that the value of the variable in the truth table is unimportant (can be either 0 or 1). When X appears in a circuit, it means that the circuit node has an unknown or illegal value.

 


Tristate Buffer
E
A   Y

E	A	Y
0	0	Z
0	1	Z
1	0	0
1	1	1
Figure 2.40 Tristate buffer


E
 
2.6.2	Floating Value: Z
The symbol Z indicates that a node is being driven neither HIGH nor LOW. The node is said to be floating, high impedance, or high Z. A typical misconception is that a floating or undriven node is the same as a logic 0. In reality, a floating node might be 0, might be 1, or might be at some voltage in between, depending on the history of the system. A floating node does not always mean there is an error in the circuit, so long as some other circuit element does drive the node to a valid logic level when the value of the node is relevant to circuit operation.
One common way to produce a floating node is to forget to con- nect a voltage to a circuit input or to assume that an unconnected input is the same as an input with the value of 0. This mistake may cause the circuit to behave erratically, as the floating input randomly changes from 0 to 1. Indeed, touching the circuit may be enough to trigger the change by means of static electricity from the body. We have seen cir-
 
A	Y	cuits that operate correctly only as long as the student keeps a finger pressed on a chip.
The tristate buffer, shown in Figure 2.40, has three possible output states: HIGH (1), LOW (0), and floating (Z). The tristate buffer has an input A, output Y, and enable E. When the enable is TRUE, the tristate buffer acts as a simple buffer, transferring the input value to the output. When the enable is FALSE, the output is allowed to float (Z).
 
Figure 2.41 Tristate buffer with active low enable
 
The tristate buffer in Figure 2.40 has an active high enable. That is, when the enable is HIGH (1), the buffer is enabled. Figure 2.41 shows a
 
2.7	Karnaugh Maps	73
 











shared bus
 










Figure 2.42 Tristate bus connecting multiple chips
 









tristate buffer with an active low enable. When the enable is LOW (0), the buffer is enabled. We show that the signal is active low by putting a bubble on its input wire. We often indicate an active low input by draw- ing a bar over its name, E, or appending the letters “b” or “bar” after its name, Eb or Ebar.
Tristate buffers are commonly used on busses that connect multiple chips. For example, a microprocessor, a video controller, and an Ethernet controller might all need to communicate with the memory system in a personal computer. Each chip can connect to a shared memory bus using tristate buffers, as shown in Figure 2.42. Only one chip at a time is allowed to assert its enable signal to drive a value onto the bus. The other chips must produce floating outputs so that they do not cause con- tention with the chip talking to the memory. Any chip can read the information from the shared bus at any time. Such tristate busses were once common. However, in modern computers, higher speeds are possi- ble with point-to-point links, in which chips are connected to each other directly rather than over a shared bus.

2.7	KARNAUGH MAPS
After working through several minimizations of Boolean equations using Boolean algebra, you will realize that, if you’re not careful, you sometimes end up with a completely different equation instead of a sim- plified equation. Karnaugh maps (K-maps) are a graphical method for simplifying Boolean equations. They were invented in 1953 by Maurice Karnaugh, a telecommunications engineer at Bell Labs. K-maps work
 
74	CHAPTER TWO
 
Combinational Logic Design
 


well for problems with up to four variables. More important, they give insight into manipulating Boolean equations.
Recall that logic minimization involves combining terms. Two terms containing an implicant P and the true and complementary forms of
some variable A are combined to eliminate A : PA + PA = P. Karnaugh
maps make these combinable terms easy to see by putting them next to
each other in a grid.
Figure 2.43 shows the truth table and K-map for a three-input func- tion. The top row of the K-map gives the four possible values for the A and B inputs. The left column gives the two possible values for the C input. Each square in the K-map corresponds to a row in the truth table and contains the value of the output Y for that row. For example, the top left square corresponds to the first row in the truth table and indi- cates that the output value Y = 1 when ABC = 000. Just like each row in a truth table, each square in a K-map represents a single minterm. For the purpose of explanation, Figure 2.43(c) shows the minterm corresponding to each square in the K-map.
Each square, or minterm, differs from an adjacent square by a change in a single variable. This means that adjacent squares share all the same literals except one, which appears in true form in one square and in complementary form in the other. For example, the squares rep- resenting the minterms ABC and ABC are adjacent and differ only in the variable C. You may have noticed that the A and B combinations in the top row are in a peculiar order: 00, 01, 11, 10. This order is called a Gray code. It differs from ordinary binary order (00, 01, 10, 11) in that adjacent entries differ only in a single variable. For example, 01:11 changes only A from 0 to 1, while 01:10 would change A from 0 to 1 and B from 1 to 0. Hence, writing the combinations in binary order would not have produced our desired property of adjacent squares dif- fering only in one variable.
The K-map also “wraps around.” The squares on the far right are effectively adjacent to the squares on the far left in that they differ only in one variable, A. In other words, you could take the map and roll it into a cylinder, then join the ends of the cylinder to form a torus (i.e., a donut), and still guarantee that adjacent squares would differ only in one variable.

2.7.1	Circular Thinking
In the K-map in Figure 2.43, only two minterms are present in the equa- tion, ABC and ABC, as indicated by the 1’s in the left column. Reading the minterms from the K-map is exactly equivalent to reading equations in sum-of-products form directly from the truth table.
 
2.7 Karnaugh Maps	75
 




00	01

0

1
 




11	10
 




00	01

0

1
 




11	10




 

 
(a)
 
(b)	
 
(c)	
 
Figure 2.43 Three-input function: (a) truth table, (b) K-map, (c) K-map showing minterms

Y  AB
 
C	00	01
0
1
 
11	10
 
Figure 2.44 K-map minimization
 
As before, we can use Boolean algebra to minimize equations in sum-of- products form.
Y = ABC + ABC = AB(C + C) = AB	(2.7)
K-maps help us do this simplification graphically by circling 1’s in adjacent squares, as shown in Figure 2.44. For each circle, we write the corresponding implicant. Remember from Section 2.2 that an implicant is the product of one or more literals. Variables whose true and comple- mentary forms are both in the circle are excluded from the implicant. In this case, the variable C has both its true form (1) and its complementary form (0) in the circle, so we do not include it in the implicant. In other words, Y is TRUE when A = B = 0, independent of C. So, the implicant is AB. The K-map gives the same answer we reached using Boolean algebra.

2.7.2	Logic Minimization with K-Maps
K-maps provide an easy visual way to minimize logic. Simply circle all the rectangular blocks of 1’s in the map, using the fewest possible num- ber of circles. Each circle should be as large as possible. Then, read off the implicants that were circled.
More formally, recall that a Boolean equation is minimized when it is written as a sum of the fewest number of prime implicants. Each circle on the K-map represents an implicant. The largest possible circles are prime implicants.
 
76	CHAPTER TWO
 
Combinational Logic Design
 



For example, in the K-map of Figure 2.44, ABC and ABC are impli- cants, but not prime implicants. Only AB is a prime implicant in that K-map. Rules for finding a minimized equation from a K-map are as follows:
   Use the fewest circles necessary to cover all the 1’s.
   All the squares in each circle must contain 1’s.
	Each circle must span a rectangular block that is a power of 2 (i.e., 1, 2, or 4) squares in each direction.
	Each circle should be as large as possible.
	A circle may wrap around the edges of the K-map.
	A 1 in a K-map may be circled multiple times if doing so allows fewer circles to be used.

Example 2.9 MINIMIZATION OF A THREE-VARIABLE FUNCTION USING A K-MAP
Suppose we have the function Y = F(A, B, C) with the K-map shown in Figure
2.45. Minimize the equation using the K-map.
Solution Circle the 1’s in the K-map using as few circles as possible, as shown in Figure 2.46. Each circle in the K-map represents a prime implicant, and the dimension of each circle is a power of two (2 × 1 and 2 × 2). We form the prime implicant for each circle by writing those variables that appear in the circle only in true or only in complementary form.
For example, in the 2 × 1 circle, the true and complementary forms of B are included in the circle, so we do not include B in the prime implicant. However, only the true form of A (A) and complementary form of C (C) are in this circle, so we include these variables in the prime implicant AC. Similarly, the 2 × 2 circle covers all squares where B = 0, so the prime implicant is B.
Notice how the top-right square (minterm) is covered twice to make the prime implicant circles as large as possible. As we saw with Boolean algebra techniques, this is equivalent to sharing a minterm to reduce the size of the implicant. Also notice how the circle covering four squares wraps around the sides of the K-map.

 



Figure 2.45 K-map for Example 2.9
 
Y AB C
0

1
 


00	01
 


11	10
 
2.7 Karnaugh Maps	77
 



Y AB C
0

1
 




00	01
 


AC
11	10
 







Figure 2.46 Solution for Example 2.9
 

   
Y = AC + B
B





 
Example 2.10 SEVEN-SEGMENT DISPLAY DECODER
A seven-segment display decoder takes a 4-bit data input D3:0 and produces seven outputs to control light-emitting diodes to display a digit from 0 to 9. The seven outputs are often called segments a through g, or Sa–Sg, as defined in Figure 2.47. The digits are shown in Figure 2.48. Write a truth table for the outputs, and use K-maps to find Boolean equations for outputs Sa and Sb. Assume that illegal input values (10–15) produce a blank readout.
Solution The truth table is given in Table 2.6. For example, an input of 0000 should turn on all segments except Sg.
Each of the seven outputs is an independent function of four variables. The K-maps for outputs Sa and Sb are shown in Figure 2.49. Remember that adjacent squares may differ in only a single variable, so we label the rows and columns in Gray code order: 00, 01, 11, 10. Be careful to also remember this ordering when entering the output values into the squares.
Next, circle the prime implicants. Use the fewest number of circles necessary to cover all the 1’s. A circle can wrap around the edges (vertical and horizontal), and a 1 may be circled more than once. Figure 2.50 shows the prime implicants and the simplified Boolean equations.
Note that the minimal set of prime implicants is not unique. For example, the 0000 entry in the Sa K-map was circled, along with the 1000 entry to produce the D2 D1 D0 minterm. The circle could have included the 0010 entry instead, producing a D3 D2 D0 minterm, as shown with dashed lines in Figure 2.51.
Figure 2.52 (see page 80) illustrates a common error in which a nonprime implicant was chosen to cover the 1 in the upper left corner. This minterm, D3 D2 D1 D0 , gives a sum-of-products equation that is not minimal. The minterm could have been combined with either of the adjacent ones to form a larger cir- cle, as was done in the previous two figures.
 
 





Figure 2.47 Seven-segment display decoder icon
 
78	CHAPTER TWO
 
Combinational Logic Design
 



 
Figure 2.48 Seven-segment display digits
 



0	1	2
 



3	4	5	6	7	8	9
 



Table 2.6 Seven-segment display decoder truth table

D3:0	Sa	Sb	Sc	Sd	Se	Sf	Sg
0000	1	1	1	1	1	1	0
0001	0	1	1	0	0	0	0
0010	1	1	0	1	1	0	1
0011	1	1	1	1	0	0	1
0100	0	1	1	0	0	1	1
0101	1	0	1	1	0	1	1
0110	1	0	1	1	1	1	1
0111	1	1	1	0	0	0	0
1000	1	1	1	1	1	1	1
1001	1	1	1	0	0	1	1
others	0	0	0	0	0	0	0



Sa	Sb
01	11	10	01	11	10
	
00	
1	
0	
0	
1	
00
Figure 2.49 Karnaugh maps for
Sa and Sb	
01	
0	
1	
0	
1	
01
	
11	
1	
1	
0	
0	
11
	
10	
1	
1	
0	
0	
10
 
2.7	Karnaugh Maps	79
 
Sa
D1:0
 
D3:2 00
 
01	11	10
 
Sb D1:0
 
D3:2
00
 
01	11	10
 
D2 D1D0




D3D1
 




D3D2D1






Sa = D3D1 + D3D2D0 + D3D2D1 + D2D1D0
 
00

D3D1D0
01


11


10

D3D2
 

 










Sb = D3D2 + D2D1 + D3D1D0 + D3D1D0
 
Figure 2.50 K-map solution for Example 2.10

Sa
01	11	10


     
 
D3D2D0




D3D
 



D3D2D1
 

Figure 2.51 Alternative K-map for Sa showing different set of prime implicants
 



 	 	   	     
Sa = D3D1 + D3D2D0 + D3D2D1 + D3D2D0



2.7.3	Don’t Cares
Recall that “don’t care” entries for truth table inputs were introduced in Section 2.4 to reduce the number of rows in the table when some variables do not affect the output. They are indicated by the symbol X, which means that the entry can be either 0 or 1.
Don’t cares also appear in truth table outputs where the output value is unimportant or the corresponding input combination can never
 
80	CHAPTER TWO
 
Combinational Logic Design
 


 
Sa
D1:0
 

D3:2
00
 


01	11	10
 




Figure 2.52 Alternative K-map for Sa showing incorrect nonprime implicant
 

00	1

D3D2D1D0
 

0	0	1
 




D3D2D1
 

 
D3D



Sa = D3D1 + D3D2D0 + D3D2D1 + D3D2D1D0

happen. Such outputs can be treated as either 0’s or 1’s at the designer’s discretion.
In a K-map, X’s allow for even more logic minimization. They can be circled if they help cover the 1’s with fewer or larger circles, but they do not have to be circled if they are not helpful.

Example 2.11 SEVEN-SEGMENT DISPLAY DECODER WITH DON’T CARES
Repeat Example 2.10 if we don’t care about the output values for illegal input values of 10 to 15.
Solution The K-map is shown in Figure 2.53 with X entries representing don’t care. Because don’t cares can be 0 or 1, we circle a don’t care if it allows us to cover the 1’s with fewer or bigger circles. Circled don’t cares are treated as 1’s, whereas uncircled don’t cares are 0’s. Observe how a 2 × 2 square wrapping around all four corners is circled for segment Sa. Use of don’t cares simplifies the logic substantially.



2.7.4	The Big Picture
Boolean algebra and Karnaugh maps are two methods of logic simplifi- cation. Ultimately, the goal is to find a low-cost method of implementing a particular logic function.
In modern engineering practice, computer programs called logic syn- thesizers produce simplified circuits from a description of the logic func- tion, as we will see in Chapter 4. For large problems, logic synthesizers are much more efficient than humans. For small problems, a human with a bit of experience can find a good solution by inspection. Neither of the
 
2.8	Combinational Building Blocks	81
 


Sa D3:2 D1:0	00
00
 




01	11	10
 


Sb D3:2 D1:0	00
00
 




01	11	10
 

 
01	01

11	11

10	10

Sa = D3 + D2D0 + D2D0 + D1	Sb = D2 + D1D0 + D1D0
 

Figure 2.53 K-map solution with don’t cares
 

authors has ever used a Karnaugh map in real life to solve a practical problem. But the insight gained from the principles underlying Karnaugh maps is valuable. And Karnaugh maps often appear at job interviews!

2.8	COMBINATIONAL BUILDING BLOCKS	S
Combinational logic is often grouped into larger building blocks to	D0
build more complex systems. This is an application of the principle of	Y
abstraction, hiding the unnecessary gate-level details to emphasize the	D1
function of the building block. We have already studied three such build- ing blocks: full adders (from Section 2.1), priority circuits (from Section 2.4), and seven-segment display decoders (from Section 2.7). This sec- tion introduces two more commonly used building blocks: multiplexers and decoders. Chapter 5 covers other combinational building blocks.

 
2.8.1	Multiplexers
Multiplexers are among the most commonly used combinational cir- cuits. They choose an output from among several possible inputs, based on the value of a select signal. A multiplexer is sometimes affectionately called a mux.

2:1 Multiplexer
Figure 2.54 shows the schematic and truth table for a 2:1 multiplexer with two data inputs D0 and D1, a select input S, and one output Y. The multiplexer chooses between the two data inputs, based on the select: if S = 0, Y = D0, and if S = 1, Y = D1. S is also called a control signal because it controls what the multiplexer does.
A 2:1 multiplexer can be built from sum-of-products logic as shown in Figure 2.55. The Boolean equation for the multiplexer may be derived
 



Figure 2.54 2:1 multiplexer symbol and truth table
 
82	CHAPTER TWO
 
Combinational Logic Design
 


Y D1:0
 
S	00	01
0
1
 
11	10
 
Figure 2.55 2:1 multiplexer implementation using two-level logic
 

 
Y = D0S + D1S

D0



S D1
 


Y
S

D0	using a Karnaugh map or read off by inspection (Y is 1 if S = 0 AND D0
Y	is 1 OR if S = 1 AND D1 is 1).
Alternatively, multiplexers can be built from tristate buffers as
D1	shown in Figure 2.56. The tristate enables are arranged such that
 

 
Y = D S + D S
 
exactly one tristate buffer is active at all times. When S = 0, tristate T0
 
0	1	is enabled, allowing D0 to flow to Y. When S = 1, tristate T1 is enabled,
 
Figure 2.56 Multiplexer using tristate buffers











S1:0
D0
 
allowing D1 to flow to Y.

Wider Multiplexers
A 4:1 multiplexer has four data inputs and one output, as shown in Figure 2.57. Two select signals are needed to choose among the four data inputs. The 4:1 multiplexer can be built using sum-of-products logic, tristates, or multiple 2:1 multiplexers, as shown in Figure 2.58.
The product terms enabling the tristates can be formed using AND gates and inverters. They can also be formed using a decoder, which we will introduce in Section 2.8.2.
Wider multiplexers, such as 8:1 and 16:1 multiplexers, can be built by expanding the methods shown in Figure 2.58. In general, an N:1 multiplexer needs log2N select lines. Again, the best implementation choice depends on the target technology.
 
D1
D2	Multiplexer Logic
D3
Multiplexers can be used as lookup tables to perform logic functions.
 
Figure 2.57 4:1 multiplexer
 
Figure 2.59 shows a 4:1 multiplexer used to implement a two-input
 
2.8 Combinational Building Blocks	83
S1  S0
 


D0	D0
D1
D1
2

D3
D2


Y	D3
 

   
S1S0


S0	S1

D0
Y
D1
Y
D2 D3
 






Figure 2.58 4:1 multiplexer implementations: (a) two-level logic, (b) tristates, (c) hierarchical
 
(a)	(b)	(c)

 
AND gate. The inputs, A and B, serve as select lines. The multiplexer data inputs are connected to 0 or 1, according to the corresponding row of the truth table. In general, a 2N-input multiplexer can be programmed to perform any N-input logic function by applying 0’s and 1’s to the appropriate data inputs. Indeed, by changing the data inputs, the multi- plexer can be reprogrammed to perform a different function.
With a little cleverness, we can cut the multiplexer size in half, using only a 2N–1-input multiplexer to perform any N-input logic function. The strategy is to provide one of the literals, as well as 0’s and 1’s, to the multiplexer data inputs.
To illustrate this principle, Figure 2.60 shows two-input AND and XOR functions implemented with 2:1 multiplexers. We start with an ordi- nary truth table and then combine pairs of rows to eliminate the right- most input variable by expressing the output in terms of this variable. For example, in the case of AND, when A = 0, Y = 0, regardless of B. When A = 1, Y = 0 if B = 0 and Y = 1 if B = 1, so Y = B. We then use the multi- plexer as a lookup table according to the new, smaller truth table.

Example 2.12 LOGIC WITH MULTIPLEXERS
Alyssa P. Hacker needs to implement the function Y = AB + BC + ABC to fin- ish her senior project, but when she looks in her lab kit, the only part she has left
is an 8:1 multiplexer. How does she implement the function?
Solution Figure 2.61 shows Alyssa’s implementation using a single 8:1 multi- plexer. The multiplexer acts as a lookup table, where each row in the truth table corresponds to a multiplexer input.
 

A	B	Y
0	0	0
0	1	0
1	0	0
1	1	1
Y = AB A B 

Y


Figure 2.59 4:1 multiplexer implementation of two-input AND function
 

 
 
84	CHAPTER TWO
 
Combinational Logic Design
 


 






Figure 2.60 Multiplexer logic using variable inputs
 



Y = AB






Y = A  B
 
A


Y
B
(a)

A


Y


(b)	
 

A B C



Figure 2.61 Alyssa’s circuit:
(a)	truth table, (b) 8:1 multiplexer	Y
implementation


     
 
Y = AB + BC + ABC
(a)
 

(b)
 


 
Example 2.13 LOGIC WITH MULTIPLEXERS, REPRISED
Alyssa turns on her circuit one more time before the final presentation and blows up the 8:1 multiplexer. (She accidently powered it with 20V instead of 5 V after not sleeping all night.) She begs her friends for spare parts and they give her a 4:1 multiplexer and an inverter. Can she build her circuit with only these parts?
Solution Alyssa reduces her truth table to four rows by letting the output depend on C. (She could also have chosen to rearrange the columns of the truth table to let the output depend on A or B.) Figure 2.62 shows the new design.


2.8.2	Decoders
A decoder has N inputs and 2N outputs. It asserts exactly one of its outputs depending on the input combination. Figure 2.63 shows a 2:4 decoder. When A1:0 = 00, Y0 is 1. When A1:0 = 01, Y1 is 1. And so forth. The outputs are called one-hot, because exactly one is “hot” (HIGH) at a given time.
 
2.8	Combinational Building Blocks	85
 











(a)
 





AB 

C	Y

(b)	(c)
 






Figure 2.62 Alyssa’s new circuit
 

 
 
Example 2.14 DECODER IMPLEMENTATION
Implement a 2:4 decoder with AND and NOT gates.
Solution Figure 2.64 shows an implementation for the 2:4 decoder, using four AND gates. Each gate depends on either the true or the complementary form of each input. In general, an N:2N decoder can be constructed from 2N N-input AND gates that accept the various combinations of true or complementary inputs. Each output in a decoder represents a single minterm. For example, Y0 represents the minterm A1 A0. This fact will be handy when using decoders with other digital building blocks.

 
 

 





A1	A0	Y3	Y2	Y1	Y0
0	0	0	0	0	1
0	1	0	0	1	0
1	0	0	1	0	0
1	1	1	0	0	0
Figure 2.63 2:4 decoder
 

A1	A0




Y3 Y2 Y1
 





Decoder Logic
 
Y0

Figure 2.64 2:4 decoder implementation
 

Minterm
AB
A	AB
B	AB
AB
 
Decoders can be combined with OR gates to build logic functions. Figure 2.65 shows the two-input XNOR function using a 2:4 decoder and a single OR gate. Because each output of a decoder represents a sin- gle minterm, the function is built as the OR of all of the minterms in the
 

 
Y = A  B
Y
Figure 2.65 Logic function using
 
function. In Figure 2.65, Y
 
= AB + AB = A ⊕ B.
 
decoder
 
86	CHAPTER TWO
 
Combinational Logic Design
 


When using decoders to build logic, it is easiest to express functions as a truth table or in canonical sum-of-products form. An N-input func- tion with M 1’s in the truth table can be built with an N:2N decoder and an M-input OR gate attached to all of the minterms containing 1’s in the truth table. This concept will be applied to the building of read-only memories (ROMs) in Section 5.5.6.

2.9	TIMING
In previous sections, we have been concerned primarily with whether the circuit works—ideally, using the fewest gates. However, as any seasoned circuit designer will attest, one of the most challenging issues in circuit design is timing: making a circuit run fast.
An output takes time to change in response to an input change. Figure 2.66 shows the delay between an input change and the subse- quent output change for a buffer. The figure is called a timing diagram; it portrays the transient response of the buffer circuit when an input changes. The transition from LOW to HIGH is called the rising edge. Similarly, the transition from HIGH to LOW (not shown in the figure) is called the falling edge. The blue arrow indicates that the rising edge of Y is caused by the rising edge of A. We measure delay from the 50% point of the input signal, A, to the 50% point of the output signal, Y. The 50% point is the point at which the signal is halfway (50%) between its LOW and HIGH values as it transitions.

2.9.1	Propagation and Contamination Delay
Combinational logic is characterized by its propagation delay and con- tamination delay. The propagation delay tpd is the maximum time from when any input changes until the output or outputs reach their final value. The contamination delay tcd is the minimum time from when any input changes until any output starts to change its value.


A	Y



Figure 2.66 Circuit delay




Time
 
2.9 Timing	87
A	Y
Figure 2.67 Propagation and contamination delay
Time

Figure 2.67 illustrates a buffer’s propagation delay and contamina- tion delay in blue and gray, respectively. The figure shows that A is ini- tially either HIGH or LOW and changes to the other state at a particular time; we are interested only in the fact that it changes, not what value it has. In response, Y changes some time later. The arcs indicate that Y may start to change tcd after A transitions and that Y definitely settles to its new value within tpd.
The underlying causes of delay in circuits include the time required to charge the capacitance in a circuit and the speed of light. tpd and tcd may be different for many reasons, including
	different rising and falling delays
	multiple inputs and outputs, some of which are faster than others
	circuits slowing down when hot and speeding up when cold
Calculating tpd and tcd requires delving into the lower levels of abstraction beyond the scope of this book. However, manufacturers nor- mally supply data sheets specifying these delays for each gate.
Along with the factors already listed, propagation and contamina- tion delays are also determined by the path a signal takes from input to output. Figure 2.68 shows a four-input logic circuit. The critical path, shown in blue, is the path from input A or B to output Y. It is the longest—and, therefore, the slowest—path because the input travels

 

Critical Path
A B
C
 




Figure 2.68 Short path and critical path
 
D	Y
Short Path
 
88	CHAPTER TWO
 
Combinational Logic Design
 


 

A = 1  0
B = 1
C = 0
D = 1
 

 n1
 



 n2
 
Critical Path

A

Y = 1  0	n1

n2
 

Y

Time

 

A = 1	n1
B = 1
C = 0
 
Short Path


n2
 
D = 1  0	Y = 1  0

Time
Figure 2.69 Critical and short path waveforms


through three gates to the output. This path is critical because it limits the speed at which the circuit operates. The short path through the cir- cuit, shown in gray, is from input D to output Y. This is the shortest— and, therefore, the fastest—path through the circuit because the input travels through only a single gate to the output.
The propagation delay of a combinational circuit is the sum of the propagation delays through each element on the critical path. The con- tamination delay is the sum of the contamination delays through each element on the short path. These delays are illustrated in Figure 2.69 and are described by the following equations:

 
tpd
 
= 2tpd– AND + tpd–OR	(2.8)
 
tcd
 
= tcd– AND	(2.9)
 

 
Example 2.15 FINDING DELAYS
Ben Bitdiddle needs to find the propagation delay and contamination delay of the circuit shown in Figure 2.70. According to his data book, each gate has a propagation delay of 100 picoseconds (ps) and a contamination delay of 60 ps.
 
2.9 Timing	89
Solution Ben begins by finding the critical path and the shortest path through the circuit. The critical path, highlighted in blue in Figure 2.71, is from input A or B through three gates to the output Y. Hence, tpd is three times the propagation delay of a single gate, or 300 ps.
The shortest path, shown in gray in Figure 2.72, is from input C, D, or E through two gates to the output Y. There are only two gates in the shortest path, so tcd is 120 ps.

A B
C	Y	Figure 2.70 Ben’s circuit
D E

A B
C	Y	Figure 2.71 Ben’s critical path
D			 E

A B
C	Y	Figure 2.72 Ben’s shortest path
D E

Example 2.16 MULTIPLEXER TIMING: CONTROL-CRITICAL VS. DATA-CRITICAL
Compare the worst-case timing of the three four-input multiplexer designs shown in Figure 2.58 on page 83. Table 2.7 lists the propagation delays for the components. What is the critical path for each design? Given your timing analy- sis, why might you choose one design over the other?
Solution One of the critical paths for each of the three design options is high- lighted in blue in Figures 2.73 and 2.74. tpd_sy indicates the propagation delay from input S to output Y; tpd_dy indicates the propagation delay from input D to output Y; tpd for the circuit is the worst of the two: max(tpd_sy, tpd_dy).
For both the two-level logic and tristate implementations in Figure 2.73, the crit- ical path is from one of the control signals S to the output Y: tpd = tpd_sy. These circuits are control critical, because the critical path is from the control signals to the output. Any additional delay in the control signals will add directly to the worst-case delay. The delay from D to Y in Figure 2.73(b) is only 50 ps, com- pared with the delay from S to Y of 125 ps.
 
90	CHAPTER TWO
 
Combinational Logic Design
 


Figure 2.74 shows the hierarchical implementation of the 4:1 multiplexer using two stages of 2:1 multiplexers. The critical path is from any of the D inputs to the output. This circuit is data critical, because the critical path is from the data input to the output: tpd = tpd_dy.
If data inputs arrive well before the control inputs, we would prefer the design with the shortest control-to-output delay (the hierarchical design in Figure 2.74). Similarly, if the control inputs arrive well before the data inputs, we would prefer the design with the shortest data-to-output delay (the tristate design in Figure 2.73(b)).
The best choice depends not only on the critical path through the circuit and the input arrival times but also on the power, cost, and availability of parts.


Table 2.7 Timing specifications for multiplexer circuit elements

Gate	tpd (ps)
NOT	30
2-input AND	60
3-input AND	80
4-input OR	90
tristate (A to Y)	50
tristate (enable to Y)	35


2.9.2	Glitches
So far, we have discussed the case where a single input transition causes a single output transition. However, it is possible that a single input transition can cause multiple output transitions. These are called glitches or hazards. Although glitches usually don’t cause problems, it is import- ant to realize that they exist and recognize them when looking at timing diagrams. Figure 2.75 shows a circuit with a glitch and the Karnaugh map of the circuit.
The Boolean equation is correctly minimized, but let’s look at what happens when A = 0, C = 1, and B transitions from 1 to 0. Figure 2.76 (see page 92) illustrates this scenario. The short path (shown in gray) goes through two gates, the AND and OR gates. The critical path (shown in blue) goes through an inverter and two gates, the AND and OR gates.
 
2.9	Timing	91
S1  S0
S1  S0
 

D0 D1 D2
Out
D3
 







Figure 2.73 4:1 multiplexer propagation delays: (a) two-level logic, (b) tristate
 


 




(a)
 
Out
tpd_sy = tpd_INV + tpd_AND3 + tpd_OR4
= 30 ps + 80 ps + 90 ps
= 200 ps
tpd_dy = tpd_AND3 + tpd_OR4
= 170 ps
 




(b)
 

tpd_sy = tpd_INV + tpd_AND2 + tpd_TRI_sy
= 30 ps + 60 ps + 35 ps
= 125 ps
tpd_dy = tpd_TRI_ay
= 50 ps
 


 
S0
D0	A
B

D1
C
Y
D2	Y
C

D3
 








AB
00	01

0
 




Y




11	10
 

 
tpd_s0y = tpd_TRI_sy + tpd_TRI_ay = 85 ps
tpd_dy = 2 tpd_TRI_ay = 100 ps
Figure 2.74 4:1 multiplexer propagation delays: hierarchical using 2:1 multiplexers
 
1

Y = AB + BC

Figure 2.75 Circuit with a glitch
 

As B transitions from 1 to 0, n2 (on the short path) falls before n1 (on the critical path) can rise. Until n1 rises, the two inputs to the OR gate are 0, and the output Y drops to 0. When n1 eventually rises, Y returns to 1. As shown in the timing diagram of Figure 2.76, Y starts at 1 and ends at 1 but momentarily glitches to 0.
 
92	CHAPTER TWO
 
Combinational Logic Design
 


 

A = 0
B = 1  0

C = 1
 
Critical Path


Y = 1  0  1
 

Short Path

Figure 2.76 Timing of a glitch










As long as we wait for the propagation delay to elapse before we depend on the output, glitches are not a problem, because the output eventually settles to the right answer.
If we choose to, we can avoid this glitch by adding another gate to the implementation. This is easiest to understand in terms of the K-map. Figure 2.77 shows how an input transition on B from ABC = 011 to ABC = 001 moves from one prime implicant circle to another. The tran- sition across the boundary of two prime implicants in the K-map indi- cates a possible glitch.
As we saw from the timing diagram in Figure 2.76, if the circuitry implementing one of the prime implicants turns off before the circuitry of the other prime implicant can turn on, there is a glitch. To fix this, we add another circle that covers that prime implicant boundary, as shown in Figure 2.78. You might recognize this as the consensus theorem, where the added term, AC , is the consensus or redundant term.


Y


Figure 2.77 Input change crosses implicant boundary


Y = AB + BC
 
2.10	Summary	93
 
Y AB C
 
00	01
 
11	10
 
Figure 2.78 K-map without glitch
AC	Y = AB + BC + AC
 




A = 0
B = 1  0

C = 1
 





Y = 1
 






Figure 2.79 Circuit without glitch
 





Figure 2.79 shows the glitch-proof circuit. The added AND gate is highlighted in blue. Now, a transition on B when A = 0 and C = 1 does not cause a glitch on the output because the blue AND gate outputs 1 throughout the transition.
In general, a glitch can occur when a change in a single variable crosses the boundary between two prime implicants in a K-map. We can eliminate the glitch by adding redundant implicants to the K-map to cover these boundaries. This, of course, comes at the cost of extra hardware.
However, simultaneous transitions on multiple inputs can also cause glitches. These glitches cannot be fixed by adding hardware. Because the vast majority of interesting systems have simultaneous (or near- simultaneous) transitions on multiple inputs, glitches are a fact of life in most circuits. Although we have shown how to eliminate one kind of glitch, the point of discussing glitches is not to eliminate them but to be aware that they exist. This is especially important when looking at tim- ing diagrams on a simulator or oscilloscope.

2.10 SUMMARY
A digital circuit is a module with discrete-valued inputs and outputs and a specification describing the function and timing of the module. This chapter has focused on combinational circuits, whose outputs depend only on the current values of the inputs.
 
94	CHAPTER TWO
 
Combinational Logic Design
 


The function of a combinational circuit can be given by a truth table or a Boolean equation. The Boolean equation for any truth table can be obtained systematically using sum-of-products (SOP) or product-of- sums (POS) form. In sum-of-products form, the function is written as the sum (OR) of one or more implicants. Implicants are the product (AND) of literals. Literals are the true or complementary forms of the input variables.
Boolean equations can be simplified using the rules of Boolean alge- bra. In particular, they can be simplified into minimal sum-of-products form by combining implicants that differ only in the true and comple-
mentary forms of one of the literals: PA + PA = P. Karnaugh maps
are a visual tool for minimizing functions of up to four variables. With
practice, designers can usually simplify functions of a few variables by inspection. Computer-aided design tools are used for more complicated functions; such methods and tools are discussed in Chapter 4.
Logic gates are connected to create combinational circuits that per- form the desired function. Any function in sum-of-products form can be built using two-level logic: NOT gates form the complements of the inputs, AND gates form the products, and OR gates form the sum. Depending on the function and the building blocks available, multilevel logic implementations with various types of gates may be more efficient. For example, CMOS circuits favor NAND and NOR gates because these gates can be built directly from CMOS transistors without requir- ing extra NOT gates. When using NAND and NOR gates, bubble push- ing is helpful to keep track of the inversions.
Logic gates are combined to produce larger circuits, such as multi- plexers, decoders, and priority circuits. A multiplexer chooses one of the data inputs based on the select input. A decoder sets one of the outputs HIGH according to the inputs. A priority circuit produces an output indicating the highest priority input. These circuits are all examples of combinational building blocks. Chapter 5 will introduce more building blocks, including other arithmetic circuits. These building blocks will be used extensively to build a microprocessor in Chapter 7.
The timing specification of a combinational circuit consists of the propagation and contamination delays through the circuit. These indi- cate the longest and shortest times between an input change and the consequent output change. Calculating the propagation delay of a cir- cuit involves identifying the critical path through the circuit, then adding up the propagation delays of each element along that path. There are many different ways to implement complicated combinational circuits; these ways offer trade-offs between speed and cost.
The next chapter will move to sequential circuits, whose outputs depend on current as well as previous values of the inputs. In other words, sequential circuits have memory of the past.
 


Exercises	95

Exercises
Exercise 2.1 Write a Boolean equation in sum-of-products canonical form for each of the truth tables in Figure 2.80.

(a)				(b)					(c)					(d)						(e)	
A	B	Y		A	B	C	Y		A	B	C	Y		A	B	C	D	Y		A	B	C	D	Y
0	0	1		0	0	0	1		0	0	0	1		0	0	0	0	1		0	0	0	0	1
0	1	0		0	0	1	0		0	0	1	0		0	0	0	1	1		0	0	0	1	0
1	0	1		0	1	0	0		0	1	0	1		0	0	1	0	1		0	0	1	0	0
1	1	1		0	1	1	0		0	1	1	0		0	0	1	1	1		0	0	1	1	1
				1	0	0	0		1	0	0	1		0	1	0	0	0		0	1	0	0	0
				1	0	1	0		1	0	1	1		0	1	0	1	0		0	1	0	1	1
				1	1	0	0		1	1	0	0		0	1	1	0	0		0	1	1	0	1
				1	1	1	1		1	1	1	1		0	1	1	1	0		0	1	1	1	0
	1	0	0	0	1		1	0	0	0	0
	1	0	0	1	0		1	0	0	1	1
	1	0	1	0	1		1	0	1	0	1
	1	0	1	1	0		1	0	1	1	0
	1	1	0	0	0		1	1	0	0	1
	1	1	0	1	0		1	1	0	1	0
	1	1	1	0	1		1	1	1	0	0
	1	1	1	1	0		1	1	1	1	1
Figure 2.80 Truth tables for Exercises 2.1, 2.3, and 2.41


Exercise 2.2 Write a Boolean equation in sum-of-products canonical form for each of the truth tables in Figure 2.81.

(a)				(b)					(c)					(d)						(e)	
A	B	Y		A	B	C	Y		A	B	C	Y		A	B	C	D	Y		A	B	C	D	Y
0	0	0		0	0	0	0		0	0	0	0		0	0	0	0	1		0	0	0	0	0
0	1	1		0	0	1	1		0	0	1	1		0	0	0	1	0		0	0	0	1	0
1	0	1		0	1	0	1		0	1	0	0		0	0	1	0	1		0	0	1	0	0
1	1	1		0	1	1	1		0	1	1	0		0	0	1	1	1		0	0	1	1	1
				1	0	0	1		1	0	0	0		0	1	0	0	0		0	1	0	0	0
				1	0	1	0		1	0	1	0		0	1	0	1	0		0	1	0	1	0
				1	1	0	1		1	1	0	1		0	1	1	0	1		0	1	1	0	1
				1	1	1	0		1	1	1	1		0	1	1	1	1		0	1	1	1	1
	1	0	0	0	1		1	0	0	0	1
	1	0	0	1	0		1	0	0	1	1
	1	0	1	0	1		1	0	1	0	1
	1	0	1	1	0		1	0	1	1	1
	1	1	0	0	0		1	1	0	0	0
	1	1	0	1	0		1	1	0	1	0
	1	1	1	0	0		1	1	1	0	0
	1	1	1	1	0		1	1	1	1	0
Figure 2.81 Truth tables for Exercises 2.2 and 2.4
 


 

96	CHAPTER TWO
 

Combinational Logic Design
 


Exercise 2.3 Write a Boolean equation in product-of-sums canonical form for the truth tables in Figure 2.80.

Exercise 2.4 Write a Boolean equation in product-of-sums canonical form for the truth tables in Figure 2.81.

Exercise 2.5 Minimize each of the Boolean equations from Exercise 2.1.

Exercise 2.6 Minimize each of the Boolean equations from Exercise 2.2.

Exercise 2.7 Sketch a reasonably simple combinational circuit implementing each of the functions from Exercise 2.5. Reasonably simple means that you are not wasteful of gates, but you don’t waste vast amounts of time checking every possible implementation of the circuit either.

Exercise 2.8 Sketch a reasonably simple combinational circuit implementing each of the functions from Exercise 2.6.

Exercise 2.9 Repeat Exercise 2.7 using only NOT gates and AND and OR gates.

Exercise 2.10 Repeat Exercise 2.8 using only NOT gates and AND and OR gates.

Exercise 2.11 Repeat Exercise 2.7 using only NOT gates and NAND and NOR gates.

Exercise 2.12 Repeat Exercise 2.8 using only NOT gates and NAND and NOR gates.

Exercise 2.13 Simplify the following Boolean equations using Boolean theorems. Check for correctness using a truth table or K-map.
(a)	Y = AC + ABC
(b)	Y = AB + ABC + (A + C)
(c)	Y = ABCD + ABC + ABCD + ABD + ABCD + BCD + A
Exercise 2.14 Simplify the following Boolean equations using Boolean theorems. Check for correctness using a truth table or K-map.
(a)	Y = ABC + ABC

(b)	Y = ABC + AB
(c)	Y = ABCD + ABCD + (A + B + C + D)
 


Exercises	97


Exercise 2.15 Sketch a reasonably simple combinational circuit implementing each of the functions from Exercise 2.13.

Exercise 2.16 Sketch a reasonably simple combinational circuit implementing each of the functions from Exercise 2.14.

Exercise 2.17 Simplify each of the following Boolean equations. Sketch a reasonably simple combinational circuit implementing the simplified equation.
(a)	Y = BC + ABC + BC
(b)	Y = A + AB + AB + A + B
(c)	Y = ABC + ABD + ABE + ACD + ACE + (A + D + E) + BCD
+ BCE + BDE + CDE
Exercise 2.18 Simplify each of the following Boolean equations. Sketch a reasonably simple combinational circuit implementing the simplified equation.
(a)	Y = ABC + BC + BC

(b)	Y = (A + B + C)D + AD + B
(c)	Y = ABCD + ABCD + (B + D)E 
Exercise 2.19 Give an example of a truth table requiring between 3 billion and 5 billion rows that can be constructed using fewer than 40 (but at least 1) two- input gates.

Exercise 2.20 Give an example of a circuit with a cyclic path that is nevertheless combinational.

Exercise 2.21 Alyssa P. Hacker says that any Boolean function can be written in minimal sum-of-products form as the sum of all of the prime implicants of the function. Ben Bitdiddle says that there are some functions whose minimal equation does not involve all of the prime implicants. Explain why Alyssa is right or provide a counterexample demonstrating Ben’s point.

Exercise 2.22 Prove that the following theorems are true using perfect induction. You need not prove their duals.
(a)	The idempotency theorem (T3)
(b)	The distributivity theorem (T8)
(c)	The combining theorem (T10)
 


 

98	CHAPTER TWO
 

Combinational Logic Design
 


Exercise 2.23 Prove De Morgan’s Theorem (T12) for three variables, A, B, and
C, using perfect induction.

Exercise 2.24 Write Boolean equations for the circuit in Figure 2.82. You need not minimize the equations.



A	B	C	D
Y	Z
Figure 2.82 Circuit schematic for Exercise 2.24


Exercise 2.25 Minimize the Boolean equations from Exercise 2.24 and sketch an improved circuit with the same function.

Exercise 2.26 Using De Morgan equivalent gates and bubble pushing methods, redraw the circuit in Figure 2.83 so that you can find the Boolean equation by inspection. Write the Boolean equation.



A B
C D E
Figure 2.83 Circuit schematic for Exercises 2.26 and 2.43
 


Exercises	99
Exercise 2.27 Repeat Exercise 2.26 for the circuit in Figure 2.84.

A B C
D
Y
E

F G
Figure 2.84 Circuit schematic for Exercises 2.27 and 2.44

Exercise 2.28 Find a minimal Boolean equation for the function in Figure 2.85. Remember to take advantage of the don’t care entries.

A	B	C	D	Y
0	0	0	0	X
0	0	0	1	X
0	0	1	0	X
0	0	1	1	0
0	1	0	0	0
0	1	0	1	X
0	1	1	0	0
0	1	1	1	X
1	0	0	0	1
1	0	0	1	0
1	0	1	0	X
1	0	1	1	1
1	1	0	0	1
1	1	0	1	1
1	1	1	0	X
1	1	1	1	1
Figure 2.85 Truth table for Exercise 2.28



Exercise 2.29 Sketch a circuit for the function from Exercise 2.28.

Exercise 2.30 Does your circuit from Exercise 2.29 have any potential glitches when one of the inputs changes? If not, explain why not. If so, show how to modify the circuit to eliminate the glitches.

Exercise 2.31 Find a minimal Boolean equation for the function in Figure 2.86. Remember to take advantage of the don’t care entries.
 


 

100
 

CHAPTER TWO
 

Combinational Logic Design
 



A	B	C	D	Y
0	0	0	0	0
0	0	0	1	1
0	0	1	0	X
0	0	1	1	X
0	1	0	0	0
0	1	0	1	X
0	1	1	0	X
0	1	1	1	X
1	0	0	0	1
1	0	0	1	0
1	0	1	0	0
1	0	1	1	1
1	1	0	0	0
1	1	0	1	1
1	1	1	0	X
1	1	1	1	1
Figure 2.86 Truth table for Exercise 2.31


Exercise 2.32 Sketch a circuit for the function from Exercise 2.31.

Exercise 2.33 Ben Bitdiddle will enjoy his picnic on sunny days that have no ants. He will also enjoy his picnic any day he sees a hummingbird, as well as on days where there are ants and ladybugs. Write a Boolean equation for his
enjoyment (E) in terms of sun (S), ants (A), hummingbirds (H), and ladybugs (L).

Exercise 2.34 Complete the design of the seven-segment decoder segments Sc
through Sg (see Example 2.10):
(a)	Derive Boolean equations for the outputs Sc through Sg assuming that inputs greater than 9 must produce blank (0) outputs.
(b)	Derive Boolean equations for the outputs Sc through Sg assuming that inputs greater than 9 are don’t cares.
(c)	Sketch a reasonably simple gate-level implementation of part (b). Multiple outputs can share gates where appropriate.

Exercise 2.35 A circuit has four inputs and two outputs. The inputs A3:0 represent a number from 0 to 15. Output P should be TRUE if the number is prime (0 and 1 are not prime, but 2, 3, 5, and so on, are prime). Output D should be TRUE if the number is divisible by 3. Give simplified Boolean equations for each output and sketch a circuit.

Exercise 2.36 A priority encoder has 2N inputs. It produces an N-bit binary output indicating the most significant bit of the input that is TRUE or 0 if none
 


Exercises	101


of the inputs are TRUE. It also produces an output NONE that is TRUE if none of the inputs are TRUE. Design an eight-input priority encoder with inputs A7:0 and outputs Y2.0 and NONE. For example, if the input is 00100000, the output Y should be 101 and NONE should be 0. Give a simplified Boolean equation for each output, and sketch a schematic.

Exercise 2.37 Design a modified priority encoder (see Exercise 2.36) that receives an 8-bit input, A7:0, and produces two 3-bit outputs, Y2:0 and Z2:0.
Y indicates the most significant bit of the input that is TRUE. Z indicates the
second most significant bit of the input that is TRUE. Y should be 0 if none of the inputs are TRUE. Z should be 0 if no more than one of the inputs is TRUE. Give a simplified Boolean equation for each output and sketch a schematic.

Exercise 2.38 An M-bit thermometer code for the number k consists of k 1’s in the least significant bit positions and M – k 0’s in all the more significant bit positions. A binary-to-thermometer code converter has N inputs and 2N–1 outputs. It produces a 2N–1 bit thermometer code for the number specified
by the input. For example, if the input is 110, the output should be 0111111. Design a 3:7 binary-to-thermometer code converter. Give a simplified Boolean equation for each output and sketch a schematic.

Exercise 2.39 Write a minimized Boolean equation for the function performed by the circuit in Figure 2.87.




Y

Figure 2.87 Multiplexer circuit for Exercise 2.39


Exercise 2.40 Write a minimized Boolean equation for the function performed by the circuit in Figure 2.88.


C, D	A, B

Y


Figure 2.88 Multiplexer circuit for Exercise 2.40
 


 

102
 

CHAPTER TWO
 

Combinational Logic Design
 


Exercise 2.41 Implement the function from Figure 2.80(b) using
(a)	an 8:1 multiplexer
(b)	a 4:1 multiplexer and one inverter
(c)	a 2:1 multiplexer and two other logic gates

Exercise 2.42 Implement the function from Exercise 2.17(a) using
(a)	an 8:1 multiplexer
(b)	a 4:1 multiplexer and no other gates
(c)	a 2:1 multiplexer, one OR gate, and an inverter

Exercise 2.43 Determine the propagation delay and contamination delay of the circuit in Figure 2.83. Use the gate delays given in Table 2.8.

Exercise 2.44 Determine the propagation delay and contamination delay of the circuit in Figure 2.84. Use the gate delays given in Table 2.8.


Table 2.8 Gate delays for Exercises 2.43–2.45 and 2.47–2.48

Gate	tpd (ps)	tcd (ps)
NOT	15	10
2-input NAND	20	15
3-input NAND	30	25
2-input NOR	30	25
3-input NOR	45	35
2-input AND	30	25
3-input AND	40	30
2-input OR	40	30
3-input OR	55	45
2-input XOR	60	40


Exercise 2.45 Sketch a schematic for a fast 3:8 decoder. Suppose gate delays are given in Table 2.8 (and only the gates in that table are available). Design your decoder to have the shortest possible critical path and indicate what that path is. What are its propagation delay and contamination delay?
 


Exercises	103


Exercise 2.46 Design an 8:1 multiplexer with the shortest possible delay from the data inputs to the output. You may use any of the gates from Table 2.7 on page 90. Sketch a schematic. Using the gate delays from the table, determine this delay.

Exercise 2.47 Redesign the circuit from Exercise 2.35 to be as fast as possible. Use only the gates from Table 2.8. Sketch the new circuit and indicate the critical path. What are its propagation delay and contamination delay?

Exercise 2.48 Redesign the priority encoder from Exercise 2.36 to be as fast as possible. You may use any of the gates from Table 2.8. Sketch the new circuit and indicate the critical path. What are its propagation delay and contamination delay?

Exercise 2.49 Another way to think about transistor-level design (see Section 1.7) is to use De Morgan’s theorem to consider the pull-up and pull-down networks. Design the pull-down network of a transistor-level gate directly from the equations below. Then, apply De Morgan’s theorem to the equations and draw the pull-up network using that rewritten equation. Also, state the numbers of transistors used. Do not forget to draw (and count) the inverters needed to complement the inputs, if needed.
(a)	W = A + BC + CD
(b)	X = A(B + C + D) + AD
(c)	Y = A(BC + BC) + ABC
Exercise 2.50 Repeat Exercise 2.49 for the equations below.
(a)	W = (A + B)(C + D)
(b)	X = AB(C + D) + AD
(c)	Y = A(B + CD) + ABCD
 


 

104
 

CHAPTER TWO
 

Combinational Logic Design
 

Interview Questions
The following exercises present questions that have been asked at interviews for digital design jobs.

Question 2.1 Sketch a schematic for the two-input XOR function, using only NAND gates. How few can you use?

Question 2.2 Design a circuit that will tell whether a given month has 31 days in it. The month is specified by a 4-bit input A3:0. For example, if the inputs are 0001, the month is January, and if the inputs are 1100, the month is December. The circuit output Y should be HIGH only when the month specified by the inputs has 31 days in it. Write the simplified equation, and draw the circuit diagram using a minimum number of gates. (Hint: Remember to take advantage of don’t cares.)

Question 2.3 What is a tristate buffer? How and why is it used?

Question 2.4 A gate or set of gates is universal if it can be used to construct any Boolean function. For example, the set {AND, OR, NOT} is universal.
(a)	Is an AND gate by itself universal? Why or why not?
(b)	Is the set {OR, NOT} universal? Why or why not?
(c)	Is a NAND gate by itself universal? Why or why not?

Question 2.5 Explain why a circuit’s contamination delay might be less than (instead of equal to) its propagation delay.
 
 
 
Sequential Logic Design	3
 






3.1	INTRODUCTION
In the last chapter, we showed how to analyze and design combinational logic. The output of combinational logic depends only on current input values. Given a specification in the form of a truth table or Boolean equation, we can create an optimized circuit to meet the specification.
In this chapter, we will analyze and design sequential logic. The outputs of sequential logic depend on both current and prior input values. Hence, sequential logic has memory. Sequential logic might explicitly remember certain previous inputs or it might distill the prior inputs into a smaller amount of information called the state of the system. The state of a digital sequential circuit is a set of bits called state variables that contain all the information about the past necessary to explain the future behavior of the circuit.
The chapter begins by studying latches and flip-flops, which are simple sequential circuits that store one bit of state. In general, sequen- tial circuits are complicated to analyze. To simplify design, we disci- pline ourselves to build only synchronous sequential circuits consisting of combinational logic and banks of flip-flops containing the state of the circuit. The chapter describes finite state machines, which are an easy way to design sequential circuits. Finally, we analyze the speed of sequential circuits and discuss parallelism as a way to increase speed.

3.2	LATCHES AND FLIP-FLOPS
The fundamental building block of memory is a bistable element, an ele- ment with two stable states. Figure 3.1(a) shows a simple bistable ele- ment consisting of a pair of inverters connected in a loop. Figure 3.1(b) shows the same circuit redrawn to emphasize the symmetry. The invert- ers are cross-coupled, meaning that the input of I1 is the output of I2 and vice versa. The circuit has no inputs, but it does have two outputs,

Digital Design and Computer Architecture, RISC-V Edition. DOI: 10.1016/B978-0-12-820064-3.00003-9
Copyright © 2022 Elsevier Inc. All rights reserved.
 



3.1	Introduction
3.2	Latches and Flip-Flops
3.3	Synchronous Logic Design
3.4	Finite State Machines
3.5	Timing of Sequential Logic
3.6	Parallelism
3.7	Summary
Exercises
Interview Questions



Application	>”hello
Software	world!”
Operating Systems

Architecture
Micro- architecture
Logic	
Digital Circuits
Analog	
Circuits
Devices	 

Physics


107
 
108
 

CHAPTER THREE
 
Sequential Logic Design
 


 


Figure 3.1 Cross-coupled inverter pair
 





(a)
 
Q


Q
(b)
 



Q and Q. Analyzing this circuit is different from analyzing a combina- tional circuit because it is cyclic: Q depends on Q, and Q depends on Q.
Consider the two cases, Q is 0 or Q is 1. Working through the consequences of each case, we have:
	Case I: Q = 0
As shown in Figure 3.2(a), I2 receives a FALSE input, Q, so it pro- duces a TRUE output on Q. I1 receives a TRUE input, Q, so it pro- duces a FALSE output on Q. This is consistent with the original
assumption that Q = 0, so the case is said to be stable.
	Case II: Q = 1
As shown in Figure 3.2(b), I2 receives a TRUE input and produces a FALSE output on Q. I1 receives a FALSE input and produces a TRUE output on Q. This is again stable.

Because the cross-coupled inverters have two stable states, Q = 0 and Q = 1, the circuit is said to be bistable. A subtle point is that the circuit has a third possible state with both outputs approximately half- way between 0 and 1. This is called a metastable state, which will be discussed in Section 3.5.4.
An element with N stable states conveys log2N bits of informa- tion, so a bistable element stores one bit. The state of the cross-coupled inverters is contained in one binary state variable, Q. The value of Q tells us everything about the past that is necessary to explain the future behavior of the circuit. Specifically, if Q = 0, it will remain 0 forever, and if Q = 1, it will remain 1 forever. The circuit does have another node, Q, but Q does not contain any additional information because if Q is


 


Figure 3.2 Bistable operation of cross-coupled inverters
 

1

0

(a)
 
Q	0	Q

Q	1	Q
(b)
 
3.2 Latches and Flip-Flops	109



known, Q is also known. On the other hand, Q is also an acceptable choice for the state variable.
When power is first applied to a sequential circuit, the initial state is unknown and usually unpredictable. It may differ each time the circuit is turned on.
Although the cross-coupled inverters can store a bit of information, they are not practical because the user has no inputs to control the state. However, other bistable elements, such as latches and flip-flops, provide inputs to control the value of the state variable. The remainder of this section considers these circuits.

 
3.2.1	SR Latch
One of the simplest sequential circuits is the SR latch, which is composed of two cross-coupled NOR gates, as shown in Figure 3.3. The latch has two inputs, S and R, and two outputs, Q and Q. The SR latch is similar to the cross-coupled inverters, but its state can be controlled through the S and R inputs, which set and reset the output Q.
A good way to understand an unfamiliar circuit is to work out its truth table, so that is where we begin. Recall that a NOR gate produces a FALSE output when either input is TRUE. Consider the four possible combinations of R and S.
	Case I: R = 1, S = 0
N1 sees at least one TRUE input, R, so it produces a FALSE output on
Q. N2 sees both Q and S FALSE, so it produces a TRUE output on Q.
	Case II: R = 0, S = 1
 	 
N1 receives inputs of 0 and Q. Because we don’t yet know Q, we can’t determine the output Q. N2 receives at least one TRUE input, S, so it produces a FALSE output on Q. Now we can revisit N1, knowing that both inputs are FALSE, so the output Q is TRUE.
	Case III: R = 1, S = 1
N1 and N2 both see at least one TRUE input (R or S), so each produces a FALSE output. Hence, Q and Q are both FALSE.
	Case IV: R = 0, S = 0
N1 receives inputs of 0 and Q. Because we don’t yet know Q, we can’t determine the output. N2 receives inputs of 0 and Q. Because we don’t yet know Q, we can’t determine the output. Now we are
 


R



S
Figure 3.3 SR latch schematic
 
110
 

CHAPTER THREE
 
Sequential Logic Design
 


 


Figure 3.4 Bistable states of SR latch
 
R



S
(a)
 
R



S
(b)
 

 



















 





Figure 3.5 SR latch truth table



Figure 3.6 SR latch symbol
 
stuck. This is reminiscent of the cross-coupled inverters. But we know that Q must either be 0 or 1, so we can solve the problem by checking what happens in each of these subcases.
   Case IVa: Q = 0
Because S and Q are FALSE, N2 produces a TRUE output on Q, as shown in Figure 3.4(a). Now N1 receives one TRUE input, Q, so its output, Q, is FALSE, just as we had assumed.
   Case IVb: Q = 1
 
Because Q is TRUE, N2 produces a FALSE output on Q, as shown in Figure 3.4(b). Now N1 receives two FALSE inputs, R and Q, so its output, Q, is TRUE, just as we had assumed.
Putting this all together, suppose that Q has some known prior value, which we will call Qprev, before we enter Case IV. Qprev is either 0 or 1 and represents the state of the system. When R and S are 0, Q will remember this old value, Qprev, and Q will be its com- plement, Qprev . This circuit has memory.
The truth table in Figure 3.5 summarizes these four cases. The inputs S and R stand for Set and Reset. To set a bit means to make it TRUE. To reset a bit means to make it FALSE. The outputs, Q and Q, are normally complementary. When R is asserted, Q is reset to 0 and Q does the oppo- site. When S is asserted, Q is set to 1 and Q does the opposite. When nei- ther input is asserted, Q remembers its old value, Qprev. Asserting both S and R simultaneously doesn’t make much sense because it means the latch should be set and reset at the same time, which is impossible. The poor confused circuit responds by making both outputs 0.
The SR latch is represented by the symbol in Figure 3.6. Using the symbol is an application of abstraction and modularity. There are vari- ous ways to build an SR latch, such as using different logic gates or tran- sistors. Nevertheless, any circuit element with the relationship specified by the truth table in Figure 3.5 and the symbol in Figure 3.6 is called an SR latch.
Like the cross-coupled inverters, the SR latch is a bistable element with one bit of state stored in Q. However, the state can be controlled through the S and R inputs. When R is asserted, the state is reset to 0. When S is asserted, the state is set to 1. When neither is asserted, the
 
3.2 Latches and Flip-Flops	111


state retains its old value. Notice that the entire history of inputs can be accounted for by the single state variable Q. No matter what pattern of setting and resetting occurred in the past, all that is needed to predict the future behavior of the SR latch is whether it was most recently set or reset.

3.2.2	D Latch
The SR latch is awkward because it behaves strangely when both S and R are simultaneously asserted. Moreover, the S and R inputs conflate the issues of what and when. Asserting one of the inputs determines not only what the state should be but also when it should change. Designing circuits becomes easier when these questions of what and when are separated. The D latch in Figure 3.7(a) solves these prob- lems. It has two inputs. The data input, D, controls what the next state should be. The clock input, CLK, controls when the state should change.
Again, we analyze the latch by writing the truth table, given in Figure 3.7(b). For convenience, we first consider the internal nodes D, S, and R. If CLK = 0, both S and R are FALSE, regardless of the value of
D. If CLK = 1, one AND gate will produce TRUE and the other FALSE depending on the value of D. Given S and R, Q and Q are determined using Figure 3.5. Observe that when CLK = 0, Q remembers its old value, Qprev. When CLK = 1, Q = D. In all cases, Q is the complement of Q, as would seem logical. The D latch avoids the strange case of simul- taneously asserted R and S inputs.
Putting it all together, we see that the clock controls when data flows through the latch. When CLK = 1, the latch is transparent. The data at D flows through to Q as if the latch were just a buffer. When CLK = 0, the latch is opaque. It blocks the new data from flowing through to Q, and Q retains the old value. Hence, the D latch is some- times called a transparent latch or a level-sensitive latch. The D latch symbol is given in Figure 3.7(c).
The D latch updates its state continuously while CLK = 1. We shall see later in this chapter that it is useful to update the state only at a specific instant in time. The D flip-flop described in the next section does just that.

CLK

 

D
(a)
 


(b)
Figure 3.7 D latch: (a) schematic, (b) truth table, (c) symbol
 


(c)
 
112
 

CHAPTER THREE
 
Sequential Logic Design
 


 



CLK
D D	Q N1 L1 Q
 
CLK

CLK
D	Q Q
L2  Q Q
 

3.2.3	D FIip-Flop
A D flip-flop can be built from two back-to-back D latches controlled by complementary clocks, as shown in Figure 3.8(a). The first latch, L1, is called the leader. The second latch, L2, is called the follower, because
 

(a)





(b)
 
master	slave



(c)
 
it follows whatever L1 does.
The node between them is named N1. A symbol for the D flip-flop is given in Figure 3.8(b). When the Q output is not needed, the symbol is often condensed, as in Figure 3.8(c).
When CLK = 0, the leader (latch L1) is transparent and the follower (L2) is opaque. Therefore, whatever value was at D propagates through to N1. When CLK = 1, the leader (L1) goes opaque and the follower (L2) becomes transparent. The value at N1 propagates through to Q,
 
Figure 3.8 D flip-flop:
(a)	schematic, (b) symbol,
(c) condensed symbol
 
but N1 is cut off from D. Hence, whatever value was at D immediately before the clock rises from 0 to 1 gets copied to Q immediately after the clock rises. At all other times, Q retains its old value, because there is always an opaque latch blocking the path between D and Q.
In other words, a D flip-flop copies D to Q on the rising edge of the clock and remembers its state at all other times. Reread this defini- tion until you have it memorized; one of the most common problems for beginning digital designers is to forget what a flip-flop does. The rising edge of the clock is often just called the clock edge for brevity. The D input specifies what the new state will be. The clock edge indicates when the state should be updated.
A D flip-flop is also known as an edge-triggered flip-flop or a pos- itive edge-triggered flip-flop. The triangle in the symbols denotes an edge-triggered clock input. The Q output is often omitted when it is not needed.
 

 
Example 3.1 FLIP-FLOP TRANSISTOR COUNT
How many transistors are needed to build the D flip-flop described in this section?
Solution A NAND or NOR gate uses four transistors. A NOT gate uses two transistors. An AND gate is built from a NAND and a NOT, so it uses six tran- sistors. The SR latch uses two NOR gates, or eight transistors. The D latch uses an SR latch, two AND gates, and a NOT gate, or 22 transistors. The D flip-flop uses two D latches and a NOT gate, or 46 transistors. Section 3.2.7 describes a more efficient CMOS implementation, using transmission gates.

3.2.4	Register
An N-bit register is a bank of N flip-flops that share a common CLK input so that all bits of the register are updated at the same time. Registers are the key building block of most sequential circuits.
 
3.2 Latches and Flip-Flops	113
CLK
D3	Q3
 
D2	Q2
D1	Q1
 
Figure 3.9 A 4-bit register:
(a) schematic and (b) symbol
 
D0
(a)
 


CLK
Q0	4	4
3:0
(b)
 
Q3:0
 

Figure 3.9 shows the schematic and symbol for a four-bit register with inputs D3:0 and outputs Q3:0. D3:0 and Q3:0 are both 4-bit busses.

3.2.5	Enabled Flip-Flop
An enabled flip-flop adds another input called EN or ENABLE to deter- mine whether data is loaded on the clock edge. When EN is TRUE, the enabled flip-flop behaves like an ordinary D flip-flop. When EN is FALSE, the enabled flip-flop ignores the clock and retains its state. Enabled flip-flops are useful when we wish to load a new value into a flip-flop only some of the time, rather than on every clock edge.
Figure 3.10 shows two ways to construct an enabled flip-flop from a D flip-flop and an extra gate. In Figure 3.10(a), an input multiplexer passes the value D if EN is TRUE or recycles the old state from Q if EN is FALSE. In Figure 3.10(b), the clock is gated. If EN is TRUE, the CLK input to the flip-flop toggles normally. If EN is FALSE, the CLK input is also FALSE and the flip-flop retains its old value. Notice that EN must

CLK EN

 
EN	CLK



D
 


Q	D  	Q
 


Figure 3.10 Enabled flip-flop: (a, b) schematics, (c) symbol
 

 
(a)
 
(b)
 
(c)
 
114
 

CHAPTER THREE
 
Sequential Logic Design
 


not change while CLK = 1 lest the flip-flop see a clock glitch (switch at an incorrect time). Generally, performing logic on the clock is a bad idea. Clock gating delays the clock and can cause timing errors, as we will see in Section 3.5.3, so do it only if you are sure you know what you are doing. The symbol for an enabled flip-flop is given in Figure 3.10(c).

 











	D  RESET

(a)

(b)	(c)
 









CLK


Q
 
3.2.6	Resettable Flip-Flop
A resettable flip-flop adds another input, called RESET. When RESET is FALSE, the resettable flip-flop behaves like an ordinary D flip-flop. When RESET is TRUE, the resettable flip-flop ignores D and resets the output to 0. Resettable flip-flops are useful when we want to force a known state (i.e., 0) into all the flip-flops in a system when we first turn it on.
Such flip-flops may be synchronously or asynchronously resettable. Synchronously resettable flip-flops reset themselves only on the rising edge of CLK. Asynchronously resettable flip-flops reset themselves as soon as RESET becomes TRUE, independent of CLK.
Figure 3.11(a) shows how to construct a synchronously resettable flip-flop from an ordinary D flip-flop and an AND gate. When the signal RESET is FALSE, the AND gate forces a 0 into the input of the flip-flop. When RESET is TRUE, the AND gate passes D to the flip-flop. In this example, RESET is an active low signal, meaning that the reset signal performs its function—in this case, resetting the flip-flop—when it is 0, not 1. By adding an inverter, the circuit could have accepted an active high reset signal instead. Figures 3.11(b) and 3.11(c) show symbols for
 
Figure 3.11 Synchronously resettable flip-flop: (a) schematic, (b, c) symbols
 
the resettable flip-flop with active high reset.
Asynchronously resettable flip-flops require modifying the internal structure of the flip-flop and are left to you to design in Exercise 3.13. Both synchronously and asynchronously resettable flip-flops are fre- quently available to the designer as standard components.
As you might imagine, settable flip-flops are also occasionally used. They load a 1 into the flip-flop when SET is asserted and they, too, come in synchronous and asynchronous flavors. Resettable and settable flip- flops may also have an enable input and may be grouped into N-bit registers.

3.2.7	Transistor-Level Latch and Flip-Flop Designs*
Example 3.1 showed that latches and flip-flops require a large num- ber of transistors when built from logic gates. But the fundamental role of a latch is to be transparent or opaque, much like a switch. Recall
 
3.2	Latches and Flip-Flops	115
 


from Section 1.7.7 that a transmission gate is an efficient way to build a CMOS switch, so we might expect that we could take advantage of transmission gates to reduce the transistor count.
A compact D latch can be constructed from a single transmission gate, as shown in Figure 3.12(a). When CLK = 1 and CLK = 0, the transmission gate is ON, so D flows to Q and the latch is transparent. When CLK = 0 and CLK = 1, the transmission gate is OFF, so Q is iso- lated from D and the latch is opaque. This latch suffers from two major limitations:

 Floating output node: When the latch is opaque, Q is not held at its value by any gates. Thus, Q is called a floating or dynamic node. After some time, noise and charge leakage may disturb the value of Q.
 No buffers: The lack of buffers has caused malfunctions on several commercial chips. A spike of noise that pulls D to a negative volt-
 


CLK

D	Q

CLK
(a)




D





(b)
 










Q






CLK
 
age can turn on the nMOS transistor, making the latch transpar- ent, even when CLK = 0. Likewise, a spike on D above VDD can turn on the pMOS transistor even when CLK = 0. And the trans- mission gate is symmetric, so it could be driven backward with noise on Q, affecting the input D. The general rule is that neither the input of a transmission gate nor the state node of a sequential circuit should ever be exposed to the outside world, where noise is likely.
Figure 3.12(b) shows a more robust 12-transistor D latch used on modern commercial chips. It is still built around a clocked transmission gate, but it adds inverters I1 and I2 to buffer the input and output. The state of the latch is held on node N1. Inverter I3 and the tristate buffer, T1, provide feedback to turn N1 into a static node. If a small amount of noise occurs on N1 while CLK = 0, T1 will drive N1 back to a valid logic value.
Figure 3.13 shows a D flip-flop constructed from two static latches controlled by CLK and CLK. Some redundant internal inverters have been removed, so the flip-flop requires only 20 transistors.
 
Figure 3.12 D latch schematic
 

 

CLK

D
 

CLK

Q
 




Figure 3.13 D flip-flop schematic
 


CLK	CLK
 
116
 

CHAPTER THREE
 
Sequential Logic Design
 

3.2.8 Putting It All Together
Latches and flip-flops are the fundamental building blocks of sequential circuits. Remember that a D latch is level-sensitive, whereas a D flip-flop is edge-triggered. The D latch is transparent when CLK = 1, allowing the input D to flow through to the output Q. The D flip-flop copies D to Q on the rising edge of CLK. At all other times, latches and flip-flops retain their old state. A register is a bank of several D flip-flops that share a common CLK signal.

Example 3.2 FLIP-FLOP AND LATCH COMPARISON
Ben Bitdiddle applies the D and CLK inputs shown in Figure 3.14 to a D latch and a D flip-flop. Help him determine the output, Q, of each device.
Solution Figure 3.15 shows the output waveforms, assuming a small delay for Q to respond to input changes. The arrows indicate the cause of an output change. The initial value of Q is unknown and could be 0 or 1, as indicated by the pair of horizontal lines. First, consider the latch. On the first rising edge of CLK, D = 0, so Q definitely becomes 0. Each time D changes while CLK = 1, Q also follows. When D changes while CLK = 0, D is ignored. Now, consider the flip-flop. On each rising edge of CLK, D is copied to Q. At all other times, Q retains its state.




Q (latch)

 
Q (flop)
 


Figure 3.14 Example waveforms
 


 
Figure 3.15 Solution waveforms
 
3.3	Synchronous Logic Design	117

3.3	SYNCHRONOUS LOGIC DESIGN
In general, sequential circuits include all circuits that are not combinational— that is, those whose output cannot be determined simply by looking at the current inputs. Some sequential circuits are just plain kooky. This section begins by examining some of those curious circuits. It then introduces the notion of synchronous sequential circuits and the dynamic discipline. By disciplining ourselves to synchronous sequential circuits, we can develop easy, systematic ways to analyze and design sequential systems.

3.3.1	Some Problematic Circuits


 
Example 3.3 ASTABLE CIRCUITS
Alyssa P. Hacker encounters three misbegotten inverters who have tied them- selves in a loop, as shown in Figure 3.16. The output of the third inverter is fed back to the first inverter. Each inverter has a propagation delay of 1 ns. Help Alyssa determine what the circuit does.
Solution Suppose that node X is initially 0. Then, Y = 1, Z = 0, and, hence, X = 1, which is inconsistent with our original assumption. The circuit has no stable states and is said to be unstable or astable. Figure 3.17 shows the behavior of the circuit. If X rises at time 0, Y will fall at 1 ns, Z will rise at 2 ns, and X will fall again at 3 ns. In turn, Y will rise at 4 ns, Z will fall at 5 ns, and X will rise again at 6 ns; then, the pattern will repeat. Each node oscillates between 0 and 1, with a period (repetition time) of 6 ns. This circuit is called a ring oscillator.
The period of the ring oscillator depends on the propagation delay of each inverter. This delay depends on how the inverter was manufactured, the power supply voltage, and even the temperature. Therefore, the ring oscillator period is difficult to accurately predict. In short, the ring oscillator is a sequential circuit with zero inputs and one output that changes periodically.
 


Figure 3.16 Three-inverter loop
 


Figure 3.17 Ring oscillator waveforms

0 1 2 3 4 5 6 7 8 Time (ns)


Example 3.4 RACE CONDITIONS
Ben Bitdiddle designed a new D latch that he claims is better than the one in Figure 3.7 because it uses fewer gates. He has written the truth table to find the output, Q, given the two inputs, D and CLK, and the old state of the
 
118
 

CHAPTER THREE
 
Sequential Logic Design
 



 
Q = CLK·D + CLK·Qprev

Figure 3.18 An improved (?)
D latch	Q




 





 
Figure 3.19 Latch waveforms illustrating race condition
 
latch, Qprev. Based on this truth table, he has derived Boolean equations. He obtains Qprev by feeding back the output, Q. His design is shown in Figure
3.18. Does his latch work correctly, independent of the delays of each gate?

Solution Figure 3.19 shows that the circuit has a race condition that causes it to fail when certain gates are slower than others. Suppose that CLK = D = 1. The latch is transparent and passes D through to make Q = 1. Now, CLK falls. The latch should remember its old value, keeping Q  = 1. However, sup- pose that the delay through the inverter from CLK to CLK is rather long compared with the delays of the AND and OR gates. Then, nodes N1 and Q may both fall before CLK rises. In such a case, N2 will never rise and Q becomes stuck at 0.
This is an example of asynchronous circuit design in which outputs are directly fed back to inputs. Asynchronous circuits are infamous for having race condi- tions where the behavior of the circuit depends on which of two paths through logic gates is fastest. One circuit may work, while a seemingly identical one built from gates with slightly different delays may not work. Or the circuit may work only at certain temperatures or voltages at which the delays are just right. These malfunctions are extremely difficult to track down.
 

 


3.3.2	Synchronous Sequential Circuits
The previous two examples contain loops called cyclic paths, in which outputs are fed directly back to inputs. They are sequential rather than combinational circuits. Combinational logic has no cyclic paths and no races. If inputs are applied to combinational logic, the outputs will always settle to the correct value within a propagation delay. However, sequential circuits with cyclic paths can have undesirable races or unsta- ble behavior. Analyzing such circuits for problems is time-consuming, and many bright people have made mistakes.
To avoid these problems, designers break the cyclic paths by insert- ing registers somewhere in the path. This transforms the circuit into a
 
3.3	Synchronous Logic Design	119
 


collection of combinational logic and registers. The registers contain the state of the system, which changes only at the clock edge, so we say the state is synchronized to the clock. If the clock is sufficiently slow, so that the inputs to all registers settle before the next clock edge, all races are eliminated. Adopting this discipline of always using registers in the feedback path leads us to the formal definition of a synchronous sequential circuit.
Recall that a circuit is defined by its input and output terminals and its functional and timing specifications. A sequential circuit has a finite set of discrete states {S0, S1, S2,…}. A synchronous sequential circuit has a clock input, whose rising edges indicate a sequence of times at which state transitions occur. We often use the terms current state and next state to distinguish the state of the system at the present from the state to which it will enter on the next clock edge. The func- tional specification details the next state and the value of each output for each possible combination of current state and input values. The timing specification consists of an upper bound, tpcq, and a lower bound, tccq, on the time from the rising edge of the clock until the out- put changes, as well as setup and hold times, tsetup and thold, that indi- cate when the inputs must be stable relative to the rising edge of the clock.
The rules of synchronous sequential circuit composition teach us that a circuit is a synchronous sequential circuit if it consists of intercon- nected circuit elements, such that
	Every circuit element is either a register or a combinational circuit
	At least one circuit element is a register
	All registers receive the same clock signal
	Every cyclic path contains at least one register
Sequential circuits that are not synchronous are called asynchronous.
A flip-flop is the simplest synchronous sequential circuit. It has one input, D, one clock, CLK, one output, Q, and two states,
{0, 1}. The functional specification for a flip-flop is that the next state is D and that the output, Q, is the current state, as shown in Figure 3.20.
We often call the current state variable S and the next state variable S . In this case, the prime after S indicates next state, not inversion. The timing of sequential circuits will be analyzed in Section 3.5.
Two other common types of synchronous sequential circuits are
 














































S  Next State
 












































CLK D	Q
 















































S
Current State
 
called finite state machines and pipelines. These will be covered later in this chapter.
 
Figure 3.20 Flip-flop current state and next state
 
120
 

CHAPTER THREE
 
Sequential Logic Design
 


CLK	CLK
 	 
(a)	(b)	(c)

 


Figure 3.21 Example circuits
 
CLK
 

(d)	(e)	(f)
 

CLK
 

CLK
 

CLK
 

CLK
 
 
(g)	(h)


Example 3.5 SYNCHRONOUS SEQUENTIAL CIRCUITS
Which of the circuits in Figure 3.21 are synchronous sequential circuits?

Solution Circuit (a) is combinational, not sequential, because it has no registers.
(b)	is a simple sequential circuit with no feedback. (c) is neither a combinational circuit nor a synchronous sequential circuit because it has a latch that is neither a register nor a combinational circuit. (d) and (e) are synchronous sequential logic; they are two forms of finite state machines, which are discussed in Section 3.4.
(f) is neither combinational nor synchronous sequential because it has a cyclic path from the output of the combinational logic back to the input of the same logic but no register in the path. (g) is synchronous sequential logic in the form of a pipeline, which we will study in Section 3.6. (h) is not, strictly speaking, a syn- chronous sequential circuit, because the second register receives a different clock signal than the first, delayed by two inverter delays.


3.3.3	Synchronous and Asynchronous Circuits
Asynchronous design in theory is more general than synchronous design because the timing of the system is not limited by clocked registers. Just as analog circuits are more general than digital circuits because analog circuits can use any voltage, asynchronous circuits are more general than synchronous circuits because they can use any kind of feedback. However, synchronous circuits have proved to be easier to design and use than asynchronous circuits, just as digital are easier than analog cir- cuits. Despite decades of research on asynchronous circuits, virtually all digital systems are essentially synchronous.
 
3.4	Finite State Machines	121


Of course, asynchronous circuits are occasionally necessary when communicating between systems with different clocks or when receiving inputs at arbitrary times, just as analog circuits are necessary when com- municating with the real world of continuous voltages. Furthermore, research in asynchronous circuits continues to generate interesting insights, some of which can also improve synchronous circuits.

3.4	FINITE STATE MACHINES
Synchronous sequential circuits can be drawn in the forms shown in Figure 3.22. These forms are called finite state machines (FSMs). They get their name because a circuit with k registers can be in one of a finite num- ber (2k) of unique states. An FSM has M inputs, N outputs, and k bits of state. It also receives a clock and, optionally, a reset signal. An FSM con- sists of two blocks of combinational logic, next state logic and output logic, and a register that stores the state. On each clock edge, the FSM advances to the next state, which was computed based on the current state and inputs. There are two general classes of finite state machines, characterized by their functional specifications. In Moore machines, the outputs depend only on the current state of the machine. In Mealy machines, the outputs depend on both the current state and the current inputs. Finite state machines provide a systematic way to design synchro- nous sequential circuits given a functional specification. This method will be explained in the remainder of this section, starting with an example.

3.4.1	FSM Design Example
To illustrate the design of FSMs, consider the problem of inventing a controller for a traffic light at a busy intersection on campus. Engineering students are moseying between their dorms and the labs on Academic

 


inputs
 
CLK
 


N
	 outputs
 

 
(a)




inputs	outputs
 

Figure 3.22 Finite state machines: (a) Moore machine,
(b) Mealy machine
 

(b)
 
122
 

CHAPTER THREE
 
Sequential Logic Design
 


Avenue. They are busy reading about FSMs in their favorite textbook and aren’t looking where they are going. Football players are hustling between the athletic fields and the dining hall on Bravado Boulevard. They are tossing the ball back and forth and aren’t looking where they are going either. Several serious injuries have already occurred at the intersection of these two roads, and the Dean of Students asks Ben Bitdiddle to install a traffic light before there are fatalities.
Ben decides to solve the problem with an FSM. He installs two traf- fic sensors, TA and TB, on Academic Ave. and Bravado Blvd., respec- tively. Each sensor indicates TRUE if students are present and FALSE if the street is empty. He also installs two traffic lights, LA and LB, to control traffic. Each light receives digital inputs specifying whether it should be green, yellow, or red. Hence, his FSM has two inputs, TA and TB, and two outputs, LA and LB. The intersection with lights and sensors is shown in Figure 3.23. Ben provides a clock with a 5-second period. On each clock tick (rising edge), the lights may change based on the traf- fic sensors. He also provides a reset button so that Physical Plant techni- cians can put the controller in a known initial state when they turn it on. Figure 3.24 shows a black box view of the state machine.
Ben’s next step is to sketch the state transition diagram, shown in Figure 3.25, to indicate all possible states of the system and the transi- tions between these states. When the system is reset, the lights are green on Academic Ave. and red on Bravado Blvd. Every 5 seconds, the control- ler examines the traffic pattern and decides what to do next. As long as





Figure 3.23 Campus map






CLK

 
Figure 3.24 Black box view of finite state machine
 
TA	LA

TB	LB
 

 
Reset
 
3.4 Finite State Machines	123







Figure 3.25 State transition diagram







traffic is present on Academic Ave., the lights do not change. When there is no longer traffic on Academic Ave., the light on Academic Ave. becomes yellow for 5 seconds before it turns red and Bravado Blvd.’s light turns green. Similarly, the Bravado Blvd. light remains green as long as traffic is present on the boulevard, then turns yellow and eventually red.
In a state transition diagram, circles represent states and arcs represent transitions between states. The transitions take place on the rising edge of the clock; we do not bother to show the clock on the diagram, because it is always present in a synchronous sequential circuit. Moreover, the clock simply controls when the transitions should occur, whereas the diagram indicates which transitions occur. The arc labeled Reset, pointing from outer space into state S0 indicates that the system should enter that state upon reset regardless of what previous state it was in. If a state has mul- tiple arcs leaving it, the arcs are labeled to show what input triggers each transition. For example, when in state S0, the system will remain in that state if TA is TRUE and move to S1 if TA is FALSE. If a state has a single arc leaving it, that transition always occurs regardless of the inputs. For example, when in state S1, the system will always move to S2 at the clock edge. The value that the outputs have while in a particular state are indi- cated in the state. For example, while in state S2, LA is red and LB is green. Ben rewrites the state transition diagram as a state transition table (Table 3.1), which indicates, for each state and input, what the next state, S , should be. Note that the table uses don’t care symbols (X) whenever the next state does not depend on a particular input. Also, note that Reset is omitted from the table. Instead, we use resettable flip-
flops that always go to state S0 on reset, independent of the inputs.
The state transition diagram is abstract in that it uses states labeled
{S0, S1, S2, S3} and outputs labeled {red, yellow, green}. To build a real circuit, the states and outputs must be assigned binary encodings. Ben chooses the simple encodings given in Tables 3.2 and 3.3. Each state and output is encoded with two bits: S1:0, LA1:0, and LB1:0.
 
124
 

CHAPTER THREE
 
Sequential Logic Design
 


 
Table 3.1 State transition table
 
Table 3.2 State encoding
 
Table 3.3 Output encoding
 

 	 


Ben updates the state transition table to use these binary encodings, as shown in Table 3.4. The revised state transition table is a truth table specifying the next state logic. It defines the next state, S , as a function of the current state, S, and the inputs.
From this table, it is straightforward to read off the Boolean equa- tions for the next state in sum-of-products form.

 
S1′ = S1S0 + S1 S0TB + S1S0TB
 

(3.1)
 
S0′ = S1 S0 TA + S1 S0 TB
The equations can be simplified, using Karnaugh maps. However, doing it by inspection is often easier. For example, the TB and TB terms
in the S1′ equation are clearly redundant. Thus, S1′ reduces to an XOR
operation. Equation 3.2 gives the simplified next state equations.

Table 3.4 State transition table with binary encodings

Current State
S1	S0	
TA	Inputs	
TB	Next State
S1′	S0′
0	0	0		X	0	1
0	0	1		X	0	0
0	1	X		X	1	0
1	0	X		0	1	1
1	0	X		1	1	0
1	1	X		X	0	0
 
3.4 Finite State Machines	125
Table 3.5 Output table
 









S1′
 








= S1 ⊕ S0
 











(3.2)
 
S0′ = S1S0TA + S1S0TB
Similarly, Ben writes an output table (Table 3.5) that indicates, for
each state, what the output should be in that state. Again, it is straightfor- ward to read off and simplify the Boolean equations for the outputs. For example, observe that LA1 is TRUE only on the rows where S1 is TRUE.
 
LA1 LA0 LB1 LB0
 
= S1
= S1S0
= S1
= S1S0
 


(3.3)
 
Finally, Ben sketches his Moore FSM in the form of Figure 3.22(a). First, he draws the 2-bit state register, as shown in Figure 3.26(a). On each clock edge, the state register copies the next state, S1 :0, to become the state S1:0. The state register receives a synchronous or asynchronous reset to initialize the FSM at startup. Then, he draws the next state logic, based on Equation 3.2, which computes the next state from the current state and inputs, as shown in Figure 3.26(b). Finally, he draws the output logic, based on Equation 3.3, which computes the outputs from the current state, as shown in Figure 3.26(c).
Figure 3.27 shows a timing diagram illustrating the traffic light con- troller going through a sequence of states. The diagram shows CLK, Reset, the inputs TA and TB, next state S , state S, and outputs LA and LB. Arrows indicate causality; for example, changing the state causes the out- puts to change, and changing the inputs causes the next state to change. Dashed lines indicate the rising edges of CLK when the state changes.
The clock has a 5-second period, so the traffic lights change at most once every 5 seconds. When the finite state machine is first turned on, its state is unknown, as indicated by the question marks. Therefore, the sys- tem should be reset to put it into a known state. In this timing diagram, S
 
126
 

CHAPTER THREE
 
Sequential Logic Design
 


CLK

 

S'1


S'0
 
CLK
S1

 
TA

S0	TB
 

   

 
 
Reset
state register
(a)
 

inputs
(b)
 

next state logic	state register
 

LA1

LA0

TA
LB1
TB
LB0

 
inputs
(c)
 
next state logic
 
state register
 
output logic
 
outputs
 
Figure 3.26 State machine circuit for traffic light controller




CLK

Reset TA TB S'1:0 S1:0 LA1:0 LB1:0

 
0	5	10	15	20	25	30	35	40	45

Figure 3.27 Timing diagram for traffic light controller
 
t (sec)
 
3.4 Finite State Machines	127


immediately resets to S0, indicating that asynchronously resettable flip- flops are being used. In state S0, light LA is green and light LB is red.
In this example, traffic arrives immediately on Academic Ave. Therefore, the controller remains in state S0, keeping LA green even though traffic arrives on Bravado Blvd. and starts waiting. After 15 seconds, the traffic on Academic Ave. has all passed through and TA falls. At the following clock edge, the controller moves to state S1, turning LA yellow. In another 5 seconds, the controller proceeds to state S2, in which LA turns red and LB turns green. The controller waits in state S2 until all traffic on Bravado Blvd. has passed through. It then proceeds to state S3, turning LB yellow. Five seconds later, the controller enters state S0, turning LB red and LA green. The process repeats.

3.4.2	State Encodings
In the previous example, the state and output encodings were selected arbitrarily. A different choice would have resulted in a different circuit. A nat- ural question is how to determine the encoding that produces the circuit with the fewest logic gates or the shortest propagation delay. Unfortunately, there is no simple way to find the best encoding except to try all possibil- ities, which is infeasible when the number of states is large. However, it is often possible to choose a good encoding by inspection so that related states or outputs share bits. Computer-aided design (CAD) tools are also good at searching the set of possible encodings and selecting a reasonable one.
One important decision in state encoding is the choice between binary encoding and one-hot encoding. With binary encoding, as was used in the traffic light controller example, each state is represented as a binary number. Because K binary numbers can be represented by log2K bits, a system with K states needs only log2K bits of state.
In one-hot encoding, a separate bit of state is used for each state. It is called one-hot because only one bit is “hot” or TRUE at any time. For example, a one-hot encoded FSM with three states would have state encod- ings of 001, 010, and 100. Each bit of state is stored in a flip-flop, so one- hot encoding requires more flip-flops than binary encoding. However, with one-hot encoding, the next state and output logic is often simpler, so fewer gates are required. The best encoding choice depends on the specific FSM.

Example 3.6 FSM STATE ENCODING
A divide-by-N counter has one output and no inputs. The output Y is HIGH for one clock cycle out of every N. In other words, the output divides the frequency of the clock by N. The waveform and state transition diagram for a divide-by-3 counter is shown in Figure 3.28. Sketch circuit designs for such a counter using binary and one-hot state encodings.
 
128
 

CHAPTER THREE
 
Sequential Logic Design
 


 

(a)

Figure 3.28 Divide-by-3 counter
(a) waveform and (b) state transition diagram




(b)

 
Table 3.6 Divide-by-3 counter state transition table
 
Solution Tables 3.6 and 3.7 show the abstract state transition and output tables, respectively, before encoding.
Table 3.8 compares binary and one-hot encodings for the three states.
The binary encoding uses two bits of state. Using this encoding, the state tran- sition table is shown in Table 3.9. Note that there are no inputs; the next state depends only on the current state. The output table is left as an exercise to the reader. The next state and output equations are:
 

 
S1′ = S1S0 S0′ = S1S0
 

(3.4)
 
Table 3.7 Divide-by-3 counter
output table
 
Y = S1 S0	(3.5)
The one-hot encoding uses three bits of state. The state transition table for this
encoding is shown in Table 3.10 and the output table is again left as an exercise to the reader. The next state and output equations are as follows:
S2′ = S1
 
S1′ = S0 S0′ = S2
 
(3.6)
 
Y = S0	(3.7)
Figure 3.29 shows schematics for each of these designs. Note that the hardware
for the binary encoded design could be optimized to share the same gate for Y and S 0. Also, observe that one-hot encoding requires both settable (s) and reset- table (r) flip-flops to initialize the machine to S0 on reset. The best implementa- tion choice depends on the relative cost of gates and flip-flops, but the one-hot design is usually preferable for this specific example.

A related encoding is the one-cold encoding, in which K states are represented with K bits, exactly one of which is FALSE.
 
3.4 Finite State Machines	129


Table 3.8 One-hot and binary encodings for divide-by-3 counter


State	One-Hot Encoding
S2	S1	S0	Binary Encoding
S1	S0
S0	0	0	1	0	0
S1	0	1	0	0	1
S2	1	0	0	1	0

Table 3.9 State transition table with binary encoding

Current State
S1	S0	Next State
S1′	S0′
0	0	0	1
0	1	1	0
1	0	0	0


Table 3.10 State transition table with one-hot encoding


S2	Current State
S1	
S0	
S2′	Next State
S1′	
S0′
0	0	1	0	1	0
0	1	0	1	0	0
1	0	0	0	0	1

CLK

Y


 



next state logic state register
(a)

CLK
 



output logic
 



output
 
Figure 3.29 Divide-by-3 circuits for (a) binary and (b) one-hot encodings
 


Reset
(b)
 
S0	Y
 
130
 

CHAPTER THREE
 
Sequential Logic Design
 



3.4.3 Moore and Mealy Machines
So far, we have shown examples of Moore machines, in which the output depends only on the state of the system. Hence, in state transition diagrams for Moore machines, the outputs are labeled in the circles. Recall that Mealy machines are much like Moore machines, but the outputs can depend on inputs as well as the current state. Hence, in state transition diagrams for Mealy machines, the outputs are labeled on the arcs instead of in the circles. The block of combinational logic that com- putes the outputs uses the current state and inputs, as was shown in Figure 3.22(b).


Example 3.7 MOORE VERSUS MEALY MACHINES
Alyssa P. Hacker owns a pet robotic snail with an FSM brain. The snail crawls from left to right along a paper tape containing a sequence of 1’s and 0’s. On each clock cycle, the snail crawls to the next bit. The snail smiles when the last two bits that it has crawled over are 01. Design the FSM to compute when the snail should smile. The input A is the bit underneath the snail’s antennae. The output Y is TRUE when the snail smiles. Compare Moore and Mealy state machine designs. Sketch a timing diagram for each machine showing the input, states, and output as Alyssa’s snail crawls along the sequence 0100110111.
Solution The Moore machine requires three states, as shown in Figure 3.30(a). Convince yourself that the state transition diagram is correct. In particular, why is there an arc from S2 to S1 when the input is 0?
In comparison, the Mealy machine requires only two states, as shown in Figure 3.30(b). Each arc is labeled as A/Y. A is the value of the input that causes that transition, and Y is the corresponding output.
Tables 3.11 and 3.12 show the state transition and output tables, respectively for the Moore machine. The Moore machine requires at least two bits of state. Consider using a binary state encoding: S0 = 00, S1 = 01, and S2 = 10. Tables 3.13 and 3.14 rewrite the state transition and output tables, respectively, with these encodings.
From these tables, we find the next state and output equations by inspection. Note that these equations are simplified using the fact that state 11 does not exist. Thus, the corresponding next state and output for the nonexistent state are don’t cares (not shown in the tables). We use the don’t cares to minimize our equations.
S1′ = S0A
 
S0′ = A
 
(3.8)
 
Y = S1	(3.9)
 
3.4 Finite State Machines	131
Table 3.15 shows the combined state transition and output table for the Mealy machine. The Mealy machine requires only one bit of state. Consider using a binary state encoding: S0 = 0 and S1 = 1. Table 3.16 rewrites the state transition and output table with these encodings.
From these tables, we find the next state and output equations by inspection.
 
S0′ = A
 
(3.10)
 
Y = S0 A	(3.11)
The Moore and Mealy machine schematics are shown in Figure 3.31. The timing diagrams for each machine are shown in Figure 3.32 (see page 133). The two machines follow a different sequence of states. Moreover, the Mealy machine’s output rises a cycle sooner because it responds to the input rather than wait- ing for the state change. If the Mealy output were delayed through a flip-flop, it would match the Moore output. When choosing your FSM design style, consider when you want your outputs to respond.
 







1

(a)
 



Reset




1/0
 




0/0

S0	S1

0/0
1/1 (b)
 
Figure 3.30 FSM state transition diagrams: (a) Moore machine, (b) Mealy machine


Table 3.11 Moore state transition table




Table 3.12 Moore output table

Current State
S	Output
Y
S0	0
S1	0
S2	1
 
132
 

CHAPTER THREE
 
Sequential Logic Design
 


 
Table 3.13 Moore state transition table with state encodings
 






Table 3.14 Moore output table with state encodings
 

Current State
S1	S0	Output
Y
0	0	0
0	1	0
1	0	1

Table 3.15 Mealy state transition and output table

Current State
S	Input
A	Next State
S 	Output
Y
S0	0	S1	0
S0	1	S0	0
S1	0	S1	0
S1	1	S0	1

Table 3.16 Mealy state transition and output table with state encodings

Current State
S0	Input
A	Next State
S0′	Output
Y
0	0	1	0
0	1	0	0
1	0	1	0
1	1	0	1



3.4.4	Factoring State Machines
Designing complex FSMs is often easier if they can be broken down into multiple interacting simpler state machines, such that the output of some machines is the input of others. This application of hierarchy and modularity is called factoring of state machines.
 
3.4 Finite State Machines	133
Y
A
Figure 3.31 FSM schematics for
Y	(a) Moore and (b) Mealy machines
Reset
(a)	(b)
 



CLK
Reset
A

S Y

S Y
 






Figure 3.32 Timing diagrams for Moore and Mealy machines
 


 
Example 3.8 UNFACTORED AND FACTORED STATE MACHINES
Modify the traffic light controller from Section 3.4.1 to have a parade mode, which keeps the Bravado Boulevard light green while spectators and the band march to football games in scattered groups. The controller receives two more inputs: P and R. Asserting P for at least one cycle enters parade mode. Asserting R for at least one cycle leaves parade mode. When in parade mode, the control- ler proceeds through its usual sequence until LB turns green, then remains in that state with LB green until parade mode ends.
First, sketch a state transition diagram for a single FSM, as shown in Figure 3.33(a). Then, sketch the state transition diagrams for two interacting FSMs, as shown in Figure 3.33(b). The Mode FSM asserts the output M when it is in parade mode. The Lights FSM controls the lights based on M and the traffic sensors, TA and TB.
Solution Figure 3.34(a) shows the single FSM design. States S0 to S3 handle nor- mal mode. States S4 to S7 handle parade mode. The two halves of the diagram are almost identical, but in parade mode, the FSM remains in S6 with a green light on Bravado Blvd. The P and R inputs control movement between these two halves. The FSM is messy and tedious to design. Figure 3.34(b) shows the factored FSM design. The Mode FSM has two states to track whether the lights are in normal or parade mode. The Lights FSM is modified to remain in S2 while M is TRUE.
 
134
 

CHAPTER THREE
 
Sequential Logic Design
 




P R

Figure 3.33 (a) Single and
(b) factored designs for modified	T	LA
traffic light controller FSM	A
TB	LB
P
R	LA
TA	L
TB

(a)	(b)

P TA













Figure 3.34 State transition diagrams: (a) unfactored,
(b)	factored











 


(b)
 
M + TB
Lights FSM
 
R
Mode FSM
 
3.4 Finite State Machines	135


3.4.5	Deriving an FSM from a Schematic
Deriving the state transition diagram from a schematic follows nearly the reverse process of FSM design. This process can be necessary, for example, when taking on an incompletely documented project or reverse engineering somebody else’s system.
	Examine circuit, stating inputs, outputs, and state bits.
	Write next state and output equations.
	Create next state and output tables.
	Reduce the next state table to eliminate unreachable states.
	Assign each valid state bit combination a name.
	Rewrite next state and output tables with state names.
	Draw state transition diagram.
	State in words what the FSM does.
In the final step, be careful to succinctly describe the overall purpose and function of the FSM—do not simply restate each transition of the state transition diagram.


Example 3.9 DERIVING AN FSM FROM ITS CIRCUIT
Alyssa P. Hacker arrives home, but her keypad lock has been rewired and her old code no longer works. A piece of paper is taped to it showing the circuit diagram in Figure 3.35. Alyssa thinks the circuit could be a finite state machine and decides to derive the state transition diagram to see whether it helps her get in the door.
Solution Alyssa begins by examining the circuit. The input is A1:0 and the output is Unlock. The state bits are already labeled in Figure 3.35. This is a Moore


 
A1 A0
 
CLK
 

Unlock


Figure 3.35 Circuit of found FSM for Example 3.9
 
136
 

CHAPTER THREE
 
Sequential Logic Design
 


machine because the output depends only on the state bits. From the circuit, she writes down the next state and output equations directly:
S1′ = S0 A1A0
 
S0′ = S1 S0A1A0
Unlock = S1
 
(3.12)
 
Next, she writes down the next state and output tables from the equations, as shown in Tables 3.17 and 3.18, respectively, first placing 1’s in the tables as indi- cated by Equation 3.12. She places 0’s everywhere else.
Alyssa reduces the table by removing unused states and combining rows using don’t cares. The S1:0 = 11 state is never listed as a possible next state in Table 3.17, so rows with this current state are removed. For current state S1:0 = 10, the next

 
Table 3.17 Next state table derived from circuit in Figure 3.35
 





















Table 3.18 Output table derived from circuit in Figure 3.35
 

Current State
S1	S0	Output
Unlock
0	0	0
0	1	0
1	0	1
1	1	1
 
3.4	Finite State Machines	137
 
Table 3.19 Reduced next state table

Current State
S1	S0	
A1	Input	
A0	Next State
S1′	S0′
0	0	0		0	0	0
0	0	0		1	0	0
0	0	1		0	0	0
0	0	1		1	0	1
0	1	0		0	0	0
0	1	0		1	1	0
0	1	1		0	0	0
0	1	1		1	0	0
1	0	X		X	0	0


Table 3.21 Symbolic next state table
 












Table 3.20 Reduced output table

Current State
S1	S0	Output
Unlock
0	0	0
0	1	0
1	0	1











Table 3.22 Symbolic output table
 

Current State
S	Output
Unlock
S0	0
S1	0
S2	1

state is always S1:0 = 00, independent of the inputs, so don’t cares are inserted for the inputs. The reduced tables are shown in Tables 3.19 and 3.20.
She assigns names to each state bit combination: S0 is S1:0 = 00, S1 is S1:0 = 01, and S2 is S1:0 = 10. Tables 3.21 and 3.22 show the next state and output tables, respectively, with state names.
 
138
 

CHAPTER THREE
 
Sequential Logic Design
 


Reset



A = 3


Figure 3.36 State transition diagram of found FSM from Example 3.9









Alyssa writes down the state transition diagram shown in Figure 3.36 using Tables 3.21 and 3.22. By inspection, she can see that the finite state machine unlocks the door only after detecting an input value, A1:0, of three followed by an input value of one. The door is then locked again. Alyssa tries this code on the door keypad and the door opens!

3.4.6 FSM Review
Finite state machines are a powerful way to systematically design sequential circuits from a written specification. Use the following procedure to design an FSM:
	Identify the inputs and outputs.
	Sketch a state transition diagram.
	For a Moore machine:
–	Write a state transition table.
–	Write an output table.
	For a Mealy machine:
–	Write a combined state transition and output table.
	Select state encodings—your selection affects the hardware design.
	Write Boolean equations for the next state and output logic.
	Sketch the circuit schematic.
 
3.5	Timing of Sequential Logic	139


We will repeatedly use FSMs to design complex digital systems throughout this book.

3.5 TIMING OF SEQUENTIAL LOGIC
Recall that a flip-flop copies the input D to the output Q on the rising edge of the clock. This process is called sampling D on the clock edge. If D is stable at either 0 or 1 when the clock rises, this behavior is clearly defined. But what happens if D is changing at the same time the clock rises?
This problem is similar to that faced by a camera when snapping a picture. Imagine photographing a frog jumping from a lily pad into the lake. If you take the picture before the jump, you will see a frog on a lily pad. If you take the picture after the jump, you will see ripples in the water. But if you take it just as the frog jumps, you may see a blurred image of the frog stretching from the lily pad into the water. A camera is characterized by its aperture time, during which the object must remain still for a sharp image to be captured. Similarly, a sequential element has an aperture time around the clock edge, during which the input must be stable for the flip-flop to produce a well-defined output.
The aperture of a sequential element is defined by a setup time and a hold time, before and after the clock edge, respectively. Just as the static discipline limited us to using logic levels outside the forbidden zone, the dynamic discipline limits us to using signals that change outside the aperture time. By taking advantage of the dynamic discipline, we can think of time in discrete units called clock cycles, just as we think of sig- nal levels as discrete 1’s and 0’s. A signal may glitch and oscillate wildly for some bounded amount of time. Under the dynamic discipline, we are concerned only about its final value at the end of the clock cycle, after it has settled to a stable value. Hence, we can simply write A[n], the value of signal A at the end of the nth clock cycle, where n is an integer, rather than A(t), the value of A at some instant t, where t is any real number.
The clock period has to be long enough for all signals to settle. This sets a limit on the speed of the system. In real systems, the clock does not reach all flip-flops at precisely the same time. This variation in time, called clock skew, further increases the necessary clock period.
Sometimes it is impossible to satisfy the dynamic discipline, especially when interfacing with the real world. For example, consider a circuit with an input coming from a button. A monkey might press the button just as the clock rises. This can result in a phenomenon called metastability, where the flip-flop captures a value partway between 0 and 1 that can take an unlimited amount of time to resolve into a good logic value. The solution to such asynchronous inputs is to use a synchronizer, which has a very small (but nonzero) probability of producing an illegal logic value.
We expand on all of these ideas in the rest of this section.
 
140
 

CHAPTER THREE
 
Sequential Logic Design
 



3.5.1	The Dynamic Discipline
So far, we have focused on the functional specification of sequential cir- cuits. Recall that a synchronous sequential circuit, such as a flip-flop or FSM, also has a timing specification, as illustrated in Figure 3.37. When the clock rises, the output (or outputs) may start to change after the clock- to-Q contamination delay, tccq, and must definitely settle to the final value within the clock-to-Q propagation delay, tpcq. These represent the fastest and slowest delays through the circuit, respectively. For the circuit to sam- ple its input correctly, the input (or inputs) must have stabilized at least some setup time, tsetup, before the rising edge of the clock and must remain stable for at least some hold time, thold, after the rising edge of the clock. The sum of the setup and hold times is called the aperture time of the circuit, because it is the total time for which the input must remain stable.
The dynamic discipline states that the inputs of a synchronous sequential circuit must be stable during the setup and hold aperture time around the clock edge. By imposing this requirement, we guarantee that the flip-flops sample signals while they are not changing. Because we are concerned only about the final values of the inputs at the time they are sampled, we can treat signals as discrete in time as well as in logic levels.

3.5.2	System Timing
The clock period or cycle time, Tc, is the time between rising edges of a repetitive clock signal. Its reciprocal, fc = 1/Tc, is the clock frequency. All else being the same, increasing the clock frequency increases the work that a digital system can accomplish per unit time. Frequency is measured in units of Hertz (Hz), or cycles per second: 1 megahertz (MHz) = 106 Hz, and 1 gigahertz (GHz) = 109 Hz.
Figure 3.38(a) illustrates a generic path in a synchronous sequen- tial circuit whose clock period we wish to calculate. On the rising edge of the clock, register R1 produces output (or outputs) Q1. These sig- nals enter a block of combinational logic, producing D2, the input (or inputs) to register R2. The timing diagram in Figure 3.38(b) shows that each output signal may start to change a contamination delay after its

 



Figure 3.37 Timing specification for synchronous sequential circuit
 
CLK

output(s) input(s)
 
3.5 Timing of Sequential Logic	141
 





CLK
 





CLK
 






Figure 3.38 Path between registers and timing diagram
 
R1	R2
(a)
 

(b)
 

input changes and settles to the final value within a propagation delay after its input settles. The gray arrows represent the contamination delay through R1 and the combinational logic, and the blue arrows represent the propagation delay through R1 and the combinational logic. We ana- lyze the timing constraints with respect to the setup and hold time of the second register, R2.

Setup Time Constraint
Figure 3.39 is the timing diagram showing only the maximum delay through the path, indicated by the blue arrows. To satisfy the setup time of R2, D2 must settle no later than the setup time before the next clock edge. Hence, we find an equation for the minimum clock period:
Tc ≥ tpcq + tpd + tsetup	(3.13)
In commercial designs, the clock period is often dictated by the Director of Engineering or by the marketing department (to ensure a competitive product). Moreover, the flip-flop clock-to-Q propagation delay and setup time, tpcq and tsetup, are specified by the manufacturer. Hence, we rearrange Equation 3.13 to solve for the maximum propa- gation delay through the combinational logic, which is usually the only variable under the control of the individual designer.
 
tpd
 
≤ Tc − (tpcq + tsetup )
 
(3.14)
 
The term in parentheses, tpcq + tsetup, is called the sequencing over- head. Ideally, the entire cycle time Tc would be available for useful

CLK	CLK
 
 
R1	R2
Tc
 

Figure 3.39 Maximum delay for setup time constraint
 
142
 

CHAPTER THREE
 
Sequential Logic Design
 


computation in the combinational logic, tpd. However, the sequencing overhead of the flip-flop cuts into this time. Equation 3.14 is called the setup time constraint or max-delay constraint because it depends on the setup time and limits the maximum delay through combinational logic.
If the propagation delay through the combinational logic is too great, D2 may not have settled to its final value by the time R2 needs it to be stable and samples it. Hence, R2 may sample an incorrect result or even an illegal logic level, a level in the forbidden region. In such a case, the circuit will malfunction. The problem can be solved by increasing the clock period or by redesigning the combinational logic to have a shorter propagation delay.

Hold Time Constraint
The register R2 in Figure 3.38(a) also has a hold time constraint. Its input, D2, must not change until some time, thold, after the rising edge of the clock. According to Figure 3.40, D2 might change as soon as tccq + tcd after the rising edge of the clock. Hence, we find
 
tccq + tcd
 
≥ thold	(3.15)
 
Again, tccq and thold are characteristics of the flip-flop that are usu- ally outside the designer’s control. Rearranging, we can solve for the minimum contamination delay through the combinational logic:
 
tcd
 
≥ thold − tccq
 
(3.16)
 
Equation 3.16 is called the hold time constraint or min-delay constraint
because it limits the minimum delay through combinational logic.
We have assumed that any logic elements can be connected to each other without introducing timing problems. In particular, we would expect that two flip-flops may be directly cascaded as in Figure 3.41 without causing hold time problems.


CLK	CLK
 
R1	R2

Figure 3.40 Minimum delay for hold time constraint
 
3.5 Timing of Sequential Logic	143
In such a case, tcd = 0 because there is no combinational logic between flip-flops. Substituting into Equation 3.16 yields the requirement that
 
thold ≤ tccq
 
(3.17)
 
Figure 3.41 Back-to-back
 
In other words, a reliable flip-flop must have a hold time shorter than its contamination delay. Often, flip-flops are designed with thold = 0 so that Equation 3.17 is always satisfied. Unless noted otherwise, we will usually make that assumption and ignore the hold time constraint in this book.
Nevertheless, hold time constraints are critically important. If they are violated, the only solution is to increase the contamination delay through the logic, which requires redesigning the circuit. Unlike setup time constraints, they cannot be fixed by adjusting the clock period. Redesigning an integrated circuit and manufacturing the corrected design takes months and millions of dollars in today’s advanced technologies, so hold time violations must be taken extremely seriously.

Putting It All Together
Sequential circuits have setup and hold time constraints that dictate the maximum and minimum delays of the combinational logic between flip- flops. Modern flip-flops are usually designed so that the minimum delay through the combinational logic can be 0—that is, flip-flops can be placed back-to-back. The maximum delay constraint limits the number of consecutive gates on the critical path of a high-speed circuit because a high clock frequency means a short clock period.
 
flip-flops
 


 
Example 3.10 TIMING ANALYSIS
Ben Bitdiddle designed the circuit in Figure 3.42. According to the data sheets for the components he is using, flip-flops have a clock-to-Q contamination delay of 30 ps and a propagation delay of 80 ps. They have a setup time of 50 ps and a hold time of 60 ps. Each logic gate has a propagation delay of 40 ps

CLK	CLK
A	n1

 
B

C			X '	X D			Y '	Y
 

Figure 3.42 Sample circuit for timing analysis
 
144
 

CHAPTER THREE
 
Sequential Logic Design
 


and a contamination delay of 25 ps. Help Ben determine the maximum clock frequency and whether any hold time violations could occur. This process is called timing analysis.
Solution Figure 3.43(a) shows waveforms illustrating when the signals might change. The inputs, A to D, are registered, so they only change shortly after CLK rises.
The critical path occurs when B = 1, C = 0, D = 0, and A rises from 0 to 1, triggering n1 to rise, X to rise, and Y to fall, as shown in Figure 3.43(b). This path involves three gate delays. For the critical path, we assume that each gate requires its full propagation delay. Y must set up before the next rising edge of the CLK. Hence, the minimum cycle time is
Tc ≥ tpcq + 3tpd + tsetup = 80 + 3 × 40 + 50 = 250 ps	(3.18)
The maximum clock frequency is fc = 1/Tc = 4 GHz.
A short path occurs when A = 0 and C rises, causing X to rise, as shown in Figure 3.43(c). For the short path, we assume that each gate switches after only a contamination delay. This path involves only one gate delay, so it may occur after tccq + tcd = 30 + 25 = 55 ps. But recall that the flip-flop has a hold time of


0	50	100	150	200	250	t (ps)







(a)
Figure 3.43 Timing diagram:
(a) general case, (b) critical path,
(c) short path




(b)




(c)
 
3.5 Timing of Sequential Logic	145
60 ps, meaning that X must remain stable for 60 ps after the rising edge of CLK for the flip-flop to reliably sample its value. In this case, X = 0 at the first rising edge of CLK, so we want the flip-flop to capture X = 0. Because X did not hold stable long enough, the actual value of X is unpredictable. The circuit has a hold time violation and may behave erratically at any clock frequency.


Example 3.11 FIXING HOLD TIME VIOLATIONS
Alyssa P. Hacker proposes to fix Ben’s circuit by adding buffers to slow down the short paths, as shown in Figure 3.44. The buffers have the same delays as other gates. Help her determine the maximum clock frequency and whether any hold time problems could occur.
Solution Figure 3.45 shows waveforms illustrating when the signals might change. The critical path from A to Y is unaffected because it does not pass through any buffers. Therefore, the maximum clock frequency is still 4 GHz. However, the short paths are slowed by the contamination delay of the buffer. Now, X will not change until tccq + 2tcd = 30 + 2 × 25 = 80 ps. This is after the 60 ps hold time has elapsed, so the circuit now operates correctly.
This example had an unusually long hold time to illustrate the point of hold time problems. Most flip-flops are designed with thold < tccq to avoid such


CLK	CLK
 
A	n1

B

C	n2

Buffers added to fix
D	hold time violation
n3
 





	X'	X

Y'	Y
 



Figure 3.44 Corrected circuit to fix hold time problem
 


 
0	50	100	150	200	250	t (ps)


Figure 3.45 Timing diagram with buffers to fix hold time problem
 
146
 

CHAPTER THREE
 
Sequential Logic Design
 


problems. However, some high-performance microprocessors, including the Pentium 4, use an element called a pulsed latch in place of a flip-flop. The pulsed latch behaves like a flip-flop but has a short clock-to-Q delay and a long hold time. In general, adding buffers can usually, but not always, solve hold time problems without slowing the critical path.


3.5.3	Clock Skew*
In the previous analysis, we assumed that the clock reaches all regis- ters at exactly the same time. In reality, there is some variation in this time. This variation in clock edges is called clock skew. For example, the wires from the clock source to different registers may be of different lengths, resulting in slightly different delays, as shown in Figure 3.46. Noise also results in different delays. Clock gating, described in Section 3.2.5, further delays the clock. If some clocks are gated and others are not, there will be substantial skew between the gated and ungated clocks. In Figure 3.46, CLK2 is early with respect to CLK1, because the clock wire between the two registers follows a scenic route. If the clock had been routed differently, CLK1 might have been early instead. When doing timing analysis, we consider the worst-case scenario so that we can guarantee that the circuit will work under all circumstances.
Figure 3.47 adds skew to the timing diagram from Figure 3.38. The heavy clock line indicates the latest time at which the clock signal might reach any register; the hashed lines show that the clock might arrive up to tskew earlier.
First, consider the setup time constraint shown in Figure 3.48. In the worst case, R1 receives the latest skewed clock and R2 receives the earli- est skewed clock, leaving as little time as possible for data to propagate between the registers.

delay




 

Figure 3.46 Clock skew caused by wire delay
 
R1	R 2
 
3.5 Timing of Sequential Logic	147
 





CLK
 





CLK
 



CLK Q1 D2
 


t skew
c
 





Figure 3.47 Timing diagram with clock skew
 
R1	R 2
(a)
 

(b)
 

CLK1	CLK2
 
 
R1	R2
Tc
CLK1
 


Figure 3.48 Setup time constraint
 
CLK2 	

Q1 D2
 





tpcq
 




tpd	t setup t skew
 
with clock skew
 


The data propagates through the register and combinational logic and must set up before R2 samples it. Hence, we conclude that
Tc ≥ tpcq + tpd + tsetup + tskew	(3.19)
 
tpd
 
≤ Tc − (tpcq + tsetup + tskew )
 
(3.20)
 
Next, consider the hold time constraint shown in Figure 3.49. In the worst case, R1 receives an early skewed clock, CLK1, and R2 receives a late skewed clock, CLK2. The data zips through the register and combi- national logic, but must not arrive until a hold time after the late clock. Thus, we find that
 
tccq + tcd
 
≥ thold + tskew	(3.21)
 
tcd
 
≥ thold + tskew − tccq
 
(3.22)
 
In summary, clock skew effectively increases both the setup time and the hold time. It adds to the sequencing overhead, reducing the time avail- able for useful work in the combinational logic. It also increases the required minimum delay through the combinational logic. Even if thold = 0, a pair of back-to-back flip-flops will violate Equation 3.22 if tskew > tccq. To prevent serious hold time failures, designers must not permit too much
 
148
 

CHAPTER THREE
 
Sequential Logic Design
 


CLK1	CLK2
 
R1	R 2

 


Figure 3.49 Hold time constraint with clock skew
 
CLK1 CLK2 Q1 D2
 





tccq
 





tcd
 

t skewt hold


clock skew. Sometimes, flip-flops are intentionally designed to be partic- ularly slow (i.e., large tccq), to prevent hold time problems even when the clock skew is substantial.


Example 3.12 TIMING ANALYSIS WITH CLOCK SKEW
Revisit Example 3.10 and assume that the system has 50 ps of clock skew.
Solution The critical path remains the same, but the setup time is effectively increased by the skew. Hence, the minimum cycle time is
 
Tc ≥ tpcq + 3tpd + tsetup + tskew
= 80 + 3 × 40 + 50 + 50 = 300 ps
The maximum clock frequency is fc = 1/Tc = 3.33 GHz.
 

(3.23)
 
The short path also remains the same at 55 ps. The hold time is effectively increased by the skew to 60 + 50 = 110 ps, which is much greater than 55 ps. Hence, the circuit will violate the hold time and malfunction at any frequency. The circuit violated the hold time constraint even without skew. Skew in the system just makes the violation worse.


Example 3.13 FIXING HOLD TIME VIOLATIONS
Revisit Example 3.11 and assume that the system has 50 ps of clock skew.
Solution The critical path is unaffected, so the maximum clock frequency remains 3.33 GHz.
 
3.5 Timing of Sequential Logic	149
 


The short path increases to 80 ps. This is still less than thold + tskew = 110 ps, so the circuit still violates its hold time constraint.
To fix the problem, even more buffers could be inserted. Buffers would need to be added on the critical path as well, reducing the clock frequency. Alternatively, a better flip-flop with a shorter hold time might be used.

 

3.5.4	Metastability
As noted earlier, it is not always possible to guarantee that the input to a sequential circuit is stable during the aperture time, especially when the input arrives from the external world. Consider a button connected to the input of a flip-flop, as shown in Figure 3.50. When the button is not pressed, D = 0. When the button is pressed, D = 1. A monkey presses the button at some random time relative to the rising edge of CLK. We want to know the output Q after the rising edge of CLK. In Case I, when the button is pressed much before CLK, Q = 1. In Case II, when the button is not pressed until long after CLK, Q = 0. But in Case III, when the button is pressed sometime between tsetup before CLK and thold after CLK, the input violates the dynamic discipline and the output is undefined.

Metastable State
When a flip-flop samples an input that is changing during its aper- ture, the output Q may momentarily take on a voltage between 0 and VDD that is in the forbidden zone. This is called a metastable state. Eventually, the flip-flop will resolve the output to a stable state of either 0 or 1. However, the resolution time required to reach the stable state is unbounded.
The metastable state of a flip-flop is analogous to a ball on the summit of a hill between two valleys, as shown in Figure 3.51. The two valleys are stable states, because a ball in the valley will remain there as long as it is not disturbed. The top of the hill is called metastable because the ball would remain there if it were perfectly balanced. But because nothing is perfect, the ball will eventually roll to one side or the other. The time required for this change to occur depends on how nearly well balanced the ball originally was. Every bistable device has a meta- stable state between the two stable states.

Resolution Time
If a flip-flop input changes at a random time during the clock cycle, the resolution time, tres, required to resolve to a stable state is also a random variable. If the input changes outside the aperture, then tres = tpcq. But if the input happens to change within the aperture, tres can be substantially longer. Theoretical and experimental analyses (see Section 3.5.6) have
 




Q



tsetup thold














Figure 3.50 Input changing before, after, or during aperture

metastable

 
Figure 3.51 Stable and metastable states


 
 
150
 

CHAPTER THREE
 
Sequential Logic Design
 


shown that the probability that the resolution time, tres, exceeds some arbitrary time, t, decreases exponentially with t:
 
P(tres
 
> t) =
 
T0 e Tc
 
− t
	(3.24)
 
where Tc is the clock period, and T0 and are characteristic of the flip- flop. The equation is valid only for t substantially longer than tpcq.
Intuitively, T0/Tc describes the probability that the input changes at a bad time (i.e., during the aperture time); this probability decreases with the cycle time, Tc. is a time constant indicating how fast the flip- flop moves away from the metastable state; it is related to the delay through the cross-coupled gates in the flip-flop.
In summary, if the input to a bistable device such as a flip-flop changes during the aperture time, the output may take on a metastable value for some time before resolving to a stable 0 or 1. The amount of time required to resolve is unbounded because for any finite time, t, the probability that the flip-flop is still metastable is nonzero. However, this probability drops off exponentially as t increases. Therefore, if we wait long enough, much longer than tpcq, we can expect with exceedingly high probability that the flip-flop will reach a valid logic level.

 

















CLK


D	Q



Figure 3.52 Synchronizer symbol
 
3.5.5	Synchronizers
Asynchronous inputs to digital systems from the real world are inevi- table. Human input is asynchronous, for example. If handled carelessly, these asynchronous inputs can lead to metastable voltages within the system, causing erratic system failures that are extremely difficult to track down and correct. The goal of a digital system designer should be to ensure that, given asynchronous inputs, the probability of encounter- ing a metastable voltage is sufficiently small. “Sufficiently” depends on the context. For a cell phone, perhaps one failure in 10 years is accept- able, because the user can always turn the phone off and back on if it locks up. For a medical device, one failure in the expected life of the universe (1010 years) is a better target. To guarantee good logic levels, all asynchronous inputs should be passed through synchronizers.
A synchronizer, shown in Figure 3.52, is a device that receives an asynchronous input D and a clock CLK. It produces an output Q within a bounded amount of time; the output has a valid logic level with extremely high probability. If D is stable during the aperture, Q should take on the same value as D. If D changes during the aperture, Q may take on either a HIGH or LOW value, but must not be metastable.
Figure 3.53 shows a simple way to build a synchronizer out of two flip-flops. F1 samples D on the rising edge of CLK. If D is changing at that time, the output D2 may be momentarily metastable. If the clock
 
3.5 Timing of Sequential Logic	151


CLK	CLK

D	Q
F1	F2


Figure 3.53 Simple synchronizer








period is long enough, D2 will, with high probability, resolve to a valid logic level before the end of the period. F2 then samples D2, which is now stable, producing a good output Q.
We say that a synchronizer fails if Q, the output of the synchro- nizer, becomes metastable. This may happen if D2 has not resolved to a valid level by the time it must set up at F2—that is, if tres > Tc − tsetup. According to Equation 3.24, the probability of failure for a single input change at a random time is
 
P(failure) =  T0 e
Tc
 
− Tc −tsetup
	(3.25)
 
The probability of failure, P(failure), is the probability that the output Q will be metastable upon a single change in D. If D changes once per second, the probability of failure per second is just P(failure). However, if D changes N times per second, the probability of failure per second is N times as great:
 
P(failure)/sec = N  T0 e
Tc
 
− Tc −tsetup

(3.26)
 
System reliability is usually measured in mean time between failures (MTBF). As the name suggests, MTBF is the average amount of time between failures of the system. It is the reciprocal of the probability that the system will fail in any given second
Tc −tsetup
 
MTBF =
 
1	= Tce 
 
	(3.27)
 
P(failure)/sec	NT0
Equation 3.27 shows that the MTBF improves exponentially as the synchronizer waits for a longer time, Tc. For most systems, a synchronizer
 
152
 

CHAPTER THREE
 
Sequential Logic Design
 


that waits for one clock cycle provides a safe MTBF. In exceptionally high-speed systems, waiting for more cycles may be necessary.

Example 3.14 SYNCHRONIZER FOR FSM INPUT
The traffic light controller FSM from Section 3.4.1 receives asynchronous inputs from the traffic sensors. Suppose that a synchronizer is used to guarantee stable inputs to the controller. Traffic arrives on average 0.2 times per second. The flip-flops in the synchronizer have the following characteristics: = 200 ps, T0 = 150 ps, and tsetup = 500 ps. How long must the synchronizer clock period be for the MTBF to exceed 1 year?
Solution 1 year   × 107 seconds. Solve Equation 3.27.
Tc −500×10−12
 
 × 107
 
Tc e 200×10−12
= (0.2)(150 × 10−12)
 
(3.28)
 
This equation has no closed form solution. However, it is easy enough to solve by guess and check. In a spreadsheet, try a few values of Tc and calculate the MTBF until discovering the value of Tc that gives an MTBF of 1 year: Tc = 3.036 ns.

3.5.6 Derivation of Resolution Time*
Equation 3.24 can be derived using a basic knowledge of circuit theory, differential equations, and probability. This section can be skipped if you are not interested in the derivation or if you are unfamiliar with the mathematics.
A flip-flop output will be metastable after some time, t, if the flip- flop samples a changing input (causing a metastable condition) and the output does not resolve to a valid level within that time after the clock edge. Symbolically, this can be expressed as
P(tres > t) = P(samples changing input) × P(unresolved)	(3.29)
We consider each probability term individually. The asynchronous input signal switches between 0 and 1 in some time, tswitch, as shown in Figure 3.54. The probability that the input changes during the aperture around the clock edge is
 
P(samples changing input) = tswitch + tsetup + thold
Tc
 

(3.30)
 
If the flip-flop does enter metastability—that is, with probabil- ity P(samples changing input)—the time to resolve from metastabil- ity depends on the inner workings of the circuit. This resolution time determines P(unresolved), the probability that the flip-flop has not yet
 
3.5	Timing of Sequential Logic	153
 


Tc
CLK


D
 





Figure 3.54 Input timing
 



 

VDD
 
vout
 


slope = G
 

v in(t)	vout(t) i(t )
 




(a)
 



v(t)
 
VDD /2


0

(b)
 
V



VDD/2
 


vin
VDD
 
G
R

C

(c)
 
Figure 3.55 Circuit model of bistable device
 

resolved to a valid logic level after a time t. The remainder of this section analyzes a simple model of a bistable device to estimate this probability.
A bistable device uses storage with positive feedback. Figure 3.55(a) shows this feedback implemented with a pair of inverters; this circuit’s behavior is representative of most bistable elements. A pair of inverters behaves like a buffer. Let us model the buffer as having the symmetric DC transfer characteristics shown in Figure 3.55(b), with a slope of G. The buffer can deliver only a finite amount of output current; we can model this as an output resistance, R. All real circuits also have some capacitance C that must be charged up. Charging the capacitor through the resistor causes an RC delay, preventing the buffer from switching instantaneously. Hence, the complete circuit model is shown in Figure 3.55(c), where vout(t) is the voltage of interest conveying the state of the bistable device.
The metastable point for this circuit is vout(t) = vin(t) = VDD/2; if the circuit began at exactly that point, it would remain there indefinitely in the absence of noise. Because voltages are continuous variables, the chance that the circuit will begin at exactly the metastable point is van- ishingly small. However, the circuit might begin at time 0 near metasta- bility at vout(0) = VDD/2 + V for some small offset V. In such a case, the positive feedback will eventually drive vout(t) to VDD if V > 0 and to 0 if V < 0. The time required to reach VDD or 0 is the resolution time of the bistable device.
The DC transfer characteristic is nonlinear, but it appears linear near the metastable point, which is the region of interest to us. Specifically, if vin(t) = VDD/2 +  V/G, then vout(t) = VDD/2 +  V for
small  V. The current through the resistor is i(t) = (vout(t) − vin(t))/R.
 
154
 

CHAPTER THREE
 
Sequential Logic Design
 


The capacitor charges at a rate dvin(t)/dt = i(t)/C. Putting these facts together, we find the governing equation for the output voltage.
 
dvout(t)  =
 
(G − 1) 
vout(t) −
 
VDD 
 
(3.31)
 
 
dt	RC	
 
 
2  
 
This is a linear first-order differential equation. Solving it with the initial condition vout(0) = VDD/2 + V gives
 
vout(t) = VDD
2
 
+ ∆Ve
 
(G−1)t RC
 

(3.32)
 
Figure 3.56 plots trajectories for vout(t), given various starting points. vout(t) moves exponentially away from the metastable point VDD/2 until it saturates at VDD or 0. The output eventually resolves to 1 or 0. The amount of time this takes depends on the initial voltage offset ( V) from the metastable point (VDD/2).
Solving  Equation  3.32  for  the  resolution  time  tres, such  that
vout(tres) = VDD or 0, gives
 
(G−1)tres
 
VDD
 
| V |e	RC
 
=	2	(3.33)
 
tres
 
=  RC  ln  VDD 
G − 1	2|∆V |
 
(3.34)
 
In summary, the resolution time increases if the bistable device has high resistance or capacitance that causes the output to change slowly. It decreases if the bistable device has high gain, G. The resolution time also increases logarithmically as the circuit starts closer to the metasta- ble point ( V  0).
Define as  RC  . Solving Equation 3.34 for V finds the initial off- set, Vres, that gives a particular resolution time, tres:
 
∆Vres
 
= VDD e−tres /	(3.35)
2
 
Suppose that the bistable device samples the input while it is chang- ing. It measures a voltage, vin(0), which we will assume is uniformly dis- tributed between 0 and VDD. The probability that the output has not

vout(t)
VDD

 
Figure 3.56 Resolution trajectories
 

VDD /2
 


0	t
 
3.6	Parallelism	155
resolved to a legal value after time tres depends on the probability that the initial offset is sufficiently small. Specifically, the initial offset on vout must be less than  Vres, so the initial offset on vin must be less than
 Vres/G. Then, the probability that the bistable device samples the input at a time to obtain a sufficiently small initial offset is
 
	VDD
 
Vres 
 
2Vres
 
P(unresolved) = P vin (0) − 2
 
<	G  = GV
 
(3.36)
 
		DD
Putting this all together, the probability that the resolution time exceeds some time t is given by the following equation:
 
P(tres
 
> t) =
 
tswitch + tsetup + thold e GTc
 
− t
	(3.37)
 
Observe that Equation 3.37 is in the form of Equation 3.24, where T0 = (tswitch + tsetup + thold)/G and = RC/(G − 1). In summary, we have derived Equation 3.24 and shown how T0 and depend on physical properties of the bistable device.

3.6 PARALLELISM
The speed of a system is characterized by the latency and throughput of information moving through it. We define a token to be a group of inputs that are processed to produce a group of outputs. The term con- jures up the notion of placing subway tokens on a circuit diagram and moving them around to visualize data moving through the circuit. The latency of a system is the time required for one token to pass through the system from start to end. The throughput is the number of tokens that can be produced per unit time.

Example 3.15 COOKIE THROUGHPUT AND LATENCY
Ben Bitdiddle is throwing a milk and cookies party to celebrate the installation of his traffic light controller. It takes him 5 minutes to roll cookies and place them on his tray. It then takes 15 minutes for the cookies to bake in the oven. Once the cookies are baked, he starts another tray. What is Ben’s throughput and latency for a tray of cookies?
Solution In this example, a tray of cookies is a token. The latency is 1/3 hour per tray. The throughput is 3 trays/hour.

As you might imagine, the throughput can be improved by process- ing several tokens at the same time. This is called parallelism, which comes in two forms: spatial and temporal. With spatial parallelism,
 
156
 

CHAPTER THREE
 
Sequential Logic Design
 


multiple copies of the hardware are provided so that multiple tasks can be done at the same time. With temporal parallelism, a task is broken into stages, like an assembly line. Multiple tasks can be spread across the stages. Although each task must pass through all stages, a different task will be in each stage at any given time, so multiple tasks can overlap. Temporal parallelism is commonly called pipelining. Spatial parallelism is sometimes just called parallelism, but we will avoid that naming con- vention because it is ambiguous.

Example 3.16 COOKIE PARALLELISM
Ben Bitdiddle has hundreds of friends coming to his party and needs to bake cookies faster. He is considering using spatial and/or temporal parallelism.
Spatial Parallelism: Ben asks Alyssa P. Hacker to help out. She has her own cookie tray and oven.
Temporal Parallelism: Ben gets a second cookie tray. Once he puts one cookie tray in the oven, he starts rolling cookies on the other tray rather than waiting for the first tray to bake.
What is the throughput and latency using spatial parallelism? Using temporal parallelism? Using both?
Solution The latency is the time required to complete one task from start to fin- ish. In all cases, the latency is 1/3 hour. If Ben starts with no cookies, the latency is the time he has to wait until he gets to eat the first cookie.
The throughput is the number of cookie trays per hour. With spatial parallelism, Ben and Alyssa each complete one tray every 20 minutes. Hence, the throughput doubles, to 6 trays/hour. With temporal parallelism, Ben puts a new tray in the oven every 15 minutes, for a throughput of 4 trays/hour. These are illustrated in Figure 3.57.
If Ben and Alyssa use both techniques, they can bake 8 trays/hour.


Consider a task with latency L. In a system with no parallelism, the throughput is 1/L. In a spatially parallel system with N copies of the hardware, the throughput is N/L. In a temporally parallel system, the task is ideally broken into N steps, or stages, of equal length. In such a case, the throughput is also N/L, and only one copy of the hardware is required. However, as the cookie example showed, finding N steps of equal length is often impractical. If the longest step has a latency L1, the pipelined throughput is 1/L1.
Pipelining (temporal parallelism) is particularly attractive because it
speeds up a circuit without duplicating the hardware. Instead, registers are placed between blocks of combinational logic to divide the logic into
 
3.6 Parallelism	157
 



Spatial Parallelism
Tray 1

Tray 2

Tray 3

Tray 4


Temporal Parallelism
Tray 1

Tray 2

Tray 3
 



Latency:
time to first tray
0	5	10	15	20	25	30	35	40	45	50

 
Time


Legend





Figure 3.57 Spatial and temporal parallelism in the cookie kitchen
 


shorter stages that can run with a faster clock. The registers prevent a token in one pipeline stage from catching up with and corrupting the token in the next stage.
Figure 3.58 shows an example of a circuit with no pipelining. It con- tains four blocks of logic between the registers. The critical path passes through blocks 2, 3, and 4. Assume that the register has a clock-to-Q propagation delay of 0.3 ns and a setup time of 0.2 ns. Then, the cycle time is Tc = 0.3 + 3 + 2 + 4 + 0.2 = 9.5 ns. The circuit has a latency of
9.5 ns and a throughput of 1/9.5 ns = 105 MHz.
Figure 3.59 shows the same circuit partitioned into a two-stage pipeline by adding a register between blocks 3 and 4. The first stage has a minimum clock period of 0.3 + 3 + 2 + 0.2 = 5.5 ns. The second stage has a minimum clock period of 0.3 + 4 + 0.2 = 4.5 ns. The clock must be slow enough for all stages to work. Hence, Tc = 5.5 ns. The latency is

CLK	CLK


 



tpd2 = 3 ns
 





Tc = 9.5 ns
 
Figure 3.58 Circuit with no pipelining
 
158
 

CHAPTER THREE
 
Sequential Logic Design
 


 
CLK
 
CLK
 
CLK
 


 
Figure 3.59 Circuit with two-stage pipeline
 


tpd 2 = 3 ns
Stage 1: 5.5 ns	Stage 2: 4.5 ns
 



 
CLK
 
CLK
 
CLK
 
CLK
 


 
Figure 3.60 Circuit with three- stage pipeline
 


tpd 2 = 3 ns
Stage 1: 3.5 ns
 




Stage 2: 2.5 ns
 




Stage 3: 4.5 ns
 


two clock cycles, or 11 ns. The throughput is 1/5.5 ns = 182 MHz. This example shows that, in a real circuit, pipelining with two stages almost doubles the throughput and slightly increases the latency. In compari- son, ideal pipelining would exactly double the throughput at no penalty in latency. The discrepancy comes about because the circuit cannot be divided into two exactly equal halves and because the registers introduce more sequencing overhead.
Figure 3.60 shows the same circuit partitioned into a three-stage pipeline. Note that two more registers are needed to store the results of blocks 1 and 2 at the end of the first pipeline stage. The cycle time is now limited by the third stage to 4.5 ns. The latency is three cycles, or
13.5 ns. The throughput is 1/4.5 ns = 222 MHz. Again, adding a pipeline stage improves throughput at the expense of some latency.
Although these techniques are powerful, they do not apply to all situations. The bane of parallelism is dependencies. If a current task is dependent on the result of a prior task, rather than just prior steps in the current task, the task cannot start until the prior task has completed. For example, if Ben wants to check that the first tray of cookies tastes good before he starts preparing the second, he has a dependency that prevents pipelining or parallel operation. Parallelism is one of the most important techniques for designing high-performance digital systems. Chapter 7 discusses pipelining further and shows examples of handling dependencies.
 
3.7 Summary	159


3.7 SUMMARY
This chapter has described the analysis and design of sequential logic. In contrast to combinational logic, whose outputs depend only on the current inputs, sequential logic outputs depend on both current and prior inputs. In other words, sequential logic remembers information about prior inputs. This memory is called the state of the logic.
Sequential circuits can be difficult to analyze and are easy to design incorrectly, so we limit ourselves to a small set of carefully designed building blocks. The most important element for our purposes is the flip-flop, which receives a clock and an input D and produces an output
Q. The flip-flop copies D to Q on the rising edge of the clock and other- wise remembers the old state of Q. A group of flip-flops sharing a com- mon clock is called a register. Flip-flops may also receive reset or enable control signals.
Although many forms of sequential logic exist, we discipline our- selves to use synchronous sequential circuits because they are easy to design. Synchronous sequential circuits consist of blocks of combinational logic separated by clocked registers. The state of the circuit is stored in the registers and updated only on clock edges.
Finite state machines are a powerful technique for designing sequential circuits. To design an FSM, first identify the inputs and out- puts of the machine and sketch a state transition diagram, indicating the states and the transitions between them. Select an encoding for the states, and rewrite the diagram as a state transition table and output table, indicating the next state and output, given the current state and input. From these tables, design the combinational logic to compute the next state and output, and sketch the circuit.
Synchronous sequential circuits have a timing specification, includ- ing the clock-to-Q propagation and contamination delays, tpcq and tccq, and the setup and hold times, tsetup and thold. For correct operation, their inputs must be stable during an aperture time that starts a setup time before the rising edge of the clock and ends a hold time after the rising edge of the clock. The minimum cycle time Tc of the system is equal to the propagation delay tpd through the combinational logic plus tpcq + tsetup of the register. For correct operation, the contamination delay through the register and combinational logic must be greater than thold. Despite the common misconception to the contrary, hold time does not affect the cycle time.
Overall system performance is measured in latency and throughput. The latency is the time required for a token to pass from start to end. The throughput is the number of tokens that the system can process per unit time. Parallelism improves system throughput.
 


 

160
 

CHAPTER THREE
 

Sequential Logic Design
 

Exercises
Exercise 3.1 Given the input waveforms shown in Figure 3.61, sketch the output, Q, of an SR latch.


Figure 3.61 Input waveforms of SR latch for Exercise 3.1

Exercise 3.2 Given the input waveforms shown in Figure 3.62, sketch the output, Q, of an SR latch.


S

R

Figure 3.62 Input waveforms of SR latch for Exercise 3.2

Exercise 3.3 Given the input waveforms shown in Figure 3.63, sketch the output, Q, of a D latch.



Figure 3.63 Input waveforms of D latch or flip-flop for Exercises 3.3 and 3.5


Exercise 3.4 Given the input waveforms shown in Figure 3.64, sketch the output, Q, of a D latch.



Figure 3.64 Input waveforms of D latch or flip-flop for Exercises 3.4 and 3.6
 


Exercises	161


Exercise 3.5 Given the input waveforms shown in Figure 3.63, sketch the output, Q, of a D flip-flop.

Exercise 3.6 Given the input waveforms shown in Figure 3.64, sketch the output, Q, of a D flip-flop.

Exercise 3.7 Is the circuit in Figure 3.65 combinational logic or sequential logic? Explain in a simple fashion what the relationship is between the inputs and outputs. What would you call this circuit?

S	Q
Figure 3.65 Mystery circuit

R	Q

Exercise 3.8 Is the circuit in Figure 3.66 combinational logic or sequential logic? Explain in a simple fashion what the relationship is between the inputs and outputs. What would you call this circuit?





 
CLK
 
Figure 3.66 Mystery circuit
 






Exercise 3.9 The toggle (T) flip-flop has one input, CLK, and one output, Q. On each rising edge of CLK, Q toggles to the complement of its previous value. Draw a schematic for a T flip-flop using a D flip-flop and an inverter.

Exercise 3.10 A JK flip-flop receives a clock and two inputs, J and K. On the rising edge of the clock, it updates the output, Q. If J and K are both 0, Q retains its old value. If only J is 1, Q becomes 1. If only K is 1, Q becomes 0. If both J and K are 1, Q becomes the opposite of its present state.
(a)	Construct a JK flip-flop, using a D flip-flop and some combinational logic.
(b)	Construct a D flip-flop, using a JK flip-flop and some combinational logic.
(c)	Construct a T flip-flop (see Exercise 3.9), using a JK flip-flop.
 


 

162
 

CHAPTER THREE
 

Sequential Logic Design
 


Exercise 3.11 The circuit in Figure 3.67 is called a Muller C-element. Explain in a simple fashion what the relationship is between the inputs and output.

A B
Figure 3.67 Muller C-element	C
B
A

Exercise 3.12 Design an asynchronously resettable D latch, using logic gates. Exercise 3.13 Design an asynchronously resettable D flip-flop, using logic gates. Exercise 3.14 Design a synchronously settable D flip-flop, using logic gates.
Exercise 3.15 Design an asynchronously settable D flip-flop, using logic gates.

Exercise 3.16 Suppose that a ring oscillator is built from N inverters connected in a loop. Each inverter has a minimum delay of tcd and a maximum delay of tpd. If N is odd, determine the range of frequencies at which the oscillator might operate.

Exercise 3.17 Why must N be odd in Exercise 3.16?

Exercise 3.18 Which of the circuits in Figure 3.68 are synchronous sequential circuits? Explain.


CLK
 
 
Figure 3.68 Circuits
 
(a)
 

CLK
 
(b)
 

CLK
 
(c)	(d)


Exercise 3.19 You are designing an elevator controller for a building with 25 floors. The controller has two inputs: UP and DOWN. It produces an output indicating the floor that the elevator is on. There is no floor 13. What is the minimum number of bits of state in the controller?
 


Exercises	163


Exercise 3.20 You are designing an FSM to keep track of the mood of four students working in the digital design lab. Each student’s mood is either HAPPY (the circuit works), SAD (the circuit blew up), BUSY (working on the circuit), CLUELESS (confused about the circuit), or ASLEEP (face down on the circuit board). How many states does the FSM have? What is the minimum number of bits necessary to represent these states?

Exercise 3.21 How would you factor the FSM from Exercise 3.20 into multiple simpler machines? How many states does each simpler machine have? What is the minimum total number of bits necessary in this factored design?

Exercise 3.22 Describe in words what the state machine in Figure 3.69 does. Using binary state encodings, complete a state transition table and output table for the FSM. Write Boolean equations for the next state and output and sketch a schematic of the FSM.




Figure 3.69 State transition diagram for Exercise 3.22

A


Exercise 3.23 Describe in words what the state machine in Figure 3.70 does. Using binary state encodings, complete a state transition table and output table for the FSM. Write Boolean equations for the next state and output and sketch a schematic of the FSM.




 




A /0
 




A + B/0
 
Figure 3.70 State transition diagram for Exercise 3.23
 


Exercise 3.24 Accidents are still occurring at the intersection of Academic Avenue and Bravado Boulevard. The football team is rushing into the intersection the moment light B turns green. They are colliding with sleep- deprived CS majors who stagger into the intersection just before light A turns
 


 

164
 

CHAPTER THREE
 

Sequential Logic Design
 


red. Extend the traffic light controller from Section 3.4.1 so that both lights are red for 5 seconds before either light turns green again. Sketch your improved Moore machine state transition diagram, state encodings, state transition table, output table, next state and output equations, and your FSM schematic.

Exercise 3.25 Alyssa P. Hacker’s snail from Section 3.4.3 has a daughter with a Mealy machine FSM brain. The daughter snail smiles whenever she slides over the pattern 1101 or the pattern 1110. Sketch the state transition diagram for this happy snail using as few states as possible. Choose state encodings and write a combined state transition and output table, using your encodings. Write the next state and output equations and sketch your FSM schematic.

Exercise 3.26 You have been enlisted to design a soda machine dispenser for your department lounge. Sodas are partially subsidized by the student chapter of the IEEE, so they cost only 25 cents. The machine accepts nickels, dimes, and quarters. When enough coins have been inserted, it dispenses the soda and returns any necessary change. Design an FSM controller for the soda machine.
The FSM inputs are Nickel, Dime, and Quarter, indicating which coin was inserted. Assume that exactly one coin is inserted on each cycle. The outputs are Dispense, ReturnNickel, ReturnDime, and ReturnTwoDimes. When the FSM reaches 25 cents, it asserts Dispense and the necessary Return outputs required to deliver the appropriate change. Then, it should be ready to start accepting coins for another soda.

Exercise 3.27 Gray codes have a useful property in that consecutive numbers differ in only a single bit position. Table 3.23 lists a 3-bit Gray code representing the numbers 0 to 7. Design a 3-bit modulo 8 Gray code counter FSM with
no inputs and three outputs. (A modulo N counter counts from 0 to N − 1,
Table 3.23 3-bit Gray code

Number	Gray code
0	0	0	0
1	0	0	1
2	0	1	1
3	0	1	0
4	1	1	0
5	1	1	1
6	1	0	1
7	1	0	0
 


Exercises	165


then repeats. For example, a watch uses a modulo 60 counter for the minutes and seconds that counts from 0 to 59.) When reset, the output should be 000. On each clock edge, the output should advance to the next Gray code. After reaching 100, it should repeat with 000.

Exercise 3.28 Extend your modulo 8 Gray code counter from Exercise 3.27 to be an UP/DOWN counter by adding an UP input. If UP = 1, the counter advances to the next number. If UP = 0, the counter retreats to the previous number.

Exercise 3.29 Your company, Detect-o-rama, would like to design an FSM that takes two inputs, A and B, and generates one output, Z. The output in cycle n, Zn, is either the Boolean AND or OR of the corresponding input An and the previous input An-1, depending on the other input, Bn:

 
Zn = An An−1	if
Zn = An + An−1  if
 
Bn = 0
Bn = 1
 
(a)	Sketch the waveform for Z, given the inputs shown in Figure 3.71.
(b)	Is this FSM a Moore or a Mealy machine?
(c)	Design the FSM. Show your state transition diagram, encoded state transition table, next state and output equations, and schematic.


Figure 3.71 FSM input waveforms for Exercise 3.29


Exercise 3.30 Design an FSM with one input, A, and two outputs, X and Y. X should be 1 if A has been 1 for at least three cycles altogether (not necessarily consecutively). Y should be 1 if A has been 1 for at least two consecutive cycles. Show your state transition diagram, encoded state transition table, next state and output equations, and schematic.

Exercise 3.31 Analyze the FSM shown in Figure 3.72. Write the state transition and output tables and sketch the state transition diagram.
 


 

166
 

CHAPTER THREE
 

Sequential Logic Design
 


X

Figure 3.72 FSM schematic for
Exercise 3.31	Q


Exercise 3.32 Repeat Exercise 3.31 for the FSM shown in Figure 3.73. Recall that the s and r register inputs indicate set and reset, respectively.



 
Figure 3.73 FSM schematic for Exercise 3.32
 

Q
A
reset
 

Exercise 3.33 Ben Bitdiddle has designed the circuit in Figure 3.74 to compute a registered four-input XOR function. Each two-input XOR gate has a propagation delay of 100 ps and a contamination delay of 55 ps. Each flip-flop has a setup time of 60 ps, a hold time of 20 ps, a clock-to-Q maximum delay of 70 ps, and a clock-to-Q minimum delay of 50 ps.
(a)	If there is no clock skew, what is the maximum operating frequency of the circuit?
(b)	How much clock skew can the circuit tolerate if it must operate at 2 GHz?
(c)	How much clock skew can the circuit tolerate before it might experience a hold time violation?
(d)	Alyssa P. Hacker points out that she can redesign the combinational logic between the registers to be faster and tolerate more clock skew. Her improved circuit also uses three two-input XORs, but they are arranged differently. What is her circuit? What is its maximum frequency if there is no clock skew? How much clock skew can the circuit tolerate before it might experience a hold time violation?

CLK


Figure 3.74 Registered four-input XOR circuit for Exercise 3.33
 


Exercises	167


Exercise 3.34 You are designing an adder for the blindingly fast 2-bit RePentium Processor. The adder is built from two full adders, such that the carry out of
the first adder is the carry in to the second adder, as shown in Figure 3.75. Your adder has input and output registers and must complete the addition in one clock cycle. Each full adder has the following propagation delays: 20 ps from Cin to Cout or to Sum (S), 25 ps from A or B to Cout, and 30 ps from A or B to
S. The adder has a contamination delay of 15 ps from Cin to either output and
22 ps from A or B to either output. Each flip-flop has a setup time of 30 ps, a hold time of 10 ps, a clock-to-Q propagation delay of 35 ps, and a clock-to-Q contamination delay of 21 ps.
(a)	If there is no clock skew, what is the maximum operating frequency of the circuit?
(b)	How much clock skew can the circuit tolerate if it must operate at 8 GHz?
(c)	How much clock skew can the circuit tolerate before it might experience a hold time violation?
 
CLK

C A0
B0

A1 B1
 
CLK



S0


S1
 





Figure 3.75 2-bit adder schematic for Exercise 3.34
 

Exercise 3.35 A field programmable gate array (FPGA) uses configurable logic blocks (CLBs) rather than logic gates to implement combinational logic. The Xilinx Spartan 3 FPGA has propagation and contamination delays of 0.61 and
0.30 ns, respectively, for each CLB. It also contains flip-flops with propagation and contamination delays of 0.72 and 0.50 ns, and setup and hold times of 0.53 and 0 ns, respectively.
(a)	If you are building a system that needs to run at 40 MHz, how many consecutive CLBs can you use between two flip-flops? Assume that there is no clock skew and no delay through wires between CLBs.
(b)	Suppose that all paths between flip-flops pass through at least one CLB. How much clock skew can the FPGA have without violating the hold time?

Exercise 3.36 A synchronizer is built from a pair of flip-flops with tsetup = 50 ps, T0 = 20 ps, and = 30 ps. It samples an asynchronous input that changes 108 times per second. What is the minimum clock period of the synchronizer to achieve a mean time between failures (MTBF) of 100 years?
 


 

168
 

CHAPTER THREE
 

Sequential Logic Design
 


Exercise 3.37 You would like to build a synchronizer that can receive asynchronous inputs with an MTBF of 50 years. Your system is running at 1 GHz, and you use sampling flip-flops with = 100 ps, T0 = 110 ps, and
tsetup = 70 ps. The synchronizer receives a new asynchronous input on average
0.5 times per second (i.e., once every 2 seconds). What is the required probability of failure to satisfy this MTBF? How many clock cycles would you have to wait before reading the sampled input signal to give that probability of error?

Exercise 3.38 You are walking down the hallway when you run into your lab partner walking in the other direction. The two of you first step one way and are still in each other’s way. Then, you both step the other way and are still in each other’s way. Then you both wait a bit, hoping the other person will step aside.
You can model this situation as a metastable point and apply the same theory that has been applied to synchronizers and flip-flops. Suppose you create a mathematical model for yourself and your lab partner. You start the unfortunate
encounter in the metastable state. The probability that you remain in this state
− t
after t seconds is e  . indicates your response rate; today, your brain has been
blurred by lack of sleep and has  = 20 seconds.
(a)	How long will it be until you have 99% certainty that you will have resolved from metastability (i.e., figured out how to pass one another)?
(b)	You are not only sleepy, but also ravenously hungry. In fact, you will starve to death if you don’t get going to the cafeteria within 3 minutes. What is the probability that your lab partner will have to drag you to the morgue?

Exercise 3.39 You have built a synchronizer using flip-flops with T0 = 20 ps and
 = 30 ps. Your boss tells you that you need to increase the MTBF by a factor of
10. By how much do you need to increase the clock period?

Exercise 3.40 Ben Bitdiddle invents a new and improved synchronizer in Figure
3.76 that he claims eliminates metastability in a single cycle. He explains that the circuit in box M is an analog “metastability detector” that produces a HIGH output if the input voltage is in the forbidden zone between VIL and VIH. The metastability detector checks to determine whether the first flip-flop has produced a metastable output on D2. If so, it asynchronously resets the flip- flop to produce a good 0 at D2. The second flip-flop then samples D2, always producing a valid logic level on Q. Alyssa P. Hacker tells Ben that there must
be a bug in the circuit, because eliminating metastability is just as impossible as building a perpetual motion machine. Who is right? Explain, showing Ben’s error or showing why Alyssa is wrong.
 


Figure 3.76 “New and improved” synchronizer for Exercise 3.40
 
CLK

D
 
CLK

Q
 


Interview Questions	169

Interview Questions
The following exercises present questions that have been asked at interviews for digital design jobs.

Question 3.1 Draw a state machine that can detect when it has received the serial input sequence 01010.

Question 3.2 Design a serial (one bit at a time) two’s complementer FSM with two inputs, Start and A, and one output, Q. A binary number of arbitrary length is provided to input A, starting with the least significant bit. The corresponding bit of the output appears at Q on the same cycle. Start is asserted for one cycle to initialize the FSM before the least significant bit is provided.

Question 3.3 What is the difference between a latch and a flip-flop? Under what circumstances is each one preferable?

Question 3.4 Design a 5-bit counter finite state machine.

Question 3.5 Design an edge detector circuit. The output should go HIGH for one cycle after the input makes a 0  1 transition.

Question 3.6 Describe the concept of pipelining and why it is used.

Question 3.7 Describe what it means for a flip-flop to have a negative hold time.

Question 3.8 Given signal A, shown in Figure 3.77, design a circuit that produces signal B.


Figure 3.77 Signal waveforms for Question 3.8

Question 3.9 Consider a block of logic between two registers. Explain the timing constraints. If you add a buffer on the clock input of the receiver (the second flip-flop), does the setup time constraint get better or worse?
 
 
 
Hardware Description Languages	4
 





4.1	INTRODUCTION
Thus far, we have focused on designing combinational and sequential digital circuits at the schematic level. The process of finding an efficient set of logic gates to perform a given function is labor intensive and error prone, requiring manual simplification of truth tables or Boolean equa- tions and manual translation of finite state machines (FSMs) into gates. In the 1990’s, designers discovered that they were far more productive if they worked at a higher level of abstraction, specifying just the logical function and allowing a computer-aided design (CAD) tool to produce the optimized gates. The specifications are generally given in a hardware description language (HDL). The two leading hardware description lan- guages are SystemVerilog and VHDL.
SystemVerilog and VHDL are built on similar principles but have different syntax. Discussion of these languages in this chapter is divided into two columns for literal side-by-side comparison, with SystemVerilog on the left and VHDL on the right. When you read the chapter for the first time, focus on one language or the other. Once you know one, you’ll quickly master the other if you need it.
Subsequent chapters show hardware in both schematic and HDL form. If you choose to skip this chapter and not learn one of the HDLs, you will still be able to master the principles of computer organization from the schematics. However, the vast majority of commercial systems are now built using HDLs rather than schematics. If you expect to do digital design at any point in your professional life, we urge you to learn one of the HDLs.

4.1.1	Modules
A block of hardware with inputs and outputs is called a module. An AND gate, a multiplexer, and a priority circuit are all examples of hardware modules. The two general styles for describing module functionality are

Digital Design and Computer Architecture, RISC-V Edition. DOI: 10.1016/B978-0-12-820064-3.00004-0
Copyright © 2022 Elsevier Inc. All rights reserved.
 

4.1	Introduction
4.2	Combinational Logic
4.3	Structural Modeling
4.4	Sequential Logic
4.5	More Combinational Logic
4.6	Finite State Machines
4.7	Data Types*
4.8	Parameterized Modules*
4.9	Testbenches
4.10	Summary
Exercises
Interview Questions



Application  >”hello
Software  world!”
Operating Systems

Architecture
Micro- architecture
Logic	
Digital Circuits
Analog	
Circuits
Devices	 

Physics

171
 
172
 

CHAPTER FOUR
 
Hardware Description Languages
 


behavioral and structural. Behavioral models describe what a module does. Structural models describe how a module is built from simpler pieces; it is an application of hierarchy. The SystemVerilog and VHDL code in HDL Example 4.1 illustrate behavioral descriptions of a module that computes the Boolean function from Example 2.6, y = a bc + ab c + abc. In both languages, the module is named sillyfunction and has three inputs, a, b, and c, and one output, y.


HDL Example 4.1 COMBINATIONAL LOGIC

SystemVerilog	VHDL
module sillyfunction(input logic a, b, c,
output logic y);

assign y = ~a & ~b & ~c |
a & ~b & ~c | a & ~b & c;	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity sillyfunction is port(a, b, c: in STD_LOGIC;
y:	out STD_LOGIC);
end;
endmodule

A SystemVerilog module begins with the module name and a listing of the inputs and outputs. The assign statement describes combinational logic. ~ indicates NOT, & indicates AND, and | indicates OR.
logic signals such as the inputs and outputs are Boolean variables (0 or 1). They may also have floating and undefined values, as discussed in Section 4.2.8.
The logic type was introduced in SystemVerilog. It supersedes the reg type, which was a perennial source of confusion in Verilog. logic should be used everywhere except on signals with multiple drivers. Signals with multiple drivers are called nets and will be explained in Section 4.7.
architecture synth of sillyfunction is begin
y <= (not a and not b and not c) or (a and not b and not c) or
(a and not b and c);
end;

VHDL code has three parts: the library use clause, the entity declaration, and the architecture body. The library use clause will be discussed in Section 4.7.2. The entity declaration lists the module name and its inputs and outputs. The architecture body defines what the module does.
VHDL signals, such as inputs and outputs, must have a type declaration. Digital signals should be declared to be STD_LOGIC type. STD_LOGIC signals can have a value of '0' or '1' as well as floating and undefined values that will be described in Section 4.2.8. The STD_LOGIC type is defined in the IEEE.STD_LOGIC_1164 library, which is why the library must be used.
VHDL lacks a good default order of operations between AND and OR, so Boolean equations should be parenthesized.

A module, as you might expect, is a good application of modularity. It has a well-defined interface, consisting of its inputs and outputs, and it per- forms a specific function. The particular way in which it is coded is unimport- ant to others that might use the module, as long as it performs its function.

4.1.2	Language Origins
Universities are almost evenly split on which of these languages is taught in a first course. Industry is trending toward SystemVerilog, but many companies still use VHDL, so many designers need to be fluent in both.
 
4.1	Introduction	173






Compared to SystemVerilog, VHDL is more verbose and cumbersome, as you might expect of a language developed by committee.
Both languages are fully capable of describing any hardware system, and both have their quirks. The best language to use is the one that is already being used at your site or the one that your customers demand. Most CAD tools today allow the two languages to be mixed so that dif- ferent modules can be described in different languages.

4.1.3	Simulation and Synthesis
The two major purposes of HDLs are logic simulation and synthesis. During simulation, inputs are applied to a module, and the outputs are checked to verify that the module operates correctly. During synthesis, the textual description of a module is transformed into logic gates.

Simulation
Humans routinely make mistakes. Such errors in hardware designs are called bugs. Eliminating the bugs from a digital system is obviously important, especially when customers are paying money and lives depend on the correct operation. Testing a system in the laboratory is time- consuming. Discovering the cause of errors in the lab can be extremely difficult because only signals routed to the chip pins can be observed.

1 The Institute of Electrical and Electronics Engineers (IEEE) is a professional society responsible for many computing standards, including Wi-Fi (802.11), Ethernet (802.3), and floating-point numbers (754).
 
174
 

CHAPTER FOUR
 
Hardware Description Languages
 




Figure 4.1 Simulation waveforms




There is no way to directly observe what is happening inside a chip. Correcting errors after the system is built can be devastatingly expensive. For example, correcting a mistake in a cutting-edge integrated circuit costs more than a million dollars and takes several months. Intel’s infamous FDIV (floating point division) bug in the Pentium processor forced the com- pany to recall chips after they had shipped at a total cost of $475 million in 1984. Logic simulation is essential to test a system before it is built.
Figure 4.1 shows waveforms from a simulation2 of the previous sillyfunction module, demonstrating that the module works cor- rectly. y is TRUE when a, b, and c are 000, 100, or 101, as specified by the Boolean equation.

Synthesis
Logic synthesis transforms HDL code into a netlist describing the hard- ware (e.g., the logic gates and the wires connecting them). The logic syn- thesizer might perform optimizations to reduce the amount of hardware required. The netlist may be a text file, or it may be drawn as a sche- matic to help visualize the circuit. Figure 4.2 shows the results of synthe- sizing the sillyfunction module.3 Notice how the three three-input AND gates are simplified into two two-input AND gates, as we discov- ered in Example 2.6 using Boolean algebra.
Circuit descriptions in HDL resemble code in a programming language. However, you must remember that the code is intended to represent hard- ware. SystemVerilog and VHDL are rich languages with many commands.




Figure 4.2 Synthesized circuit


un8_y

2 The simulations in this chapter were performed with the ModelSim PE Student Edition Version 10.3c. ModelSim was selected because it is used commercially, yet a student ver- sion with a capacity of 10,000 lines of code is freely available.
3 Throughout this chapter, synthesis was performed using Synplify Premier from Synopsys. However, many synthesis tools exist, such as those included in Vivado and Quartus, the freely available Xilinx and Intel design tools for synthesizing HDL to field programmable gate arrays (see Section 5.6.2).
 
4.2 Combinational Logic	175


Not all of these commands can be synthesized into hardware. For exam- ple, a command to print results on the screen during simulation does not translate into hardware. Because our primary interest is to build hardware, we will emphasize a synthesizable subset of the languages. Specifically, we will divide HDL code into synthesizable modules and a testbench. The syn- thesizable modules describe the hardware. The testbench contains code to apply inputs to a module, check whether the output results are correct, and print discrepancies between expected and actual outputs. Testbench code is intended only for simulation and cannot be synthesized.
One of the most common mistakes for beginners is to think of HDL as a computer program rather than as a shorthand for describing digital hardware. If you don’t know approximately what hardware your HDL should synthesize into, you probably won’t like what you get. You might create far more hardware than is necessary, or you might write code that simulates correctly but cannot be implemented in hardware. Instead, think of your system in terms of blocks of combinational logic, registers, and finite state machines. Sketch these blocks on paper and show how they are connected before you start writing code.
In our experience, the best way to learn an HDL is by exam- ple. HDLs have specific ways of describing various classes of logic; these ways are called idioms. This chapter will teach you how to write the proper HDL idioms for each type of block and then how to put the blocks together to produce a working system. When you need to describe a particular kind of hardware, look for a similar example and adapt it to your purpose. We do not attempt to rigorously define all the syntax of the HDLs, because that is deathly boring and it tends to encourage thinking of HDLs as programming languages, not short- hand for hardware. The IEEE SystemVerilog and VHDL specifications, and numerous dry but exhaustive textbooks, contain all of the details, should you find yourself needing more information on a particular topic. (See the Further Readings section at the back of the book.)

4.2	COMBINATIONAL LOGIC
Recall that we are disciplining ourselves to design synchronous sequential circuits, which consist of combinational logic and registers. The outputs of combinational logic depend only on the current inputs. This section describes how to write behavioral models of combinational logic with HDLs.

4.2.1	Bitwise Operators
Bitwise operators act on single-bit signals or on multibit busses. For example, the inv module in HDL Example 4.2 describes four inverters connected to 4-bit busses.
 
176
 

CHAPTER FOUR
 
Hardware Description Languages
 



 
HDL Example 4.2 INVERTERS

SystemVerilog	VHDL
module inv(input logic [3:0] a,
output logic [3:0] y);

assign y = ~a; endmodule
a[3:0] represents a 4-bit bus. The bits, from most significant to least significant, are a[3], a[2], a[1], and a[0]. This is called little-endian order, because the least significant bit has the smallest bit number. We could have named the bus a[4:1], in which case a[4] would have been the most signifi- cant. Or we could have used a[0:3], in which case the bits, from most significant to least significant, would be a[0], a[1], a[2], and a[3]. This is called big-endian order.	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity inv is
port(a: in STD_LOGIC_VECTOR(3 downto 0); y: out STD_LOGIC_VECTOR(3 downto 0));
end;

architecture synth of inv is begin
y <= not a; end;
VHDL uses STD_LOGIC_VECTOR to indicate busses of STD_LOGIC. STD_LOGIC_VECTOR(3 downto 0) represents a 4-bit bus. The bits, from most significant to least significant, are a(3), a(2), a(1), and a(0). This is called little-endian order, because the least significant bit has the smallest bit number. We could have declared the bus to be STD_LOGIC_VECTOR(4 downto 1), in which case bit 4 would have been the most significant. Or we could have written STD_LOGIC_VECTOR(0 to 3), in which case the bits, from most significant to least significant, would be a(0), a(1), a(2), and a(3). This is called big-endian order.

y [3:0]
Figure 4.3 inv synthesized circuit


The endianness of a bus is purely arbitrary. (See the sidebar in Section 6.6.1 for the origin of the term.) Indeed, endianness is also irrel- evant to this example because a bank of inverters doesn’t care what the order of the bits are. Endianness matters only for operators, such as addition, where the sum of one column carries over into the next. Either ordering is acceptable as long as it is used consistently. We will consistently use the little-endian order, [N − 1:0] in SystemVerilog and (N − 1 downto 0) in VHDL, for an N-bit bus.
After each code example in this chapter is a schematic produced
from the SystemVerilog code by the Synplify Premier synthesis tool. Figure 4.3 shows that the inv module synthesizes to a bank of four inverters, indicated by the inverter symbol labeled y[3:0]. The bank of inverters connects to 4-bit input and output busses. Similar hardware is produced from the synthesized VHDL code.
The gates module in HDL Example 4.3 demonstrates bitwise operations acting on 4-bit busses for other basic logic functions.
 
4.2 Combinational Logic	177
HDL Example 4.3 LOGIC GATES
 












































y2[3:0]
 













































y5[3:0]
	[3:0]
 

Figure 4.4 gates synthesized circuit
 
178
 

CHAPTER FOUR
 
Hardware Description Languages
 



4.2.2	Comments and White Space
The gates example showed how to format comments. SystemVerilog and VHDL are not picky about the use of white space (i.e., spaces, tabs, and line breaks). Nevertheless, proper indenting and use of blank lines is helpful to make nontrivial designs readable. Be consistent in your use of capitalization and underscores in signal and module names. This text uses all lower case. Module and signal names must not begin with a digit.





4.2.3	Reduction Operators
Reduction operators imply a multiple-input gate acting on a single bus. HDL Example 4.4 describes an eight-input AND gate with inputs a7, a6,...,a0. Analogous reduction operators exist for OR, XOR, NAND, NOR, and XNOR gates. Recall that a multiple-input XOR performs parity, returning TRUE if an odd number of inputs are TRUE.




HDL Example 4.4 EIGHT-INPUT AND

 
4.2 Combinational Logic	179


y

Figure 4.5 and8 synthesized circuit


4.2.4	Conditional Assignment
Conditional assignments select the output from among alternatives based on an input called the condition. HDL Example 4.5 illustrates a 2:1 multiplexer using conditional assignment.

HDL Example 4.5 2:1 MULTIPLEXER

SystemVerilog	VHDL
The conditional operator ?: chooses, based on a first expres- sion, between a second and third expression. The first expres- sion is called the condition. If the condition is 1, the operator chooses the second expression. If the condition is 0, the opera- tor chooses the third expression.
?: is especially useful for describing a multiplexer because, based on the first input, it selects between two others. The following code demonstrates the idiom for a 2:1 multiplexer with 4-bit inputs and outputs using the conditional operator.
module mux2(input logic [3:0] d0, d1,
input logic	s, output logic [3:0] y);
assign y = s ? d1 : d0; endmodule	Conditional signal assignments perform different operations, depending on some condition. They are especially useful for describing a multiplexer. For example, a 2:1 multiplexer can use conditional signal assignment to select one of two 4-bit inputs.
library IEEE; use IEEE.STD_LOGIC_1164.all; entity mux2 is
port(d0, d1: in STD_LOGIC_VECTOR(3 downto 0); s:	in STD_LOGIC;
y:	out STD_LOGIC_VECTOR(3 downto 0));
end;

architecture synth of mux2 is begin
y <= d1 when s else d0;
end;
If s is 1, then y = d1. If s is 0, then y = d0.
?: is also called a ternary operator because it takes three inputs. It is used for the same purpose in the C and Java programming languages.	The conditional signal assignment sets y to d1 if s is 1. Other- wise, it sets y to d0. Note that prior to the 2008 revision of VHDL, one had to write when s = '1' rather than when s.

y[3:0]
Figure 4.6 mux2 synthesized circuit

 
180
 

CHAPTER FOUR
 
Hardware Description Languages
 


HDL Example 4.6 shows a 4:1 multiplexer based on the same princi- ple as the 2:1 multiplexer in HDL Example 4.5. Figure 4.7 shows the schematic for the 4:1 multiplexer produced by the synthesis tool. The software uses a different multiplexer symbol than this text has shown so far. The multiplexer has multiple data (d) and one-hot enable (e) inputs. When one of the enables is asserted, the associated data is passed to the output. For example, when s[1] = s[0] = 0, the bottom AND gate, un1_s_5, produces a 1, enabling the bottom input of the multiplexer and causing it to select d0[3:0].

HDL Example 4.6 4:1 MULTIPLEXER

SystemVerilog	VHDL
A 4:1 multiplexer can select one of four inputs, using nested conditional operators.	A 4:1 multiplexer can select one of four inputs, using multiple else clauses in the conditional signal assignment.
module mux4(input logic [3:0] d0, d1, d2, d3, input logic [1:0] s,
output logic [3:0] y);

assign y = s[1] ? (s[0] ? d3 : d2)
: (s[0] ? d1 : d0);
endmodule

If s[1] is 1, then the multiplexer chooses the first expression, (s[0] ? d3 : d2). This expression, in turn, chooses either d3 or d2 based on s[0] (y = d3 if s[0] is 1 and d2 if s[0] is 0). If s[1] is 0, then the multiplexer similarly chooses the second expression, which gives either d1 or d0 based on s[0].	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity mux4 is port(d0, d1,
d2, d3: in STD_LOGIC_VECTOR(3 downto 0); s:	in STD_LOGIC_VECTOR(1 downto 0); y:	 out STD_LOGIC_VECTOR(3 downto 0));
end;

architecture synth1 of mux4 is begin
y <= d0 when s = "00" else d1 when s = "01" else d2 when s = "10" else d3;
end;
	VHDL also supports selected signal assignment statements to provide a shorthand when selecting from one of several possi- bilities. This is analogous to using a switch/case statement in place of multiple if/else statements in some programming languages. The 4:1 multiplexer can be rewritten with selected signal assignment as follows:
	architecture synth2 of mux4 is begin
with s select y <= d0 when "00",
d1 when "01",
d2 when "10", d3 when others;
end;


4.2.5 Internal Variables
Often it is convenient to break a complex function into intermediate steps. For example, a full adder, which will be described in Section 5.2.1,
 
4.2 Combinational Logic	181













Figure 4.7 mux4 synthesized circuit








un1_s_5


is a circuit with three inputs and two outputs defined by the following equations:
 
S = A ⊕ B ⊕ Cin
 
(4.1)
 
Cout
 
= AB + ACin + BCin
 
If we define intermediate signals, P and G,

P = A ⊕ B G = AB
we can rewrite the full adder as follows:
S = P ⊕ Cin
 

(4.2)


(4.3)
 
Cout
 
= G + PCin
 
P and G are called internal variables because they are neither inputs nor outputs; rather, they are used only internal to the module. They are similar to local variables in programming languages. HDL Example 4.7 shows how they are used in HDLs.
HDL assignment statements (assign in SystemVerilog and <= in VHDL) take place concurrently. This is different from conventional pro- gramming languages, such as C or Java, in which statements are evaluated in the order in which they are written. In a conventional language, it is
 
182
 

CHAPTER FOUR
 
Hardware Description Languages
 



 
HDL Example 4.7 FULL ADDER


Figure 4.8 fulladder synthesized circuit



important that S = P Cin comes after P = A B because statements are executed sequentially. In an HDL, the order does not matter. Like hard- ware, HDL assignment statements are evaluated whenever the inputs,
signals on the right-hand side, change their value regardless of the order in which the assignment statements appear in a module.

4.2.6	Precedence
Notice that we parenthesized the cout computation in HDL Example 4.7 to define the order of operations as Cout = G + (P · Cin) rather than Cout = (G + P) · Cin. If we had not used parentheses, the default oper- ation order would be defined by the language. HDL Example 4.8
 
4.2 Combinational Logic	183
 



HDL Example 4.8 OPERATOR PRECEDENCE
SystemVerilog
Table 4.1 SystemVerilog operator precedence
 





VHDL
 






Table 4.2 VHDL operator precedence
 

Op				Meaning
H	not		NOT
i
g h	*, /, mod, rem		MUL, DIV, MOD, REM
e
s	+, –		PLUS, MINUS
t	rol, ror, srl, sll		Rotate, Shift logical

L	<,	<=,	>,	>=	Relative Comparison
o	=,	/=			Equality Comparison
w
e s t	and, or, nand, nor, xor, xnor		Logical Operations

 



The operator precedence for SystemVerilog is much like you would expect in other programming languages. In particular, AND has precedence over OR. We could take advantage of this precedence to eliminate the parentheses:
assign cout = g | p & cin;
 
Multiplication has precedence over addition in VHDL, as you would expect. However, unlike SystemVerilog, all of the logical operations (and, or, etc.) have equal precedence, unlike what one might expect in Boolean algebra. Thus, parentheses are necessary. Otherwise, cout <= g or p and cin would be interpreted from left to right as cout <= (g or p) and cin.
 



specifies operator precedence from highest to lowest for each language. The tables include arithmetic, shift, and comparison operators that will be defined in Chapter 5.

4.2.7	Numbers
Numbers can be specified in binary, octal, decimal, or hexadecimal (bases 2, 8, 10, and 16, respectively). The size, that is, the number of bits, may be given optionally, and leading zeros are inserted to reach this size. Underscores in numbers are ignored and can be helpful in breaking long numbers into more readable chunks. HDL Example 4.9 explains how numbers are written in each language.
 
184
 

CHAPTER FOUR
 
Hardware Description Languages
 



 
HDL Example 4.9 NUMBERS

 
SystemVerilog
The format for declaring constants is N'Bvalue, where N is the size in bits, B is a letter indicating the base, and value gives the value. For example, 9'h25 indicates a 9-bit number with a value of 2516 = 3710 = 0001001012. SystemVerilog supports 'b for binary, 'o for octal, 'd for decimal, and 'h for hexadecimal.
If the base is omitted, it defaults to decimal. If the size is not given, the number is assumed to have as many bits as the expression in which it is being used. Zeros are automatically padded on the front of the number to bring it up to full size. For example, if w is a 6-bit bus, assign w = 'b11 gives w the value 000011. It is better practice to explicitly give the size. An exception is that '0 and '1 are SystemVerilog idioms to fill all of the bits with 0 and 1, respectively.

Table 4.3 SystemVerilog numbers
 
VHDL
In VHDL, STD_LOGIC numbers are written in binary and enclosed in single quotes: '0' and'1' indicate logic 0 and 1. The format for declaring STD_LOGIC_VECTOR constants is NB"value", where N is the size in bits, B is a letter indicating the base, and value gives the value. For example, 9X"25" indicates a 9-bit number with a value of 2516 = 3710 = 0001001012. VHDL 2008 supports B for binary, O for octal, D for decimal, and X for hexadecimal.
If the base is omitted, it defaults to binary. If the size is not given, the number is assumed to have a size matching the number of bits specified in the value. For example, y <= X"7B" requires that y be an 8-bit signal. If y has more bits, VHDL does not pad the number with 0’s on the left. Instead, an error occurs during compilation. others => '0' and others => '1' are VHDL idioms to fill all of the bits with 0 and 1, respectively.
Table 4.4 VHDL numbers
 

 	 

	'b11	?	2	3	000 … 0011			B"11"	2	2	3	11	
	8'b11	8	2	3	00000011			8B"11"	8	2	3	00000011	
	8'b1010_1011	8	2	171	10101011			8B"1010_1011"	8	2	171	10101011	
	3'd6	3	10	6	110			3D"6"	3	10	6	110	
	6'o42	6	8	34	100010			6O"42"	6	8	34	100010	
	8'hAB	8	16	171	10101011			8X"AB"	8	16	171	10101011	
	42	?	10	42	00 … 0101010			"101"	3	2	5	101	
													
								B"101"	3	2	5	101	
								X"AB"	8	16	171	10101011	
													

4.2.8 Z’s and X’s
HDLs use z to indicate a floating value. z is particularly useful for describ- ing a tristate buffer, whose output floats when the enable is 0. Recall from Section 2.6.2 that a bus can be driven by several tristate buffers, exactly one of which should be enabled. HDL Example 4.10 shows the idiom for a tristate buffer. If the buffer is enabled, the output is the same as the input. If the buffer is disabled, the output is assigned a floating value (z).
Similarly, HDLs use x to indicate an invalid logic level. If a bus is simultaneously driven to 0 and 1 by two enabled tristate buffers (or other
gates), the result is x, indicating contention. If all of the tristate buffers driving a bus are simultaneously OFF, the bus will float, indicated by z.
 
4.2 Combinational Logic	185
At the start of simulation, state nodes such as flip-flop outputs are initialized to an unknown state (x in SystemVerilog and u in VHDL). This is helpful to track errors caused by forgetting to reset a flip-flop before its output is used.

HDL Example 4.10 TRISTATE BUFFER

SystemVerilog	VHDL
module tristate(input logic [3:0] a,
input logic	en, output tri [3:0] y);
assign y = en ? a : 4'bz; endmodule
Notice that y is declared as tri rather than logic. logic signals can only have a single driver. Tristate busses can have multiple drivers, so they should be declared as a net. Two types of nets in SystemVerilog are called tri and trireg. Typically, exactly one driver on a net is active at a time, and the net takes on that value. If no driver is active, a tri floats (z), while a trireg retains the previous value. If no type is specified for an input or output, tri is assumed. Also, note that a tri output from a module can be used as a logic input to another module. Section 4.7 further discusses nets with multiple drivers.	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity tristate is
port(a: in STD_LOGIC_VECTOR(3 downto 0); en: in STD_LOGIC;
y: out STD_LOGIC_VECTOR(3 downto 0));
end;

architecture synth of tristate is begin
y <= a when en else "ZZZZ"; end;

y_1[3:0]
Figure 4.9 tristate synthesized circuit

If a gate receives a floating input, it may produce an x output when it can’t determine the correct output value. Similarly, if it receives an illegal or uninitialized input, it may produce an x output. HDL Example 4.11

HDL Example 4.11 TRUTH TABLES WITH UNDEFINED AND FLOATING INPUTS

 
186
 

CHAPTER FOUR
 
Hardware Description Languages
 





 	 

HDL Example 4.12 BIT SWIZZLING


shows how SystemVerilog and VHDL combine these different signal values in logic gates.
Seeing x or u values in simulation is almost always an indication of a bug or bad coding practice. In the synthesized circuit, this corresponds to a floating gate input, uninitialized state, or contention. The x or u may be inter- preted randomly by the circuit as 0 or 1, leading to unpredictable behavior.
4.2.9	Bit Swizzling
Often it is necessary to operate on a subset of a bus or to concatenate (join together) signals to form busses. These operations are collectively known as bit swizzling. In HDL Example 4.12, y is given the 9-bit value c2c1d0d0d0c0101 using bit swizzling operations.
4.2.10	Delays
HDL statements may be associated with delays specified in arbitrary units. They are helpful during simulation to predict how fast a circuit will work (if you specify meaningful delays) and for debugging purposes to
 
4.2 Combinational Logic	187
understand cause and effect (deducing the source of a bad output is tricky if all signals change simultaneously in the simulation results). These delays are ignored during synthesis; the delay of a gate produced by the synthe- sizer depends on its tpd and tcd specifications, not on numbers in HDL code. HDL Example 4.13 adds delays to the original function from HDL Example 4.1, y = a bc + ab c + abc. It assumes that inverters have a delay of 1 ns, three-input AND gates have a delay of 2 ns, and three-input OR gates have a delay of 4 ns. Figure 4.10 shows the simulation waveforms, with y lagging 7 ns after the inputs. Note that y is initially unknown at
the beginning of the simulation.
HDL Example 4.13 LOGIC GATES WITH DELAYS

SystemVerilog	VHDL
'timescale 1ns/1ps	library IEEE; use IEEE.STD_LOGIC_1164.all;
module example(input logic a, b, c,
output logic y);

logic ab, bb, cb, n1, n2, n3;	entity example is
port(a, b, c: in STD_LOGIC; y:	out STD_LOGIC);
end;
assign #1 {ab, bb, cb} = ~{a, b, c}; assign #2 n1 = ab & bb & cb;
assign #2 n2 = a & bb & cb; assign #2 n3 = a & bb & c; assign #4 y = n1 | n2 | n3;
endmodule

SystemVerilog files can include a timescale directive that indicates the value of each time unit. The statement is of the form 'timescale unit/precision. In this file, each unit is 1 ns and the simulation has 1 ps precision. If no timescale directive is given in the file, a default unit and precision (usually 1 ns for both) are used. In SystemVerilog, a # symbol is used to indicate the number of units of delay. It can be placed in assign statements, as well as nonblocking (<=) and blocking (=) assignments, which will be discussed in Section 4.5.4.
architecture synth of example is
signal ab, bb, cb, n1, n2, n3: STD_LOGIC; begin
ab <= not a after 1 ns; bb <= not b after 1 ns; cb <= not c after 1 ns;
n1 <= ab and bb and cb after 2 ns; n2 <= a and bb and cb after 2 ns; n3 <= a and bb and c after 2 ns;
y <= n1 or n2 or n3 after 4 ns; end;
In VHDL, the after clause is used to indicate delay. The units, in this case, are specified as nanoseconds.

Figure 4.10 Example simulation waveforms with delays (from the ModelSim simulator)
 
188
 

CHAPTER FOUR
 
Hardware Description Languages
 


4.3 STRUCTURAL MODELING
The previous section discussed behavioral modeling, describing a module in terms of the relationships between inputs and outputs. This section examines structural modeling, which describes a module in terms of how it is composed of simpler modules.
For example, HDL Example 4.14 shows how to assemble a 4:1 multi- plexer from three 2:1 multiplexers. Each copy of the 2:1 multiplexer is called



HDL Example 4.14 STRUCTURAL MODEL OF 4:1 MULTIPLEXER

SystemVerilog	VHDL
module mux4(input logic [3:0] d0, d1, d2, d3, input logic [1:0] s,
output logic [3:0] y); logic [3:0] low, high;
mux2 lowmux(d0, d1, s[0], low); mux2 highmux(d2, d3, s[0], high); mux2 finalmux(low, high, s[1], y);
endmodule

The three mux2 instances are called lowmux, highmux, and finalmux. The mux2 module must be defined elsewhere in the SystemVerilog code—see HDL Example 4.5, 4.15, or 4.34.
library IEEE; use IEEE.STD_LOGIC_1164.all;

entity mux4 is port(d0, d1,
d2, d3: in STD_LOGIC_VECTOR(3 downto 0); s:	 in STD_LOGIC_VECTOR(1 downto 0); y:	out STD_LOGIC_VECTOR(3 downto 0));
end;

architecture struct of mux4 is component mux2
port(d0,
d1:in STD_LOGIC_VECTOR(3 downto 0); s: in STD_LOGIC;
y: out STD_LOGIC_VECTOR(3 downto 0)); end component;
signal low, high: STD_LOGIC_VECTOR(3 downto 0); begin
lowmux:	mux2 port map(d0, d1, s(0), low); highmux: mux2 port map(d2, d3, s(0), high); finalmux: mux2 port map(low, high, s(1), y);
end;
	The architecture must first declare the mux2 ports using the component declaration statement. This allows VHDL tools to check that the component you wish to use has the same ports as the entity that was declared somewhere else in another entity statement, preventing errors caused by changing the entity but not the instance. However, component declaration makes VHDL code rather cumbersome.
Note that this architecture of mux4 was named struct, whereas architectures of modules with behavioral descriptions from Section 4.2 were named synth. VHDL allows multiple architectures (implementations) for the same entity; the archi- tectures are distinguished by name. The names themselves have no significance to the CAD tools, but struct and synth are common. Synthesizable VHDL code generally contains only one architecture for each entity, so we will not discuss the VHDL syntax to configure which architecture is used when multiple architectures are defined.
 
4.3	Structural Modeling	189


Figure 4.11 mux4 synthesized circuit


an instance. Multiple instances of the same module are distinguished by distinct names, in this case lowmux, highmux, and finalmux. This is an example of regularity, in which the 2:1 multiplexer is reused many times.
HDL Example 4.15 uses structural modeling to construct a 2:1 mul- tiplexer from a pair of tristate buffers. Building logic out of tristates is not recommended, however.

HDL Example 4.15 STRUCTURAL MODEL OF 2:1 MULTIPLEXER

SystemVerilog	VHDL
module mux2(input logic [3:0] d0, d1,
input logic		s, output tri	[3:0] y);
tristate t0(d0, ~s, y); tristate t1(d1, s, y);
endmodule	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity mux2 is
port(d0, d1: in STD_LOGIC_VECTOR(3 downto 0); s:	in STD_LOGIC;
y:	out STD_LOGIC_VECTOR(3 downto 0));
end;
In SystemVerilog, expressions such as ~s are permitted in the port list for an instance. Arbitrarily complicated expressions are legal but discouraged because they make the code difficult to read.	architecture struct of mux2 is component tristate
port(a: in STD_LOGIC_VECTOR(3 downto 0); en: in STD_LOGIC;
y: out STD_LOGIC_VECTOR(3 downto 0)); end component;
signal sbar: STD_LOGIC; begin
sbar <= not s;
t0: tristate port map(d0, sbar, y); t1: tristate port map(d1, s, y);
end;
	In VHDL, expressions such as not s are not permitted in the port map for an instance. Thus, sbar must be defined as a separate signal.
 
190
 

CHAPTER FOUR
 
Hardware Description Languages
 



 
Figure 4.12 mux2 synthesized circuit


HDL Example 4.16 shows how modules can access part of a bus. An 8-bit-wide 2:1 multiplexer is built using two of the 4-bit 2:1 multiplexers already defined, operating on the low and high nibbles of the byte.
In general, complex systems are designed hierarchically. The overall system is described structurally by instantiating its major components. Each of these components is described structurally from its building blocks and so forth recursively until the pieces are simple enough to describe behaviorally. It is good style to avoid (or at least to minimize) mixing structural and behavioral descriptions within a single module.

HDL Example 4.16 ACCESSING PARTS OF BUSSES

SystemVerilog	VHDL
module mux2_8(input logic [7:0] d0, d1,
input logic	s, output logic [7:0] y);
mux2 lsbmux (d0[3:0], d1[3:0], s, y[3:0]);
mux2 msbmux(d0[7:4], d1[7:4], s, y[7:4]); endmodule	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity mux2_8 is
port(d0, d1: in STD_LOGIC_VECTOR(7 downto 0); s:	in STD_LOGIC;
y:	out STD_LOGIC_VECTOR(7 downto 0));
end;
	architecture struct of mux2_8 is component mux2
port(d0, d1: in STD_LOGIC_VECTOR(3 downto 0); s:	in STD_LOGIC;
y:	out STD_LOGIC_VECTOR(3 downto 0)); end component;
begin
	lsbmux: mux2
port map(d0(3 downto 0), d1(3 downto 0), s, y(3 downto 0));
msbmux: mux2
port map(d0(7 downto 4), d1(7 downto 4), s, y(7 downto 4));
end;
 
4.4 Sequential Logic	191


Figure 4.13 mux2_8 synthesized circuit



4.4	SEQUENTIAL LOGIC
HDL synthesizers recognize certain idioms and turn them into specific sequential circuits. Other coding styles may simulate correctly but syn- thesize into circuits with blatant or subtle errors. This section presents the proper idioms to describe registers and latches.

4.4.1	Registers
The vast majority of modern commercial systems are built with registers using positive edge-triggered D flip-flops. HDL Example 4.17 shows the idiom for such flip-flops.
In SystemVerilog always statements and VHDL process state- ments, signals keep their old value until an event in the sensitivity list takes place that explicitly causes them to change. Hence, such code, with appropriate sensitivity lists, can be used to describe sequential circuits with memory. For example, the flip-flop includes only clk in the sensi- tive list. It remembers its old value of q until the next rising edge of the clk, even if d changes in the interim.
In contrast, SystemVerilog continuous assignment statements (assign) and VHDL concurrent assignment statements (<=) are reeval- uated whenever any of the inputs on the right-hand side change. Therefore, such code necessarily describes combinational logic.
 
192
 

CHAPTER FOUR
 
Hardware Description Languages
 



 
HDL Example 4.17 REGISTER

SystemVerilog	VHDL
module flop(input logic	clk,
input logic [3:0] d, output logic [3:0] q);
always_ff @(posedge clk) q <= d;
endmodule	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity flop is
port(clk: in STD_LOGIC;
d: in STD_LOGIC_VECTOR(3 downto 0); q: out STD_LOGIC_VECTOR(3 downto 0));
end;
In general, a SystemVerilog always statement is written in the form
always @(sensitivity list) statement;
The statement is executed only when the event specified in the sensitivity list occurs. In this example, the statement is q <= d (pronounced “q gets d”). Hence, the flip-flop copies d to q on the positive edge of the clock and otherwise remembers the old state of q. Note that sensitivity lists are also referred to as stimulus lists.
<= is called a nonblocking assignment. Think of it as a regular = sign for now; we’ll return to the more subtle points in Section 4.5.4. Note that <= is used instead of assign inside an always statement.
As will be seen in subsequent sections, always statements can be used to imply flip-flops, latches, or combinational logic, depending on the sensitivity list and statement. Because of this flexibility, it is easy to produce the wrong hardware inadvertently. SystemVerilog introduces always_ff, always_latch, and always_comb to reduce the risk of common errors. always_ff behaves like always but is used exclusively to imply flip-flops and allows tools to produce a warning if
anything else is implied.	architecture synth of flop is begin
process(clk) begin
if rising_edge(clk) then q <= d;
end if; end process;
end;

A VHDL process is written in the form
process(sensitivity list) begin statement;
end process;

The statement is executed when any of the variables in the sensitivity list change. In this example, the if statement checks whether the change was a rising edge on clk. If so, then q <= d (pronounced “q gets d”). Hence, the flip-flop copies d to q on the positive edge of the clock and otherwise remembers the old state of q.
An alternative VHDL idiom for a flip-flop is
process(clk) begin
if clk'event and clk = '1' then q <= d;
end if; end process;
	rising_edge(clk) is synonymous with clk'event and
	clk = '1'.

Figure 4.14 flop synthesized circuit


4.4.2 Resettable Registers
When simulation begins or power is first applied to a circuit, the output of a flop or register is unknown. This is indicated with x in SystemVerilog and u in VHDL. Generally, it is good practice to use resettable registers so that on powerup you can put your system in a known state. The reset may be either asynchronous or synchronous. Recall that asynchronous reset occurs immediately, whereas synchronous reset clears the output only on
 
4.4 Sequential Logic	193
the next rising edge of the clock. HDL Example 4.18 demonstrates the idi- oms for flip-flops with asynchronous and synchronous resets. Note that distinguishing synchronous and asynchronous reset in a schematic can be difficult.
 


HDL Example 4.18 RESETTABLE REGISTER

SystemVerilog
module flopr(input logic	clk,
input logic	reset, input logic [3:0] d, output logic [3:0] q);
// asynchronous reset
always_ff @(posedge clk, posedge reset) if (reset) q <= 4'b0;
else	q <= d; endmodule
module flopr(input logic	clk,
input logic	reset, input logic [3:0] d, output logic [3:0] q);
// synchronous reset always_ff @(posedge clk)
if (reset) q <= 4'b0; else	q <= d;
endmodule

Multiple signals in an always statement sensitivity list are separated with a comma or the word or. Notice that posedge reset is in the sensitivity list on the asynchronously resettable flop, but not on the synchronously resettable flop. Thus, the asynchronously resettable flop immediately responds to a rising edge on reset, but the synchronously resettable flop responds to reset only on the rising edge of the clock.
Because the modules have the same name, flopr, you may include only one or the other in your design. If you wanted to use both, you would need to rename one of the modules.
 




VHDL
library IEEE; use IEEE.STD_LOGIC_1164.all; entity flopr is
port(clk, reset: in STD_LOGIC;
d:	in STD_LOGIC_VECTOR(3 downto 0);
q:	out STD_LOGIC_VECTOR(3 downto 0));
end;

architecture asynchronous of flopr is begin
process(clk, reset) begin if reset then
q <= "0000";
elsif rising_edge(clk) then q <= d;
end if; end process;
end;
library IEEE; use IEEE.STD_LOGIC_1164.all; entity flopr is
port(clk, reset: in STD_LOGIC;
d:	in STD_LOGIC_VECTOR(3 downto 0);
q:	out STD_LOGIC_VECTOR(3 downto 0));
end;

architecture synchronous of flopr is begin
process(clk) begin
if rising_edge(clk) then if reset then q <= "0000"; else q <= d;
end if; end if;
end process; end;
Multiple signals in a process sensitivity list are separated with a comma. Notice that reset is in the sensitivity list on the asynchronously resettable flop but not on the synchronously resettable flop. Thus, the asynchronously resettable flop immediately responds to a rising edge on reset, but the synchronously resettable flop responds to reset only on the rising edge of the clock.
As mentioned earlier, the name of the architecture (asynchronous or synchronous, in this example) is ignored by the VHDL tools but may be helpful to the human reading the code. Because both architectures describe the entity flopr, you may include only one or the other in your design. If you wanted to use both, you would need to rename one of the modules.
 
194
 

CHAPTER FOUR
 
Hardware Description Languages
 



 


(a)


	clk
d[3:0]
reset


(b)

Figure 4.15 flopr synthesized circuit (a) asynchronous reset, (b) synchronous reset



4.4.3	Enabled Registers
Enabled registers respond to the clock only when the enable is asserted. HDL Example 4.19 shows an asynchronously resettable enabled register that retains its old value if both reset and en are FALSE.


HDL Example 4.19 RESETTABLE ENABLED REGISTER

SystemVerilog	VHDL
module flopenr(input logic	clk,
input logic	reset,
input logic	en, input logic [3:0] d, output logic [3:0] q);
// asynchronous reset
always_ff @(posedge clk, posedge reset) if	(reset) q <= 4'b0;
else if (en)	q <= d; endmodule	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity flopenr is port(clk,
reset,
en: in STD_LOGIC;
d: in STD_LOGIC_VECTOR(3 downto 0); q: out STD_LOGIC_VECTOR(3 downto 0));
end;

architecture asynchronous of flopenr is
–– asynchronous reset begin
process(clk, reset) begin if reset then
q <= "0000";
elsif rising_edge(clk) then if en then
q <= d; end if;
end if; end process;
end;
 
4.4 Sequential Logic	195



 
Figure 4.16 flopenr synthesized circuit


 
4.4.4	Multiple Registers
A single always/process statement can be used to describe multiple pieces of hardware. For example, consider the synchronizer from Section
3.5.5 made of two back-to-back flip-flops, as shown in Figure 4.17. HDL Example 4.20 describes the synchronizer. On the rising edge of clk, d is copied to n1. At the same time, n1 is copied to q.
 

CLK	CLK


D	Q


Figure 4.17 Synchronizer circuit
 


 
HDL Example 4.20  SYNCHRONIZER

SystemVerilog	VHDL
module sync(input logic clk,
input logic d, output logic q);
logic n1;

always_ff @(posedge clk) begin
n1 <= d; // nonblocking q <= n1; // nonblocking
end endmodule
Notice that the begin/end construct is necessary because multiple statements appear in the always statement. This is analogous to {} in C or Java. The begin/end was not needed in the flopr example because if/else counts as a single statement.	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity sync is
port(clk: in STD_LOGIC; d: in STD_LOGIC;
q: out STD_LOGIC);
end;

architecture good of sync is signal n1: STD_LOGIC;
begin
process(clk) begin
if rising_edge(clk) then n1 <= d;
q <= n1; end if;
end process; end;
	n1 must be declared as a signal because it is an internal signal used in the module.

n1	q

Figure 4.18 sync synthesized circuit

 
196
 

CHAPTER FOUR
 
Hardware Description Languages
 


4.4.5 Latches
Recall from Section 3.2.2 that a D latch is transparent when the clock is HIGH, allowing data to flow from input to output. The latch becomes opaque when the clock is LOW, retaining its old state. HDL Example
4.21 shows the idiom for a D latch.
Not all synthesis tools support latches well. Unless you know that your tool does support latches and you have a good reason to use them, avoid them and use edge-triggered flip-flops instead. Furthermore, take care that your HDL does not imply any unintended latches, something that is easy to do if you aren’t attentive. Many synthesis tools warn you when a latch is created; if you didn’t expect one, track down the bug in your HDL. And if you don’t know whether you intended to have a latch or not, you are probably approaching HDLs like a programming language and have bigger problems lurking.

4.5 MORE COMBINATIONAL LOGIC
In Section 4.2, we used assignment statements to describe combinational logic behaviorally. SystemVerilog always statements and VHDL process

HDL Example 4.21 D LATCH

SystemVerilog	VHDL
module latch(input logic	clk,
input logic [3:0] d, output logic [3:0] q);
always_latch
if (clk) q <= d; endmodule	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity latch is
port(clk: in STD_LOGIC;
d: in STD_LOGIC_VECTOR(3 downto 0); q: out STD_LOGIC_VECTOR(3 downto 0));
end;
always_latch is equivalent to always @(clk, d) and is the pre- ferred idiom for describing a latch in SystemVerilog. It evaluates whenever clk or d changes. If clk is HIGH, d flows through to q, so this code describes a positive level-sensitive latch. Otherwise, q keeps its old value. SystemVerilog can generate a warning if the always_latch block doesn’t imply a latch.	architecture synth of latch is begin
process(clk, d) begin if clk = '1' then
q <= d; end if;
end process; end;
	The sensitivity list contains both clk and d, so the process evaluates whenever clk or d changes. If clk is HIGH, d flows through to q.

[3:0]
d[3:0]
	 clk



Figure 4.19 latch synthesized circuit

 
4.5 More Combinational Logic	197


HDL Example 4.22 INVERTER USING always/process

SystemVerilog	VHDL
module inv(input logic [3:0] a,
output logic [3:0] y);

always_comb y = ~a;
endmodule	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity inv is
port(a: in STD_LOGIC_VECTOR(3 downto 0); y: out STD_LOGIC_VECTOR(3 downto 0));
end;
always_comb reevaluates the statements inside the always statement whenever any of the signals on the right-hand side of <= or = in the always statement change. In this case, it is equivalent to always @(a) but is better because it avoids mistakes if signals in the always statement are renamed or added. If the code inside the always block is not combinational logic, SystemVerilog will report a warning. always_comb is equivalent to always @(*) but is preferred in SystemVerilog.
The = in the always statement is called a blocking assign- ment, in contrast to the <= nonblocking assignment. In SystemVerilog, it is good practice to use blocking assignments for combinational logic and nonblocking assignments for sequential logic. This will be discussed further in Section 4.5.4.
architecture proc of inv is begin
process(all) begin y <= not a;
end process; end;
process(all) reevaluates the statements inside the process whenever any of the signals in the process change. It is equivalent to process(a) but is better because it avoids mistakes if signals in the process are renamed or added.
The begin and end process statements are required in VHDL even though the process contains only one assignment.

statements are used to describe sequential circuits because they remember the old state when no new state is prescribed. However, always/process statements can also be used to describe combinational logic behaviorally if the sensitivity list is written to respond to changes in all of the inputs and the body prescribes the output value for every possible input combi- nation. HDL Example 4.22 uses always/process statements to describe a bank of four inverters (see Figure 4.3 for the synthesized circuit).
HDLs support blocking and nonblocking assignments in an always/process statement. A group of blocking assignments are eval- uated in the order in which they appear in the code, just as one would expect in a standard programming language. A group of nonblocking assignments are evaluated concurrently; all of the statements are evalu- ated before any of the signals on the left-hand sides are updated.
HDL Example 4.23 defines a full adder using intermediate sig- nals p and g to compute s and cout. It produces the same circuit from Figure 4.8, but uses always/process statements in place of assignment statements.
HDL Examples 4.22 and 4.23 are poor applications of always/ process statements for modeling combinational logic because they require more lines than the equivalent approach with assignment state- ments from HDL Examples 4.2 and 4.7. However, case and if state- ments are convenient for modeling more complicated combinational logic. case and if statements must appear within always/process statements and are examined in the next sections.
 
198
 

CHAPTER FOUR
 
Hardware Description Languages
 


 




HDL Example 4.23 FULL ADDER USING always/process

SystemVerilog	VHDL
module fulladder(input logic a, b, cin,
output logic s, cout);
logic p, g;

always_comb begin
p = a ^ b;	// blocking
g = a & b;	// blocking
s = p ^ cin;	// blocking cout = g | (p & cin); // blocking
end endmodule
In this case, always @(a, b, cin) would have been equivalent to always_comb. However, always_comb is better because it avoids common mistakes of missing signals in the sensitivity list.
For reasons that will be discussed in Section 4.5.4, it is best to use blocking assignments for combinational logic. This example uses blocking assignments, first computing p, then g, then s, and, finally, cout.	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity fulladder is
port(a, b, cin: in STD_LOGIC; s, cout: out STD_LOGIC);
end;

architecture synth of fulladder is begin
process(all)
variable p, g: STD_LOGIC; begin
p := a xor b; –– blocking g := a and b; –– blocking s <= p xor cin;
cout <= g or (p and cin); end process;
end;

In this case, process(a, b, cin) would have been equivalent to process(all). However, process(all) is better because it avoids common mistakes of missing signals in the sensitivity list. For reasons that will be discussed in Section 4.5.4, it is best to use blocking assignments for intermediate variables in combinational logic. This example uses blocking assignments for p and g so that they get their new values before being used to
compute s and cout that depend on them.
Because p and g appear on the left-hand side of a blocking assignment (:=) in a process statement, they must be declared to be variable rather than signal. The variable declaration appears before the begin in the process where the variable is used.
 
4.5 More Combinational Logic	199

4.5.1 Case Statements
A better application of using the always/process statement for combina- tional logic is a seven-segment display decoder that takes advantage of the case statement that must appear inside an always/process statement.
As you might have noticed in the seven-segment display decoder of Example 2.10, the design process for large blocks of combinational logic is tedious and prone to error. HDLs offer a great improvement, allow- ing you to specify the function at a higher level of abstraction and then automatically synthesize the function into gates. HDL Example 4.24 uses case statements to describe a seven-segment display decoder based on its truth table. The case statement performs different actions depending on the value of its input. A case statement implies combinational logic if all

HDL Example 4.24 SEVEN-SEGMENT DISPLAY DECODER

SystemVerilog	VHDL
module sevenseg(input logic [3:0] data,
output logic [6:0] segments);
always_comb case(data)
//	abc_defg
0:	segments = 7'b111_1110;
1:	segments = 7'b011_0000;
2:	segments = 7'b110_1101;
3:	segments = 7'b111_1001;
4:	segments = 7'b011_0011;
5:	segments = 7'b101_1011;
6:	segments = 7'b101_1111;
7:	segments = 7'b111_0000;
8:	segments = 7'b111_1111;
9:	segments = 7'b111_0011; default: segments = 7'b000_0000;
endcase endmodule
The case statement checks the value of data. When data is 0, the statement performs the action after the colon, setting segments to 1111110. The case statement similarly checks other data values up to 9 (note the use of the default base, base 10).
The default clause is a convenient way to define the output for all cases not explicitly listed, guaranteeing combinational logic.
In SystemVerilog, case statements must appear inside
always statements.	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity seven_seg_decoder is
port(data:	in STD_LOGIC_VECTOR(3 downto 0); segments: out STD_LOGIC_VECTOR(6 downto 0));
end;

architecture synth of seven_seg_decoder is begin
process(all) begin case data is
––	abcdefg
when X"0" => segments <= "1111110"; when X"1" => segments <= "0110000"; when X"2" => segments <= "1101101"; when X"3" => segments <= "1111001"; when X"4" => segments <= "0110011"; when X"5" => segments <= "1011011"; when X"6" => segments <= "1011111"; when X"7" => segments <= "1110000"; when X"8" => segments <= "1111111"; when X"9" => segments <= "1110011"; when others => segments <= "0000000";
end case; end process;
end;

The case statement checks the value of data. When data is 0, the statement performs the action after the =>, setting segments to 1111110. The case statement similarly checks other data values up to 9 (note the use of X for hexadecimal numbers). The others clause is a convenient way to define the output for all cases not explicitly listed, guaranteeing combinational logic.
Unlike SystemVerilog, VHDL supports selected signal assignment statements (see HDL Example 4.6), which are much like case statements but can appear outside processes. Thus, there is less reason to use processes to describe combinational logic.
 
200
 

CHAPTER FOUR
 
Hardware Description Languages
 



[3:0]	[6:0]



Figure 4.20 sevenseg synthesized circuit


possible input combinations are defined. Otherwise, it implies sequential logic, because the output will keep its old value in the undefined cases.
The HDL for the seven-segment display decoder synthesizes into a read-only memory (ROM) containing the 7 outputs for each of the 16 possible inputs. ROMs are discussed further in Section 5.5.6.
If the default or others clause were left out of the case statement, the decoder would have remembered its previous output any time data were in the range of 10–15. This is strange behavior for hardware.
Ordinary decoders are also commonly written with case state- ments. HDL Example 4.25 describes a 3:8 decoder.

4.5.2	If Statements
always/process statements may also contain if statements. The if
statement may be followed by an else statement. If all possible input


 
HDL Example 4.25 3:8 DECODER
SystemVerilog
module decoder3_8(input logic [2:0] a,
output logic [7:0] y);

always_comb case(a)
3'b000: y = 8'b00000001;
3'b001: y = 8'b00000010;
3'b010: y = 8'b00000100;
3'b011: y = 8'b00001000;
3'b100: y = 8'b00010000;
3'b101: y = 8'b00100000;
3'b110: y = 8'b01000000;
3'b111: y = 8'b10000000;
default: y = 8'bxxxxxxxx; endcase
endmodule

The default statement isn’t strictly necessary for logic synthesis in this case because all possible input combinations are defined, but it is prudent for simulation in case one of the inputs is an x or z.
 


VHDL
library IEEE; use IEEE.STD_LOGIC_1164.all; entity decoder3_8 is
port(a: in STD_LOGIC_VECTOR(2 downto 0); y: out STD_LOGIC_VECTOR(7 downto 0));
end;

architecture synth of decoder3_8 is begin
process(all) begin case a is
when "000" => y <= "00000001";
when "001" => y <= "00000010";
when "010" => y <= "00000100";
when "011" => y <= "00001000";
when "100" => y <= "00010000";
when "101" => y <= "00100000";
when "110" => y <= "01000000";
when "111" => y <= "10000000";
when others => y <= "XXXXXXXX"; end case;
end process; end;
The others clause isn’t strictly necessary for logic synthesis in this case because all possible input combinations are defined, but it is prudent for simulation in case one of the inputs is an x, z, or u.
 
4.5 More Combinational Logic	201








[0]
	[1]
	[2]
	



[1]
	[2]
	[0]
	



[0]
	[2]
	[1]
	



[2]
	[0]
	[1]
	



[0]
	[1]
	[2]
	



[1]
	[0]
	[2]
	



[0]
	[1]
	[2]
	



[0]
	[1]
	[2]
y34
Figure 4.21 decoder3_8 synthesized circuit

 
202
 

CHAPTER FOUR
 
Hardware Description Languages
 



 
HDL Example 4.26 PRIORITY CIRCUIT

SystemVerilog	VHDL
module priorityckt(input logic [3:0] a,
output logic [3:0] y);
always_comb
if  (a[3]) y = 4'b1000;
else if (a[2]) y = 4'b0100; else if (a[1]) y = 4'b0010; else if (a[0]) y = 4'b0001; else    y = 4'b0000;
endmodule

In SystemVerilog, if statements must appear inside of
always statements.	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity priorityckt is
port(a: in STD_LOGIC_VECTOR(3 downto 0); y: out STD_LOGIC_VECTOR(3 downto 0));
end;

architecture synth of priorityckt is begin
process(all) begin
if a(3) then y <= "1000"; elsif a(2) then y <= "0100"; elsif a(1) then y <= "0010"; elsif a(0) then y <= "0001"; else	y <= "0000"; end if;
end process; end;
	Unlike SystemVerilog, VHDL supports conditional signal assignment statements (see HDL Example 4.6), which are much like if statements but can appear outside processes. Thus, there is less reason to use processes to describe combinational logic.


 
[3]
[2:0]
 

y[3:0]
 


 
[2]
[3]
 


y_1[2]
 

[2]
 

 
[3:0]
 



[2]
[3]
 



un13_y
 

[1]	[1]

y_1[1]
 


 
[1]
[2]
[3]
 



un21_y
 
[0]
 


y_1[0]
 

[0]
 
Figure 4.22 priorityckt synthesized circuit

 
4.5 More Combinational Logic	203


combinations are handled, the statement implies combinational logic. Otherwise, it produces sequential logic (like the latch in Section 4.4.5).
HDL Example 4.26 uses if statements to describe a priority circuit, defined in Section 2.4. Recall that an N-input priority circuit sets the output TRUE that corresponds to the most significant input that is TRUE.

4.5.3	Truth Tables with Don’t Cares
As examined in Section 2.7.3, truth tables may include don’t cares to allow more logic simplification. HDL Example 4.27 shows how to describe a priority circuit with don’t cares.
The synthesis tool generates a slightly different circuit for this module, shown in Figure 4.23, than it did for the priority circuit in Figure 4.22. However, the circuits are logically equivalent.

4.5.4	Blocking and Nonblocking Assignments

The guidelines on page 204 explain when and how to use each type of assignment. If these guidelines are not followed, it is possible to write code that appears to work in simulation but synthesizes to incorrect hardware. The optional remainder of this section explains the principles behind the guidelines.



HDL Example 4.27 PRIORITY CIRCUIT USING DON’T CARES

SystemVerilog	VHDL
module priority_casez(input logic [3:0] a,	library IEEE; use IEEE.STD_LOGIC_1164.all;
output logic [3:0] y);
always_comb casez(a)
4'b1???: y = 4'b1000;
4'b01??: y = 4'b0100;	
entity priority_casez is
port(a: in STD_LOGIC_VECTOR(3 downto 0); y: out STD_LOGIC_VECTOR(3 downto 0));
end;
4'b001?: y = 4'b0010;
4'b0001: y = 4'b0001;
default: y = 4'b0000; endcase
endmodule	architecture dontcare of priority_casez is begin
process(all) begin case? a is
when "1---" => y <= "1000";
The casez statement acts like a case statement except that it also recognizes ? as don’t care.	when "01--" => y <= "0100";
when "001-" => y <= "0010";
when "0001" => y <= "0001";
	when others => y <= "0000";
	end case?;
	end process;
	end;
	The case? statement acts like a case statement except
	that it also recognizes – as don’t care.
 
204
 

CHAPTER FOUR
 
Hardware Description Languages
 


 
y25
Figure 4.23 priority_casez synthesized circuit



BLOCKING AND NONBLOCKING ASSIGNMENT GUIDELINES

 
SystemVerilog
1.	Use always_ff @(posedge clk) and nonblocking assign- ments to model synchronous sequential logic.
always_ff @(posedge clk) begin
n1 <= d; // nonblocking q <= n1; // nonblocking
end

2.	Use continuous assignments to model simple combinational logic.
assign y = s ? d1 : d0;
3.	Use always_comb and blocking assignments to model more complicated combinational logic where the always statement is helpful.
always_comb
if  (a[3]) y = 4’b1000;
else if (a[2]) y = 4’b0100; else if (a[1]) y = 4’b0010; else if (a[0]) y = 4’b0001; else    y = 4’b0000;

4.	Do not make assignments to the same signal in more than one always statement or continuous assignment statement.
 
VHDL
1.	Use process(clk) and nonblocking assignments to model synchronous sequential logic.
process(clk) begin
if rising_edge(clk) then n1 <= d; –– nonblocking q <= n1; –– nonblocking
end if; end process;
2.	Use concurrent assignments outside process statements to model simple combinational logic.
y <= d0 when s = '0' else d1;
3.	Use process(all) to model more complicated combina- tional logic where the process is helpful. Use blocking assignments for internal variables.
process(all)
variable p, g: STD_LOGIC; begin
p := a xor b; –– blocking g := a and b; –– blocking s <= p xor cin;
cout <= g or (p and cin); end process;
4.	Do not make assignments to the same variable in more than one process or concurrent assignment statement.
 
4.5	More Combinational Logic	205


Combinational Logic*
The full adder from HDL Example 4.23 is correctly modeled using blocking assignments. This section explores how it operates and how it would differ if nonblocking assignments had been used.
Imagine that a, b, and cin are all initially 0. p, g, s, and cout are thus 0 as well. At some time, a changes to 1, triggering the always/process statement. The four blocking assignments evaluate in the order shown here. (In the VHDL code, s and cout are assigned concurrently.) Note that p and g get their new values before s and cout are computed because of the blocking assignments. This is important because we want to compute s and cout using the new values of p and g.
1. p  1  0 = 1
2. g  1 ! 0 = 0
3. s  1  0 = 1
4. cout  0 + 1 ! 0 = 0
In contrast, HDL Example 4.28 illustrates the use of nonblocking assignments.
Now, consider the same case of a rising from 0 to 1 while b and cin
are 0. The four nonblocking assignments evaluate concurrently:
p  1  0 = 1  g  1 ! 0 = 0	s  0  0 = 0	cout  0 + 0 ! 0 = 0

HDL Example 4.28 FULL ADDER USING NONBLOCKING ASSIGNMENTS

SystemVerilog	VHDL
// nonblocking assignments (not recommended) module fulladder(input logic a, b, cin,
output logic s, cout);
logic p, g;

always_comb begin
p <= a ^ b; // nonblocking g <= a & b; // nonblocking
s <= p ^ cin;
cout <= g | (p & cin); end
endmodule	–– nonblocking assignments (not recommended) library IEEE; use IEEE.STD_LOGIC_1164.all;
entity fulladder is
port(a, b, cin: in STD_LOGIC; s, cout: out STD_LOGIC);
end;

architecture nonblocking of fulladder is signal p, g: STD_LOGIC;
begin
process(all) begin
p <= a xor b; –– nonblocking g <= a and b; –– nonblocking s <= p xor cin;
cout <= g or (p and cin); end process;
end;
	Because p and g appear on the left-hand side of a nonblocking assignment in a process statement, they must be declared to be signal rather than variable. The signal declaration appears before the begin in the architecture, not the process.
 
206
 

CHAPTER FOUR
 
Hardware Description Languages
 


Observe that s is computed concurrently with p. Hence, it uses the old value of p, not the new value. Therefore, s remains 0 rather than becoming 1. However, p does change from 0 to 1. This change triggers the always/process statement to evaluate a second time, as follows:
p  1  0 = 1  g  1 ! 0 = 0  s  1  0 = 1  cout  0 + 1 ! 0 = 0
This time, p is already 1, so s correctly changes to 1. The nonblocking assignments eventually reach the right answer, but the always/process statement had to evaluate twice. This makes simulation slower, though it synthesizes to the same hardware.
Another drawback of nonblocking assignments in modeling combi- national logic is that the HDL will produce the wrong result if you forget to include the intermediate variables in the sensitivity list.
Worse yet, some synthesis tools will synthesize the correct hardware even when a faulty sensitivity list causes incorrect simulation. This leads to a mismatch between the simulation results and what the hardware actually does.



Sequential Logic*
The synchronizer from HDL Example 4.20 is correctly modeled using nonblocking assignments. On the rising edge of the clock, d is copied to n1 at the same time that n1 is copied to q, so the code properly describes two registers. For example, suppose initially that d = 0, n1 = 1, and
q = 0. On the rising edge of the clock, the following two assignments
occur concurrently, so that after the clock edge, n1 = 0 and q = 1.
n1  d = 0  q  n1 = 1
HDL Example 4.29 tries to describe the same module using blocking assignments. On the rising edge of clk, d is copied to n1. Then, this new value of n1 is copied to q, resulting in d improperly appearing at both n1 and q. The assignments occur one after the other so that after the clock edge, q = n1 = 0.
1. n1  d = 0
2. q  n1 = 0
 
4.6 Finite State Machines	207


HDL Example 4.29 BAD SYNCHRONIZER WITH BLOCKING ASSIGNMENTS

SystemVerilog	VHDL
// Bad implementation of a synchronizer using blocking
// assignments	–– Bad implementation of a synchronizer using blocking
–– assignment
module syncbad(input logic clk,
input logic d, output logic q);
logic n1;

always_ff @(posedge clk) begin
n1 = d; // blocking q = n1; // blocking
end endmodule	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity syncbad is port(clk:in STD_LOGIC;
d: in STD_LOGIC;
q: out STD_LOGIC);
end;

architecture bad of syncbad is begin
process(clk)
variable n1: STD_LOGIC; begin
if rising_edge(clk) then n1 := d; –– blocking
q <= n1; end if;
end process; end;

q
Figure 4.24 syncbad synthesized circuit


Because n1 is invisible to the outside world and does not influence the behavior of q, the synthesizer optimizes it away entirely, as shown in Figure 4.24.
The moral of this illustration is to exclusively use nonblocking assignment in always/process statements when modeling sequen- tial logic. With sufficient cleverness, such as reversing the orders of the assignments, you could make blocking assignments work correctly, but blocking assignments offer no advantages and only introduce the risk of unintended behavior. Certain sequential circuits will not work with blocking assignments no matter what the order.

4.6	FINITE STATE MACHINES
Recall that a finite state machine (FSM) consists of a state register and two blocks of combinational logic to compute the next state and the output given the current state and the input, as was shown in Figure 3.22. HDL descriptions of state machines are correspondingly divided into three parts to model the state register, the next state logic, and the output logic.
 
208
 

CHAPTER FOUR
 
Hardware Description Languages
 



 
HDL Example 4.30 DIVIDE-BY-3 FINITE STATE MACHINE

SystemVerilog	VHDL
module divideby3FSM(input logic clk,
input logic reset, output logic y);
typedef enum logic [1:0] {S0, S1, S2} statetype; statetype state, nextstate;	library IEEE; use IEEE.STD_LOGIC_1164.all;

entity divideby3FSM is
port(clk, reset: in STD_LOGIC; y:	out STD_LOGIC);
end;
// state register
always_ff @(posedge clk, posedge reset) if (reset) state <= S0;
else	state <= nextstate;	
architecture synth of divideby3FSM is type statetype is (S0, S1, S2); signal state, nextstate: statetype;
begin
// next state logic always_comb
case (state)
S0:	nextstate = S1;
S1:	nextstate = S2;
S2:	nextstate = S0; default: nextstate = S0;
endcase	
–– state register process(clk, reset) begin
if reset then state <= S0; elsif rising_edge(clk) then
state <= nextstate; end if;
end process;
// output logic
assign y = (state == S0); endmodule	–– next state logic
nextstate <= S1 when state = S0 else
S2 when state = S1 else S0;
The typedef statement defines statetype to be a two-bit logic value with three possibilities: S0, S1, or S2. state and nextstate are statetype signals.
The enumerated encodings default to numerical order: S0 = 00, S1 = 01, and S2 = 10. The encodings can be explicitly set by the user; however, the synthesis tool views them as sug- gestions, not requirements. For example, the following snippet
encodes the states as 3-bit one-hot values:
typedef enum logic [2:0] {S0 = 3'b001, S1 = 3'b010, S2 = 3'b100} statetype;
Notice how a case statement is used to define the state transition table. Because the next state logic should be com- binational, a default is necessary, even though the state 2'b11 should never arise.
The output, y, is 1 when the state is S0. The equality comparison a == b evaluates to 1 if a equals b and 0 otherwise. The inequality comparison a != b does the inverse, evaluating to 1 if a does not equal b.	
–– output logic
y <= '1' when state = S0 else '0'; end;
This example defines a new enumeration data type, statetype, with three possibilities: S0, S1, and S2. state and nextstate are statetype signals. By using an enumeration instead of choosing the state encoding, VHDL frees the synthesizer to explore various state encodings to choose the best one.
In the HDL above, the output, y, is 1 when the state is S0. The inequality comparison uses /=. To produce an output of 1 when the state is anything but S0, change the comparison to state /= S0.


HDL Example 4.30 describes the divide-by-3 FSM from Section
3.4.2. It provides an asynchronous reset to initialize the FSM. The state register uses the ordinary idiom for flip-flops. The next state and output logic blocks are combinational.
Synthesis tools produce just a block diagram and state transition dia- gram for state machines; they do not show the logic gates or the inputs
 
4.6	Finite State Machines	209



	clk
res	et



Figure 4.25 divideby3fsm
synthesized circuit









and outputs on the arcs and states. Therefore, be careful that you have specified the FSM correctly in your HDL code. The state transition dia- gram in Figure 4.25 for the divide-by-3 FSM is analogous to the diagram in Figure 3.28(b). The double circle indicates that S0 is the reset state. Gate-level implementations of the divide-by-3 FSM were shown in Section 3.4.2.
Notice that the states are named with an enumeration data type rather than by referring to them as binary values. This makes the code more readable and easier to change.
If, for some reason, we had wanted the output to be HIGH in states S0 and S1, the output logic would be modified as follows.






The next two examples describe the snail pattern recognizer FSM from Section 3.4.3. The code shows how to use case and if statements to handle next state and output logic that depend on the inputs as well as the current state. We show both Moore and Mealy modules. In the Moore machine (HDL Example 4.31), the output depends only on the current state, whereas in the Mealy machine (HDL Example 4.32), the output logic depends on both the current state and inputs.
 
210
 

CHAPTER FOUR
 
Hardware Description Languages
 



 
HDL Example 4.31 PATTERN RECOGNIZER MOORE FSM

 
SystemVerilog
module patternMoore(input logic clk,
input logic reset, input logic a, output logic y);
typedef enum logic [1:0] {S0, S1, S2} statetype; statetype state, nextstate;
// state register
always_ff @(posedge clk, posedge reset) if (reset) state <= S0;
else	state <= nextstate;

// next state logic always_comb
case (state)
S0: if (a) nextstate = S0; else nextstate = S1; S1: if (a) nextstate = S2; else nextstate = S1; S2: if (a) nextstate = S0; else nextstate = S1; default: nextstate = S0;
endcase

// output logic
assign y = (state = = S2); endmodule
Note how nonblocking assignments (<=) are used in the state register to describe sequential logic, whereas blocking assign- ments (=) are used in the next state logic to describe combi- national logic.
 
VHDL
library IEEE; use IEEE.STD_LOGIC_1164.all; entity patternMoore is
port(clk, reset: in STD_LOGIC; a:	in STD_LOGIC;
y:	out STD_LOGIC);
end;

architecture synth of patternMoore is type statetype is (S0, S1, S2); signal state, nextstate: statetype;
begin
–– state register process(clk, reset) begin
if reset then	state <= S0;
elsif rising_edge(clk) then state <= nextstate; end if;
end process;

–– next state logic process(all) begin
case state is when S0 =>
if a then nextstate <= S0; else nextstate <= S1; end if;
when S1 =>
if a then nextstate <= S2; else nextstate <= S1; end if;
when S2 =>
if a then nextstate <= S0; else nextstate <= S1; end if;
when others =>
nextstate <= S0;
 
end case; end process;
––output logic
y <= '1' when state = S2 else '0'; end;





[2]
y
[2:0]





Figure 4.26 patternMoore synthesized circuit

 
4.7	Data Types	211
HDL Example 4.32 PATTERN RECOGNIZER MEALY FSM
 


















































reset
 







































State
Figure 4.27 patternMealy synthesized circuit
 

 

4.7	DATA TYPES*
This section explains some subtleties about SystemVerilog and VHDL types in more depth.
 
212
 

CHAPTER FOUR
 
Hardware Description Languages
 


4.7.1	SystemVerilog
Prior to SystemVerilog, Verilog primarily used two types: reg and wire. Despite its name, a reg signal might or might not be associated with a register. This was a great source of confusion for those learning the language. SystemVerilog introduced the logic type to eliminate the confusion; hence, this book emphasizes the logic type. This section explains the reg and wire types in more detail for those who need to read old Verilog code.
In Verilog, if a signal appears on the left-hand side of <= or = in an always block, it must be declared as reg. Otherwise, it should be declared as wire. Hence, a reg signal might be the output of a flip-flop, a latch, or combinational logic, depending on the sensitivity list and statement of an always block.
Input and output ports default to the wire type unless their type is explicitly defined as reg. The following example shows how a flip-flop is described in conventional Verilog. Note that clk and d default to wire, while q is explicitly defined as reg because it appears on the left- hand side of <= in the always block.
module flop(input	clk,
input	[3:0] d, output reg [3:0] q);
always @(posedge clk) q <= d;
endmodule

SystemVerilog introduces the logic type. logic is a synonym for reg and avoids misleading users about whether it is actually a flip- flop. Moreover, SystemVerilog relaxes the rules on assign statements and hierarchical port instantiations so that logic can be used outside always blocks where a wire traditionally would have been required. Thus, nearly all SystemVerilog signals can be logic. The excep- tion is that signals with multiple drivers (e.g., a tristate bus) must be declared as a net, as described in HDL Example 4.10. This rule allows SystemVerilog to generate an error message rather than an x value when a logic signal is accidentally connected to multiple drivers.
The most common type of net is called a wire or tri. These two types are synonymous, but wire is conventionally used when a single driver is pres- ent and tri is used when multiple drivers are present. Thus, wire is obsolete in SystemVerilog because logic is preferred for signals with a single driver.
When a tri net is driven to a single value by one or more drivers, it takes on that value. When it is undriven, it floats (z). When it is driven to a different value (0, 1, or x) by multiple drivers, it is in contention (x). There are other net types that resolve differently when undriven or driven by multiple sources. These other types are rarely used but may be substituted anywhere a tri net would normally appear (e.g., for signals
with multiple drivers). Each is described in Table 4.7.
 
4.7	Data Types	213
Table 4.7 Net Resolution
tri	z	x
triand	z	0 if there are any 0
tri0	0	x

4.7.2	VHDL
Unlike SystemVerilog, VHDL enforces a strict data typing system that can protect the user from some errors but that is also clumsy at times.
Despite its fundamental importance, the STD_LOGIC type is not built into VHDL. Instead, it is part of the IEEE.STD_LOGIC_1164 library. Thus, every file must contain the library statements shown in the previ- ous examples.
Moreover, IEEE.STD_LOGIC_1164 lacks basic operations such as addition, comparison, shifts, and conversion to integers for the STD_ LOGIC_VECTOR data. These were finally added to the VHDL 2008 stan- dard in the IEEE.NUMERIC_STD_UNSIGNED library.
VHDL also has a BOOLEAN type with two values: true and false. BOOLEAN values are returned by comparisons (such as the equality com- parison, s ='0') and are used in conditional statements, such as when and if. Despite the temptation to believe a BOOLEAN true value should be equivalent to a STD_LOGIC '1' and BOOLEAN false should mean STD_LOGIC '0', these types were not interchangeable prior to VHDL 2008. For example, in old VHDL code, one must write
y <= d1 when (s = '1') else d0;
while in VHDL 2008, the when statement automatically converts s from
STD_LOGIC to BOOLEAN so one can simply write

y <= d1 when s else d0;

Even in VHDL 2008, it is still necessary to write q <= '1' when (state = S2) else '0'; instead of
q <= (state = S2);
 
214
 

CHAPTER FOUR
 
Hardware Description Languages
 


because (state = S2) returns a BOOLEAN result, which cannot be directly assigned to the STD_LOGIC signal y.
Although we do not declare any signals to be BOOLEAN, they are automatically implied by comparisons and used by conditional state- ments. Similarly, VHDL has an INTEGER type that represents both positive and negative integers. Signals of type INTEGER span at least the values
–(231 – 1) to 231 – 1. Integer values are used as indices of busses. For example, in the statement
y <= a(3) and a(2) and a(1) and a(0);
0, 1, 2, and 3 are integers serving as an index to choose bits of the a signal. We cannot directly index a bus with a STD_LOGIC or STD_LOGIC_VECTOR signal. Instead, we must convert the signal to an INTEGER. This is demon- strated in the example below for an 8:1 multiplexer that selects one bit from a vector using a 3-bit index. The TO_INTEGER function is defined in the IEEE.NUMERIC_STD_UNSIGNED library and performs the conversion from STD_LOGIC_VECTOR to INTEGER for positive (unsigned) values.
library IEEE;
use IEEE.STD_LOGIC_1164.all;
use IEEE.NUMERIC_STD_UNSIGNED.all;
entity mux8 is
port(d: in STD_LOGIC_VECTOR(7 downto 0); s: in STD_LOGIC_VECTOR(2 downto 0); y: out STD_LOGIC);
end;
architecture synth of mux8 is begin
y <= d(TO_INTEGER(s));
end;
VHDL is also strict about out ports being exclusively for output. For example, the following code for two- and three-input AND gates is illegal VHDL because v is an output and is also used to compute w.
library IEEE; use IEEE.STD_LOGIC_1164.all; entity and23 is
port(a, b, c: in STD_LOGIC; v, w: out	STD_LOGIC);
end;
architecture synth of and23 is begin
v <= a and b; w <= v and c;
end;
VHDL defines a special port type, buffer, to solve this problem. A signal connected to a buffer port behaves as an output but may also be used within the module. The corrected entity definition follows. Verilog
 
4.8	Parameterized Modules	215
 


and SystemVerilog do not have this limitation and do not require buffer ports. VHDL 2008 eliminates this restriction by allowing out ports to be readable.
entity and23 is
port(a, b, c: in STD_LOGIC; v: buffer	STD_LOGIC; w: out	STD_LOGIC);
 


Figure 4.28 and23 synthesized circuit
 
end;
Most operations such as addition, subtraction, and Boolean logic are identical whether a number is signed or unsigned. However, magnitude comparison, multiplication, and arithmetic right shifts are performed differ- ently for signed two’s complement numbers than for unsigned binary num- bers. These operations will be examined in Chapter 5. HDL Example 4.33 describes how to indicate that a signal represents a signed number.


HDL Example 4.33 (a) UNSIGNED MULTIPLIER (b) SIGNED MULTIPLIER

SystemVerilog	VHDL
// 4.33(a): unsigned multiplier
module multiplier(input logic [3:0] a, b,
output logic [7:0] y);
assign y = a * b; endmodule
// 4.33(b): signed multiplier
module multiplier(input logic signed [3:0] a, b,
output logic signed [7:0] y);

assign y = a * b; endmodule
In SystemVerilog, signals are considered unsigned by default. Adding the signed modifier (e.g., logic signed [3:0] a) causes the signal a to be treated as a signed—that is, two’s complement—number.	–– 4.33(a): unsigned multiplier
library IEEE; use IEEE.STD_LOGIC_1164.all; use IEEE.NUMERIC_STD_UNSIGNED.all;
entity multiplier is
port(a, b: in STD_LOGIC_VECTOR(3 downto 0); y:	out STD_LOGIC_VECTOR(7 downto 0));
end;

architecture synth of multiplier is begin
y <= a * b; end;
VHDL uses the NUMERIC_STD_UNSIGNED library to perform arithmetic and comparison operations on STD_LOGIC_VECTORs. The vectors are treated as unsigned.
	use IEEE.NUMERIC_STD_UNSIGNED.all;
	VHDL also defines UNSIGNED and SIGNED data types in the IEEE.NUMERIC_STD library, but these involve type conver- sions beyond the scope of this chapter.


4.8 PARAMETERIZED MODULES*
So far, all of our modules have had fixed-width inputs and outputs. For example, we had to define separate modules for 4- and 8-bit-wide 2:1 mul- tiplexers. HDLs permit variable bit widths using parameterized modules.
HDL Example 4.34 declares a parameterized 2:1 multiplexer with a default width of 8, then uses it to create 8- and 12-bit 4:1 multiplexers.
 
216
 

CHAPTER FOUR
 
Hardware Description Languages
 



 
HDL Example 4.34 PARAMETERIZED N-BIT 2:1 MULTIPLEXERS

 
SystemVerilog
module mux2 #(parameter width = 8)
(input logic [width–1:0] d0, d1, input logic	s, output logic [width–1:0] y);
assign y = s ? d1 : d0; endmodule
SystemVerilog allows a #(parameter ...) statement before the inputs and outputs to define parameters. The parameter statement includes a default value (8) of the parameter, in this case called width. The number of bits in the inputs and outputs can depend on this parameter.
module mux4_8(input logic [7:0] d0, d1, d2, d3, input logic [1:0] s,
output logic [7:0] y); logic [7:0] low, hi;
mux2 lowmux(d0, d1, s[0], low); mux2 himux(d2, d3, s[0], hi);
mux2 outmux(low, hi, s[1], y); endmodule
The 8-bit 4:1 multiplexer instantiates three 2:1 multiplexers using their default widths.
In contrast, a 12-bit 4:1 multiplexer, mux4_12, would need to override the default width using #( ) before the instance name, as shown below.
module mux4_12(input logic [11:0] d0, d1, d2, d3,
input logic [1:0] s, output logic [11:0] y);
logic [11:0] low, hi;

mux2 #(12) lowmux(d0, d1, s[0], low);
mux2 #(12) himux(d2, d3, s[0], hi);
mux2 #(12) outmux(low, hi, s[1], y); endmodule
Do not confuse the use of the # sign indicating delays with the use of #(...) in defining and overriding parameters.
 
VHDL
library IEEE; use IEEE.STD_LOGIC_1164.all; entity mux2 is
generic(width: integer := 8); port(d0,
d1: in STD_LOGIC_VECTOR(width–1 downto 0); s: in STD_LOGIC;
y: out STD_LOGIC_VECTOR(width–1 downto 0)); end;
architecture synth of mux2 is begin
y <= d1 when s else d0; end;
The generic statement includes a default value (8) of width. The value is an integer.
library IEEE; use IEEE.STD_LOGIC_1164.all; entity mux4_8 is
port(d0, d1, d2,
d3: in STD_LOGIC_VECTOR(7 downto 0); s: in STD_LOGIC_VECTOR(1 downto 0); y: out STD_LOGIC_VECTOR(7 downto 0));
end;

architecture struct of mux4_8 is component mux2
generic(width: integer := 8); port(d0,
d1: in STD_LOGIC_VECTOR(width-1 downto 0); s: in STD_LOGIC;
y: out STD_LOGIC_VECTOR(width-1 downto 0)); end component;
signal low, hi: STD_LOGIC_VECTOR(7 downto 0); begin
lowmux: mux2 port map(d0, d1, s(0), low); himux: mux2 port map(d2, d3, s(0), hi); outmux: mux2 port map(low, hi, s(1), y);
end;

The 8-bit 4:1 multiplexer, mux4_8, instantiates three 2:1 mul- tiplexers, using their default widths.
In contrast, a 12-bit 4:1 multiplexer, mux4_12, would need to override the default width using generic map, as shown below.
lowmux: mux2 generic map(12)
port map(d0, d1, s(0), low); himux: mux2 generic map(12)
port map(d2, d3, s(0), hi); outmux: mux2 generic map(12)
port map(low, hi, s(1), y);
 
4.8 Parameterized Modules	217


Figure 4.29 mux4_12 synthesized circuit


HDL Example 4.35 PARAMETERIZED N:2N DECODER

SystemVerilog	VHDL
module decoder #(parameter N = 3)
(input logic [N–1:0]	a, output logic [2**N–1:0] y);
always_comb begin
y = 0;
y[a] = 1;
end endmodule
2**N indicates 2N.	library IEEE; use IEEE.STD_LOGIC_1164.all; use IEEE. NUMERIC_STD_UNSIGNED.all;
entity decoder is generic(N: integer := 3);
port(a: in STD_LOGIC_VECTOR(N–1 downto 0);
y: out STD_LOGIC_VECTOR(2**N–1 downto 0));
end;

architecture synth of decoder is begin
process(all) begin
y <= (OTHERS => '0'); y(TO_INTEGER(a)) <= '1';
end process; end;
	2**N indicates 2N.

HDL Example 4.35 shows a decoder, which is an even better appli- cation of parameterized modules. A large N:2N decoder is cumbersome to specify with case statements, but easy using parameterized code that simply sets the appropriate output bit to 1. Specifically, the decoder uses blocking assignments to set all the bits to 0, then changes the appropri- ate bit to 1.
HDLs also provide generate statements to produce a variable amount of hardware, depending on the value of a parameter. generate supports for loops and if statements to determine how many of what types of hardware to produce. HDL Example 4.36 demonstrates how to use generate statements to produce an N-input AND function from a
 
218
 

CHAPTER FOUR
 
Hardware Description Languages
 


cascade of two-input AND gates. Of course, a reduction operator would be cleaner and simpler for this application, but the example illustrates the general principle of hardware generators.
Use generate statements with caution; it is easy to produce a large amount of hardware unintentionally!

HDL Example 4.36 PARAMETERIZED N-INPUT AND GATE




Figure 4.30 andN synthesized circuit



4.9 TESTBENCHES
A testbench is an HDL module that is used to test another module, called the device under test (DUT). The testbench contains statements to apply inputs to the DUT and, ideally, to check that the correct outputs are pro- duced. The input and desired output patterns are called test vectors.
Consider testing the sillyfunction module from Section 4.1.1 that computes y = a bc + ab c + abc. This is a simple module, so we can perform exhaustive testing by applying all eight possible test vectors.
 
4.9 Testbenches	219


HDL Example 4.37 TESTBENCH

SystemVerilog	VHDL
module testbench1();	library IEEE; use IEEE.STD_LOGIC_1164.all;
logic a, b, c, y;	
entity testbench1 is –– no inputs or outputs
// instantiate device under test	end;
sillyfunction dut(a, b, c, y);	
architecture sim of testbench1 is
// apply inputs one at a time	component sillyfunction
initial begin	port(a, b, c: in STD_LOGIC;
a = 0; b = 0; c = 0; #10;	y:	out STD_LOGIC);
c = 1;	#10;	end component;
b = 1; c = 0;	#10;	signal a, b, c, y: STD_LOGIC;
c = 1;	#10;	begin
a = 1; b = 0; c = 0; #10;	–– instantiate device under test
c = 1;	#10;	dut: sillyfunction port map(a, b, c, y);
b = 1; c = 0;	#10;
c = 1;	#10;
end endmodule	
–– apply inputs one at a time process begin
a <= '0'; b <= '0'; c <= '0'; wait for 10 ns;
c <= '1';	wait for 10 ns;
The initial statement executes the statements in its body at the start of simulation. In this case, it first applies the input pattern 000 and waits for 10 time units. It then applies 001
and waits 10 more units, and so forth until all eight possible	b <= '1'; c <= '0';    wait for 10 ns;
c <= '1';	wait for 10 ns; a <= '1'; b <= '0'; c <= '0'; wait for 10 ns; c <= '1';	 wait for 10 ns;
b <= '1'; c <= '0';    wait for 10 ns;
inputs have been applied. initial statements should be used only in testbenches for simulation, not in modules intended to be synthesized into actual hardware. Hardware has no
way of magically executing a sequence of special steps when	c <= '1';	wait for 10 ns; wait; –– wait forever
end process;
end;
it is first turned on.	The process statement first applies the input pattern 000 and
	waits for 10 ns. It then applies 001 and waits 10 more ns, and
	so forth until all eight possible inputs have been applied.
	At the end, the process waits indefinitely. Otherwise, the pro-
	cess would begin again, repeatedly applying the pattern of
	test vectors.

HDL Example 4.37 demonstrates a simple testbench. It instantiates the DUT, then applies the inputs. Blocking assignments and delays are used to apply the inputs in the appropriate order. The user must view the results of the simulation and verify by inspection that the correct outputs are produced. Testbenches are simulated the same as other HDL modules. However, they are not synthesizeable.
Checking for correct outputs is tedious and error-prone. Moreover, determining the correct outputs is much easier when the design is fresh in your mind. If you make minor changes and need to retest weeks later, determining the correct outputs becomes a hassle. A much bet- ter approach is to write a self-checking testbench, shown in HDL Example 4.38.
Writing code for each test vector also becomes tedious, especially for modules that require a large number of vectors. An even better
 
220
 

CHAPTER FOUR
 
Hardware Description Languages
 



 

 
HDL Example 4.38 SELF-CHECKING TESTBENCH
SystemVerilog
module testbench2(); logic a, b, c, y;
// instantiate device under test sillyfunction dut(a, b, c, y);
// apply inputs one at a time
// checking results initial begin
a = 0; b = 0; c = 0; #10;
assert (y = = = 1) else $error("000 failed."); c = 1; #10;
assert (y = = = 0) else $error("001 failed."); b = 1; c = 0; #10;
assert (y = = = 0) else $error("010 failed."); c = 1; #10;
assert (y = = = 0) else $error("011 failed."); a = 1; b = 0; c = 0; #10;
assert (y = = = 1) else $error("100 failed."); c = 1; #10;
assert (y = = = 1) else $error("101 failed."); b = 1; c = 0; #10;
assert (y = = = 0) else $error("110 failed."); c = 1; #10;
assert (y = = = 0) else $error("111 failed."); end
endmodule

The SystemVerilog assert statement checks whether a spec- ified condition is true. If not, it executes the else statement. The $error system task in the else statement prints an error message describing the assertion failure. assert is ignored during synthesis.
In SystemVerilog, comparison using = = or != is effective between signals that do not take on the values of x and z. Testbenches use the = = = and != = operators for comparisons of equality and inequality, respectively, because these opera- tors work correctly with operands that could be x or z.
 


VHDL
library IEEE; use IEEE.STD_LOGIC_1164.all;

entity testbench2 is –– no inputs or outputs end;
architecture sim of testbench2 is component sillyfunction
port(a, b, c: in STD_LOGIC; y:	out STD_LOGIC);
end component;
signal a, b, c, y: STD_LOGIC; begin
–– instantiate device under test
dut: sillyfunction port map(a, b, c, y);

–– apply inputs one at a time
–– checking results process begin
a <= '0'; b <= '0'; c <= '0'; wait for 10 ns; assert y = '1' report "000 failed.";
c <= '1';	wait for 10 ns; assert y = '0' report "001 failed.";
b <= '1'; c <= '0';	wait for 10 ns; assert y = '0' report "010 failed.";
c <= '1';	wait for 10 ns; assert y = '0' report "011 failed.";
a <= '1'; b <= '0'; c <= '0'; wait for 10 ns; assert y = '1' report "100 failed.";
c <= '1';	wait for 10 ns; assert y = '1' report "101 failed.";
b <= '1'; c <= '0';	wait for 10 ns; assert y = '0' report "110 failed.";
c <= '1';	wait for 10 ns; assert y = '0' report "111 failed.";
wait; –– wait forever end process;
end;
The assert statement checks a condition and prints the mes- sage given in the report clause if the condition is not satisfied. assert is meaningful only in simulation, not in synthesis.
 



approach is to place the test vectors in a separate file. The testbench simply reads the test vectors from the file, applies the input test vector to the DUT, waits, checks that the output values from the DUT match the out- put vector, and repeats until reaching the end of the test vectors file.
HDL Example 4.39 demonstrates such a testbench. The testbench generates a clock using an always/process statement with no sensitivity list, so that it is continuously reevaluated. At the beginning of the sim- ulation, it reads the test vectors from a text file and pulses reset for two cycles. Although the clock and reset aren’t necessary to test combi- national logic, they are included because they would be important when
 
4.9 Testbenches	221


testing a sequential DUT. example.txt is a text file containing the test vectors, the inputs and expected output written in binary:
000_1
001_0
010_0
011_0
100_1
101_1
110_0
111_0

HDL Example 4.39 TESTBENCH WITH TEST VECTOR FILE
 
SystemVerilog
module testbench3();
logic	clk, reset;
logic	a, b, c, y, yexpected; logic [31:0] vectornum, errors; logic [3:0] testvectors[10000:0];
// instantiate device under test sillyfunction dut(a, b, c, y);
// generate clock always
begin
clk = 1; #5; clk = 0; #5; end
// at start of test, load vectors
// and pulse reset initial
begin
$readmemb("example.txt", testvectors); vectornum = 0; errors = 0;
reset = 1; #22; reset = 0; end
// apply test vectors on rising edge of clk always @(posedge clk)
begin
#1; {a, b, c, yexpected} = testvectors[vectornum]; end
// check results on falling edge of clk always @(negedge clk)
if (~reset) begin // skip during reset
if (y ! = = yexpected) begin // check result
$display("Error: inputs = %b", {a, b, c});
$display(" outputs = %b (%b expected)", y, yexpected); errors = errors + 1;
end
vectornum = vectornum + 1;
if (testvectors[vectornum] = = = 4'bx) begin
$display("%d tests completed with %d errors", vectornum, errors);
$stop; end
end endmodule
 
VHDL
library IEEE; use IEEE.STD_LOGIC_1164.all;
use IEEE.STD_LOGIC_TEXTIO.ALL; use STD.TEXTIO.all;
entity testbench3 is –– no inputs or outputs end;
architecture sim of testbench3 is component sillyfunction
port(a, b, c: in STD_LOGIC; y:	out STD_LOGIC);
end component;
signal a, b, c, y: STD_LOGIC; signal y_expected: STD_LOGIC; signal clk, reset: STD_LOGIC;
begin
–– instantiate device under test
dut: sillyfunction port map(a, b, c, y);
–– generate clock process begin
clk <= '1'; wait for 5 ns; clk <= '0'; wait for 5 ns;
end process;

–– at start of test, pulse reset process begin
reset <= '1'; wait for 27 ns; reset <= '0'; wait;
end process;

–– run tests process is
file tv: text; variable L: line;
variable vector_in: std_logic_vector(2 downto 0); variable dummy: character;
variable vector_out: std_logic; variable vectornum: integer := 0; variable errors: integer := 0;
begin
FILE_OPEN(tv, "example.txt", READ_MODE); while not endfile(tv) loop
–– change vectors on rising edge wait until rising_edge(clk);
–– read the next line of testvectors and split into pieces readline(tv, L);
read(L, vector_in);
read(L, dummy); –– skip over underscore
 
222
 

CHAPTER FOUR
 
Hardware Description Languages
 


 
$readmemb reads a file of binary numbers into the testvectors array. $readmemh is similar but reads a file of hexadecimal numbers.
The next block of code waits one time unit after the ris- ing edge of the clock (to avoid any confusion if clock and data change simultaneously), then sets the three inputs and the expected output based on the four bits in the current test vector.
The testbench compares the generated output, y, with the expected output, yexpected, and prints an error if they don’t match. %b and %d indicate to print the values in binary and decimal, respectively. $display is a system task to print in the simulator window. For example, $display ("%b %b", y, yexpected); prints the two values, y and yexpected, in binary. %h prints a value in hexadecimal.
This process repeats until there are no more valid test vectors in the testvectors array. $stop stops the simulation. Note that even though the SystemVerilog module sup- ports up to 10,001 test vectors, it will terminate the simula-
tion after executing the eight vectors in the file.
 
read(L, vector_out);
(a, b, c) <= vector_in(2 downto 0) after 1 ns; y_expected <= vector_out after 1 ns;
-- check results on falling edge wait until falling_edge(clk);
if y /= y_expected then
report "Error: y = " & std_logic'image(y); errors := errors + 1;
end if;

vectornum := vectornum + 1; end loop;
-- summarize results at end of simulation if (errors = 0) then
report "NO ERRORS -- " & integer'image(vectornum) &
" tests completed successfully." severity failure;
else
report integer'image(vectornum) &
" tests completed, errors = " & integer'image(errors) severity failure;
end if; end process;
end;

The VHDL code uses file reading commands beyond the scope of this chapter, but it gives the sense of what a self-checking testbench looks like.
 


New inputs are applied on the rising edge of the clock, and the output is checked on the falling edge of the clock. Errors are reported as they occur. At the end of the simulation, the testbench prints the total number of test vectors applied and the number of errors detected.
The testbench in HDL Example 4.39 is overkill for such a simple circuit. However, it can easily be modified to test more complex circuits by changing the example.txt file, instantiating the new DUT, and changing a few lines of code to set the inputs and check the outputs.

4.10 SUMMARY
Hardware description languages (HDLs) are extremely important tools for modern digital designers. Once you have learned SystemVerilog or VHDL, you will be able to specify digital systems much faster than if you had to draw the complete schematics. The debug cycle is also often much faster because modifications require code changes instead of tedious schematic rewiring. However, the debug cycle can be much longer using HDLs if you don’t have a good idea of the hardware your code implies.
