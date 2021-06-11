# OP AMPS

##  Biasing 

 You give +V and -V and  add 100nF capacitor near the OP-Amps to filter out noise in the power rail. 
   -  circuit
		-  ![IMG_20210428_110711.jpg](IMG_20210428_110711.jpg)
    -  breadboard
		-  ![IMG_20210428_110727.jpg](IMG_20210428_110727.jpg)

## [[Scherz2016Practical#How Op-amp works|Open Loop]]
Used as a comparator (Sine to Square wave)
- Inverting output image
	- ![open_inverting.jpg](open_inverting.jpg)
- Inverting circuit configuration
	- ![OPEN_INVERT_circuit.jpg](OPEN_INVERT_circuit.jpg)
### What if we want output to go high whenever the signal crosses 5V instead of 0V like this?
 -  output image
	 -    ![open_invert_reference 1.jpg](open_invert_reference%201.jpg)
- circuit
	- ![OPEN_INVERT_REFERENCE_Circuit.jpg](OPEN_INVERT_REFERENCE_Circuit.jpg)
 
### We don't have 5V supply?
Need to develop voltage divider like below:
- circuit 
	- ![OPEN_INVERT_REFERENCE_VOLT_DIVID.jpg](OPEN_INVERT_REFERENCE_VOLT_DIVID.jpg)

### Problem with our stable power supply 
Normally bias voltages come from a stabilized power supply (either linear(5V) or switching type (+12V, -12V)) and thus they are formerly "stable". The use of a reference-voltage IC is welcome not exactly to get a stable signal, but rather to get an exact well-known voltage value regardless the actual bias voltage value. In fact, despite power supplies are stable, they can show slightly different absolute values at the output (for example mine is +12.4 V and yours is +12.2 V). A good circuit must be reliable and thus work the same with both supplies, that is why a known +5.00 V reference is great.
- circuit
	- ![[Reference Voltage.svg]]




### What if we have noisy input signal
- like this
	- ![[Input_signal.svg]]
- output
	- ![[noisy_signal_output.jpg]]
- noisy signal  simulating circuit
	-  ![[SIMULATING_NOISY_SIGNAL 1.jpg]]
