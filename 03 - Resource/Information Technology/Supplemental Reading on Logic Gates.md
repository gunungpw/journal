# Supplemental Reading on Logic Gates

# Logic Gates

Knowing how logic gates work is important to understanding how a computer works. Computers work by performing binary calculations. **Logic gates** are electrical components that tell a computer how to perform binary calculations. They specify rules for how to produce an electrical output based on one or more electrical inputs. Computers use these electrical signals to represent two binary states: either an “on” state or an “off” state. A logic gate takes in one or more of these binary states and determines whether to pass along an “on” or “off” signal.

Several logic gates have been developed to represent different rules for producing a binary output. This reading covers six of the most common logic gates. 

# Six common logic gates

### **NOT gate** 

The NOT gate is the simplest because it has only one input signal. The NOT gate takes that input signal and outputs a signal with the opposite binary state. If the input signal is “on,” a NOT gate outputs an “off” signal. If the input signal is “off,” a NOT gate outputs an “on” signal. All the logic gates can be defined using a schematic diagram and truth table. Here’s how this logic rule is often represented:

![Not gate schema and truth table](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/tk5lDPnpRN-OZQz56QTflw_58ca55ecf59146549c08a532acc0d9f1_01_NOT-Gate-copy.png?expiry=1716595200000&hmac=KiyLJILfjUtK-PwapKWDnHI0qlp5nYwuw9QMx7X-5UA)

On the left, you have a schematic diagram of a NOT gate. Schematic drawings usually represent a physical NOT gate as a triangle with a small circle on the output side of the gate. To the right of the schematic diagram, you also have a “truth table” that tells you the output value for each of the two possible input values.

### **AND gate** 

The AND gate involves two input signals rather than just one. Having two input signals means there will be four possible combinations of input values. The AND rule outputs an “on” signal only when both the inputs are “on.” Otherwise, the output signal will be “off.”

![AND gate schema and truth table](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/fOo7WK4oSLiqO1iuKAi4fA_5dc969b7e4fa4c6aacd5b2fcb40cc1f1_02_AND-Gate-.png?expiry=1716595200000&hmac=6e7ZJhtD4ryUjj-pCJukI-QPF0oeuTGVlWkPEo3kUSY)

### **OR gate** 

The OR gate involves two input signals. The OR rule outputs an “off” signal only when both the inputs are “off.” Otherwise, the output signal will be “on.”

![OR gate schema and truth table](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/1WbonYykTgum6J2MpG4Lug_3e5c8850f3084c418327c8f191aba5f1_03_OR-Gate.png?expiry=1716595200000&hmac=9tNo35ixzWbAYuRFfP_1QRxqPQZt2sDov408frADj3s)

### **XOR Gate** 

The XOR gate also involves two input signals. The XOR rule outputs an “on” signal when _only one_ (but _not both_) of the inputs are “on.” Otherwise, the output signal will be “off.”

![XOR gate schema and truth table](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/neK52IssTyyiudiLLF8sYA_3023510a6a0d44b99363a0ea80c1abf1_04_XOR-Gate-.png?expiry=1716595200000&hmac=Tv6xdo1ZCJpZerkyRjdJwib0Ur_nFTyxt64ltA1B60I)

The truth tables for XOR and OR gates are very similar. The only difference is that the XOR gate outputs an “off” when both inputs are “on” while the OR outputs an “on.” Sometimes you may hear the XOR gate referred to as an “exclusive OR” gate.

### **NAND gate** 

The NAND gate involves two input signals. The NAND rule outputs an “off” signal only when both the inputs are “on.” Otherwise, the output signal will be “on.”

![NAND gate schema and truth table](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/4q_pIr_sTgmv6SK_7M4JKg_058ec9f2bc5c45feae7a6a32c34d98f1_NAND-Gate.png?expiry=1716595200000&hmac=PnPmhHdtZkjN87cyeNjkP211fNGo6R4BanNKUZvlFM4)

If you compare the truth tables for the NAND and AND gates, you may notice that the NAND outputs are the opposite of the AND outputs. This is because the NAND rule is just a combination of the AND and NOT rules: it takes the AND output and runs it through the NOT rule! For this reason, you might hear the NAND referred to as a “not-AND” gate.

### **XNOR gate** 

Finally, consider the XNOR gate. It also involves two input signals. The XNOR rule outputs an “on” signal only when both the inputs are the same (both “On” or both “Off”). Otherwise, the output signal will be “off.”

![XNOR gate schema and truth table](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/_IRg3Rn_R4GEYN0Z_1eB7Q_ec617554b8384e90b70a85256ecdd7f1_XNOR-Gate.png?expiry=1716595200000&hmac=vY_9gZzhVYmXBIv4BOpuceUNE-fFPcr8GPP32CfxorI)

The XNOR rule is another combination of two earlier rules: it takes the XOR output and runs it through the NOT rule. For this reason, you might hear the XNOR referred to as a “not-XOR” gate.

# Combining gates (building circuits)

Logic gates are physical electronic components—a person can buy them and plug them into a circuit board. Logic gates can be linked together to create complex electrical systems (circuits) that perform complicated binary calculations. You link gates together by letting the output from one gate serve as an input for another gate or by using the same inputs for multiple gates. Computers are this kind of complex electrical system. 

Here’s a schematic drawing for a small circuit built with gates described above:

![Combined circuit schematic](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/mWetS5HYRWanrUuR2PVmPQ_ca5e02fc3b414262bee28fa98535a6f1_Circuit-drawing.png?expiry=1716595200000&hmac=A6s2k9GWPUYoADi4eirD4twFTjMsSq_c4y3XWiGFmYQ)

Here is the truth table for this circuit:

![Combined circuit truth table](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/6Qqgqn8zRw-KoKp_MwcPGA_ade69bff97924d6291e174ba63ab65f1_Circuit-Truth-table.png?expiry=1716595200000&hmac=wZLu5Bp5bxjcBT7Ux_FzJD8vTHx7pgOC2fuZNORJ0xQ)

This circuit uses three logic gates: an XOR gate, a NOT gate, and an AND gate. It takes two inputs (A and B) and produces two outputs (1 and 2). A and B are the inputs for the XOR gate. The output of that gate became the input of the NOT gate. Then, the output of the NOT gate became an input for the AND gate (with input A as the other). Output 1 is the output from the AND gate. Output 2 is the output from the XOR gate. 

# Key takeaways

Logic gates are the physical components that allow computers to make binary calculations.

- Logic gates represent different rules for taking one or more binary inputs and outputting a specific binary value (“on” or “off”).
    
- Logic gates can be linked so that the output of one gate serves as the input for other gates.
    
- Circuits are complex electrical systems built by linking logic gates together. Computers are this kind of complex electrical system.