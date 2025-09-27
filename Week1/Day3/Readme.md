# Day 3: Combinational and Sequential Optimization

Welcome to Day 3 of this workshop! Today we discuss optimization of combinational and sequential circuits, introducing techniques to enhance efficiency and performance.

---

## Table of Contents

- [1. Constant Propagation](#1-constant-propagation)
- [2. State Optimization](#2-state-optimization)
- [3. Cloning](#3-cloning)
- [4. Retiming](#4-retiming)
- [5. Labs on Optimization](#5-labs-on-optimization)

---

## 1. Constant Propagation

In VLSI design, constant propagation is a compiler optimization technique used to replace variables with their constant values during synthesis. This can simplify design and enhance performance.

**How it works:**  
Constant propagation analyzes the design code to identify variables with constant values. These are replaced directly, allowing tools to simplify logic and reduce circuit size.

**Benefits:**
- **Reduced Complexity:** Simpler logic, smaller circuit.
- **Performance Improvement:** Faster execution and reduced delays.
- **Resource Optimization:** Fewer gates or flip-flops required.


---

## 2. State Optimization

State optimization refines finite state machines (FSMs) to improve efficiency in IC design. It reduces the number of states, optimizes encoding, and minimizes logic.

**How it is done:**
- **State Reduction:** Merge equivalent states using algorithms.
- **State Encoding:** Assign optimal codes to states.
- **Logic Minimization:** Use Boolean algebra or tools for compact equations.
- **Power Optimization:** Techniques like clock gating reduce dynamic power.

---

## 3. Cloning

Cloning duplicates a logic cell or module to optimize performance, reduce power, or improve timing by balancing load or reducing wire length.

**How it’s done:**
- Identify critical paths using analysis tools.
- Duplicate the target cell/module.
- Redistribute connections to balance load.
- Place and route the cloned cell.
- Verify improvement via timing and power analysis.


---

## 4. Retiming

Retiming is a design optimization technique that improves circuit performance by repositioning registers (flip-flops) without changing functionality.

**How it is done:**
1. **Graph Representation:** Model circuit as a directed graph.
2. **Register Repositioning:** Move registers to balance path delays.
3. **Constraints Analysis:** Maintain timing and functional equivalence.
4. **Optimization:** Adjust register positions to minimize clock period and optimize power.

---

## 5. Labs on Optimization

### Combinational Constant Propagation

**Opt Check - 1**

```verilog
module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule
```

**Explanation:**
- `assign y = a ? b : 0;` means:
  - If `a` is true, `y` is assigned the value of `b`.
  - If `a` is false, `y` is 0.

Follow the steps from [Day 1 Synthesis Lab](https://github.com/Astrophile1509/RISC-V-Tapeout/tree/main/Week1/Day1) and add the following between `abc -liberty` and `synth -top`:
```shell
opt_clean -purge
```

![Opt Check1 Output](https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/Week1/Day3/Images/opt_check.png)

---

**Opt Check - 2**

Verilog code:

```verilog
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule
```

**Code Analysis:**
- Acts as a multiplexer:
  - `y = 1` if `a` is true.
  - `y = b` if `a` is false.

![Opt Check2 Output](https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/Week1/Day3/Images/opt_check2.png)

---

**Opt Check - 3**

Verilog code:

```verilog
module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule
```

**Functionality:**  
3 bit AND Gate; `y = a ? (c?b:0):0` (outputs `0` when `a` or `b` or `c` is `0`).

![Opt Check3 Output](https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/Week1/Day3/Images/opt_check3.png)

---

**Opt Check - 4**

Verilog code:

```verilog
module opt_check4 (input a , input b , input c , output y);
 assign y = a?(b?(a & c ):c):(!c);
 endmodule
```

**Functionality:**
- Three inputs (`a`, `b`, `c`), output `y`.
- Nested ternary logic:
  - If `a = 1`, `y = c`.
  - If `a = 0`, `y = !c`.
- Logic simplifies to:  
  `y = a ? c : !c`

![Opt Check4 Output](https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/Week1/Day3/Images/opt_check4.png)

---

### Sequential Constant Propagation
**DFF Const - 1**
Verilog code:

```verilog
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end
endmodule
```

**Functionality:**
- D flip-flop with:
  - Asynchronous reset to 0
  - Loads constant `1` when not in reset

![dff const1 Output](https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/Week1/Day3/Images/dff_const1.png)

---

**DFF Const - 2**

Verilog code:

```verilog
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end
endmodule
```

**Functionality:**
- D flip-flop always sets output `q` to `1` (regardless of reset or clock).

![dff const2 Output](https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/Week1/Day3/Images/dff_const2.png)

---
**DFF Const - 3**

Verilog code:

```verilog
module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```

**Functionality:**
- D flip-flop always sets output `q` to `1` (regardless of reset or clock).
- D flip-flop sets output `q1` to `0` when reset is high

![dff const3 Output](https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/Week1/Day3/Images/dff_const3.png)

---
**DFF Const - 4**

Verilog code:

```verilog
module dff_const4(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b1;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```

**Functionality:**
- D flip-flop always sets output `q` and `q1` to `1` (regardless of reset or clock).
- `q` and `q1` are always equal

![dff const4 Output](https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/Week1/Day3/Images/dff_const4.png)

---
**DFF Const - 5**

Verilog code:

```verilog
module dff_const5(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b0;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```


![dff const5 Output](https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/Week1/Day3/Images/dff_const5.png)

---
### Unused Output Optimisation
**Counter Opt**
Verilog code:

```verilog
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = count[0];

always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end

endmodule
```


![Counter Output](https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/Week1/Day3/Images/counter_opt.png)

---

## Summary
- **Focus:** Optimization techniques for combinational and sequential circuits in digital design, with practical Verilog labs.
  
- **Topics Covered:**
  1. **Constant Propagation:** Replacing variables with constant values to simplify logic and improve circuit efficiency.
  2. **State Optimization:** Reducing states and optimizing encoding in finite state machines to use less logic and power.
  3. **Cloning:** Duplicating logic cells/modules to improve timing and balance load.
  4. **Retiming:** Repositioning registers in a circuit to enhance performance without altering its function.