-  [[Electronics#^e79c59|solution]]
## [[Scherz2016Practical#Positive Feedback|Positive Feedback]]

- Used as a comparator (Sine to Square wave)
- this feedback creates hysteresis, which is useful in case our [[Electronics#What if we have noisy input signal|input signal is noisy]]  ^e79c59
- circuit
	- ![[postive_feedback_circuit.jpg]]
- output
	- ![[postive_feedback.jpg]]
- It is worth to mention the reason of that: it is because a noisy signal near the threshold level has several fluctuations above and below that level (crossing) , thus yielding to multiple output transitions resulting in a correspondingly noisy output signal.

## [[Scherz2016Practical#Negative Feedback|Negative Feedback]]
 
 Used as an amplifier (to amplify a sensor output). The amplified signal could be inverted or non-inverted. Let us look into the inverted case:
- output
	-   ![negative_feedback.jpg](negative_feedback.jpg)
- circuit
	-   ![NEGATIVE_FEEDBACK_circuit.jpg](NEGATIVE_FEEDBACK_circuit.jpg)

Even if the amplified signal is inverted. It is  fine because there might be other stages, such as filtering, which outputs a negative signal. Thus, the final signal might be positive

#### Voltage Follower

![VoltageFollower.svg](VoltageFollower.svg)

We might face impedance problem.
- circuit
	-  ![voltage_follower_circuit.svg](voltage_follower_circuit.svg)

#### Summing two signals

###### circuit
![SUMMING.jpg](SUMMING.jpg)
######  output
![summing_output.jpg](summing_output.jpg)
Our sine wave has been shifted down by 2.5. Now, let us replace the 2.5 V ideal battery by a voltage divide (assume that we have only 12V power supply)


##### Summing w/o Ideal Battery
###### circuit
![SUMMING_VOLTAGE_DIVIDER.png](SUMMING_VOLTAGE_DIVIDER.png)
###### output
We  have different output unlike [[Electronics#^cf2f56|ideal batter case]]
![summing_voltage_divider_op.jpg](summing_voltage_divider_op.jpg)

##### Final summing circuit with [[Electronics#Voltage Follower|Voltage Follower]]

This is wrong! It doesn't link the subheading in a file.

![[SUMMING_VOLTAGE_FOLLOWER.png]]
#### Difference Amplifier 
 It gives DC offset to a AC signal. Useful for O/P for further digital processing.
##### Circuit
![[DIFFERENCE_circuit.jpg]]
##### Output
![[DIFFERENCE.jpg]]




# Digital Memory Block
## Asynchronous Memory Block
### circuit
![SR_Circuit.svg](SR_Circuit.svg)
### working
![SR_FLIP_FLOP.svg](SR_FLIP_FLOP.svg)

## Synchronous Memory Block
### Table
| D   | Q   |
| --- | --- |
| 0   | 0   |
| 1   | 1   | 
### circuit
![D-Flip-Flop.svg](D-Flip-Flop.svg)
### working
![D-Flip-Flop_Working.svg](D-Flip-Flop_Working.svg)

# DAC

## 1 BIT DAC

| Vin       | Vout  |
| --------- | ----- |
| Logic "0" | 0V    |
| Logic "1" | 1.25V | 

![[1-bit-dac.svg]]
## 4 BIT DAC
### Circuit
![[4-bit-dac.svg]]
### Formula
$$V_{out} = \frac{V_{b0}}{16} + \frac{V_{b1}}{8} + \frac{V_{b2}}{4} + \frac{V_{b3}}{2} $$
### Sheet
<iframe width="640" height="640" src="https://docs.google.com/spreadsheets/d/1mliIpx8XqzmBSA1S-oWHxYO6t5uIcWka9XG45dhSQrQ/edit?usp=sharing" frameborder="5" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### Marco Demo
![[a.mp4]]

## Doubling Time Period 
![[doubling_time_period.svg]]
## Waveform Generator
**Goal**: To generate a wave tooth signal (analog output) from digital input using a four bit DAC.

**Limitation 1**: The picoscope we used can generate only $\pm$ 2v. But, we need 0 to 5V signals.
**Solution**: Use a negative feedback op-amp with 2V reference voltage and set the resistor value to increase the gain so that max is 5V Instead of 4V.
- circuit
	- ![[TO_OFFSET_SIGNAL_BY_DC_VOLT.JPG]]

**Limitation 2**: We have one 5V signal. But, we need 3 more digital signals for our  [[Electronics#4 BIT DAC|4 BIT DAC]]
**Solution**: Daisy chain our[[Electronics#Synchronous Memory Block|D-Flip Flop]] like below. It will double the time period(half the frequency) at each stage.
![[abc.svg]]
## 4 bit vs 5 bit
![[vlc-record-2021-05-18-16h27m59s-module_2_lec_2.mp4-.mp4]]

## Latch Circuit
So far, we have used DAC using parallel wires from waveform generator like below:
![[square_to_sawtooth.svg]]

In reality DAC will be interfaced with a digital world.
![[Digit_to_dac.svg]]

Let us say, we want to go from 0011 -> 1001
 ```mermaid
graph LR; 
A["0011"]-->B & C; 
B["1011 (undesired)"]--> D["1001"]; 
C["0001 (undesired)"]--> D; 
```

The problem is we want the inputs to change at the same time for our DAC. To address this, we have a [[Electronics#Latch Circuit|Latch Citcuit]] like below:
![[latch_circuit.svg]]

## Shift Registers
Although, the [[Electronics#Latch Circuit]] solves an important problem of making sure that DAC receives input signal simultaneously. There is another problem. It requires parallel inputs. Lot of wires. Lot of problems. Thus, we have an [[Electronics#Shift Registers]] like below: 
![[Shift_register.svg]]
![[shift_reg_assembly.svg]]

## 3rd State in Digital

### My Doubt
**Problem**: one device is logical zero and another device is logical high will lead to conflict.

**Solution**: only one deice should have access to output line. The rest should be in a high impedance state thus they draw no current. This high impedance state is a physical sate but not a logical state.

**My Doubt**: But, instead of high impedance state if I'm able to guarantee that only one device can be operated(activated) at any point of time and the rest should be in logical zero. Then, it should also work right? So, why to keep the rest of the device in high output impedance when they are not activated?

### Marco Sartore Reply

My understanding is that high impedance state means drawing no current. It doesn't mean that only one device will be activated. Even when we keep the device in high impedance state, we have to ensure that only one device is activated right? When only one device is activated. Obviously, others would be in a logical zero. So, where is the need to draw little current? Thus, isn't there no need for high impedance state?

The high-impedance state need stems from the output stages of logical devices which are mostly so called "push-pull" (explaining this involves explaining transistors, a matter not actually included in the course and thus skipped by myself).

However, think to a transistor in a push-pull stage as to a switch, either closed or open and stack two of them taking the output at the middle, one connected  to +5V and one to GND as in the attached file.

Since either logic state connects output to +5V or to GND, if more than one unit at a time is active it is clear that the voltage at the output derives from an impedance network between +5V and GND, therefore it falls to some value which is in the "undefined voltage band", i.e. the region where it is not considered a logic 0 nor a logic 1.

The only solution to share a line among multiple push-pull devices is that just one is active at a given time, all the others showing a high impedance so that no impedance-divider networks are formed and hence the voltage stuck to either +5V or GND showing a clear 1 or 0 logical.

![[pushpull.jpg]]

### My Reply
So, basically this high impedance sate is where both switches are open and it is internal state and we need not do anything on the shared output line (like adding resistor, capacitor, etc, right?) In fact, it is  abstracted away from the user.  It is within digital device(orange box) and has to nothing to do with output lines right?

![[3-states-of-digital-device.svg]]

## DAC 8552

SPI interface with dac.

## long vs short?
![[hexa_overlow.mp4]]
# ADC

There is a trade off between high resolution vs speed of sampling (bandwidth). 90% of the cases work with high resolution.

# Circuit
## Resistor
I can understand the use of 100nF capacitor in power line to filter the noise and the use of  RC circuit to filter out the noise in analog lines. But, I could see a 100 ohm resistor in waveshare schematic as shown below.

**Doubt**: Well, the only reason to use a resistor is to limit the current and not any noise right? If that is the case when we are connecting SPI using jumper wires should we also add 100 Ohm resistor or is it just a PCB thing which we do because the lines in PCB have very low resistance?

![[100r.png]]

### Marco Sartore Reply

  
Adding a resistor in series along a digital communication line prevents a phenomenon called "ringing" and due to the undesired small capacitances found by the signal along the path. Basically, after a step excitation of the line, say to go from logical 0 to logical 1 (or the opposite) we expect the signal at the line end to move accordingly, as a nice step.

What actually happens is that the signal increases (or decreases) more or less sharply and with more or less oscillations, depending on the line length, path, impedance, capacitance and inductance. Any path onto a PCB suffers from this, but also a simple wire. See attached picture. A small resistor along the line helps to filter out this effect and to keep ringing low enough to maintain signal consistency between transmitter and receiver (\*).

As a rule of thumb, as long as the circuit is simple and the paths are very short (10cm) or very well routed then series resistors can be skipped.

(\*) I did not use the terms "master" and "slave" because both can actually transmit and receive. For example, about SPI think to lines MOSI and MISO.

![[ringing.png]]

