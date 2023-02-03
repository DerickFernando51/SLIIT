# BJT audio amplifier design

# 1.0 Introduction
A bipolar junction transistor is a semiconductor device that consists of two p-n junctions.
It has three terminals known as the base, the emitter and the collector. One of its primary
functions is amplification. Amplification is the process of magnifying a weak input signal to a
larger level. In a BJT the waveform applied to the emitter terminal is amplified and produced at
the collector terminal.

The objective of this assignment is to design a DC biasing circuit. BC548 npn transistor will be used as the amplifier and a speaker of 8Ω will be used as the load. 

Initially, the values of
the required components will be obtained by analyzing the circuit. Then the accuracy of the
circuit will be confirmed using simulation software. Finally, the circuit will be physically
implemented and tested.

# 2.0 – Circuit design
## 2.1 Data references

 • Source: BC548 datasheet

 • Values obtained: hFE(min) = 110
                        hFE(max) = 800


## 2.2 Analysis steps
### 2.2.1 Biasing scheme
<img width="761" alt="image" src="https://user-images.githubusercontent.com/124335793/216581632-b2960cdb-81c0-4f68-9dc3-8cea5f89f15a.png">

• Voltage divider biasing scheme was selected


### 2.2.2 Resistor value calculation
<img width="911" alt="image" src="https://user-images.githubusercontent.com/124335793/216583837-8c0b12e6-4e1a-452f-b47f-314f12fd01d9.png">
<img width="914" alt="image" src="https://user-images.githubusercontent.com/124335793/216584267-7058bfe6-ff22-4c56-be85-5b96c57b1eec.png">
<img width="913" alt="image" src="https://user-images.githubusercontent.com/124335793/216584652-94e429a1-2a58-43ec-991a-a75ebc56d918.png">
<img width="911" alt="image" src="https://user-images.githubusercontent.com/124335793/216584829-8041ba87-c2fb-4176-8abf-0c9d8b1677dc.png">


### 2.2.3 Coupling capacitor value calculation
<img width="910" alt="image" src="https://user-images.githubusercontent.com/124335793/216585785-f28fcdd1-ea6b-4d74-8626-4080b0da6c74.png">

## Components selected
<img width="908" alt="image" src="https://user-images.githubusercontent.com/124335793/216586336-ba764690-40f6-4c47-af4a-e81a758c2c5c.png">
<img width="911" alt="image" src="https://user-images.githubusercontent.com/124335793/216586780-ef8ab9d7-c591-4bdb-8e8e-6e904fffcb63.png">

# 3.0 – Circuit simulation
## 3.1 Bias point accuracy
<img width="869" alt="image" src="https://user-images.githubusercontent.com/124335793/216587367-15eaeb88-6a73-4c76-bfaf-916c2351d49a.png">
• V<sub>CE</sub> = 6.712;  This value is approximately equal to Vcc / 2

• Therefore, the circuit is midpoint biased

## Frequency response
<img width="870" alt="image" src="https://user-images.githubusercontent.com/124335793/216590095-947ebfcf-d20a-4f00-acb4-23d1bce402fc.png">

## Peak to peak output voltage with the load
<img width="898" alt="image" src="https://user-images.githubusercontent.com/124335793/216590213-da08c2f0-00e7-44c4-a067-8c510bb4dc04.png">
<img width="912" alt="image" src="https://user-images.githubusercontent.com/124335793/216590479-7036ef21-e372-42e0-9cb5-1946a02f717d.png">
• V<sub>P-P</sub> = 185 mV

## Peak to peak output voltage when the load is removed
<img width="911" alt="image" src="https://user-images.githubusercontent.com/124335793/216590933-26c5fe32-2ba5-4456-aaa5-2d0b7b468a46.png">
<img width="913" alt="image" src="https://user-images.githubusercontent.com/124335793/216590991-0f7c7ea4-70ea-4dd8-a621-18a91bf0c0f4.png">
• V<sub>P-P</sub> = 7.66 V




 
