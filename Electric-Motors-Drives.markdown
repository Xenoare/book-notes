by Austin Hughes

## Chapter 1 : Electric Motor
+ Magnetic Field (`Excitation`) is essential to the working of the motor, it acts only as a catalyst and all of the mechanical output power comes from the electrical supply to the conductors on which force is develop.
+ The flux density (**B**) is simply the flu in the tube ($\Phi$) divided by the cross sectional area (**A**) of the tube.
$$B = \frac{\Phi}{A}$$

+ In the SI system, the unit of magnetic flux is the Weber (Wb), the flux density is clearly one weber per square meter ($\frac{Wb}{m^2}$) or known as the one Tesla (T).
+ The force on a wire length _l_ and expose to a uniform magnetic flux density _B_ throughput its length given by the simple expression, where _F_ is newtons, _B_ in tesla, _I_ in amperes, and _l_ in metres.
$$F = BIl$$

+ Majority of motors, the working maggnetic field is produced by coils of wire carrying current, we nomally called that Magnetic Circuit.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/929b9696-0514-449a-82db-94b17abec8ee"/>
</p>

+ Figure above is somewhat artificial as current can only flow in a complete circuit, so there must always be a return path.

+ One obvious way to increase the flux density is to increase the **current** in the coil or add more **turns**. We double the total flux, thereby doubling the flux density everywhere.
+ Ability of coil to produce flus in terms of **Magnetomotive Force (MMF)**. THe MMF is a product of number of turns and the current and is thus _ampere-turns_.
+ We can make use of equivalent `magnetic Ohm's law` by introducing the idea of Reluctance (**R**). The reluctance gives a measure of how difficult it is for the  magnetic flux to complete its circuit, in the same way that resistance indicates how much opposition the current encounters in the electric circuit.
$$Flux = \frac{MMF}{Reluctance} = \Phi = \frac{NI}{R}$$

+ The air path is a poor magnetic material, and therefore constitutes a high reluctance.
+ With an iron magnetic circuit, some flux can low (in the air) even before the iron is installed, and sometimes some will still leak into the air.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/3343661f-5d78-49d7-84a1-15602f518d10"/>
</p>

+ To determine how much flux will cross the gap, we need to know its reluctance. As might be expected, the reluctance is given by, where $\mu_{0}$ is a Permeability of free space or magnetics propertis of a vacuum. The value of this constant is $4\pi \times 10^{-7} H/M$
$$R_{g} = \frac{g}{A\mu_{0}}$$

+ To summarize, to calculate the flux $\Phi$, we use the magnetic Ohm's law
$$\Phi = \frac{MMF}{R} = \frac{NIA\mu_{0}}{g}$$

+ But we are usually interested in the flux density in the gap, rather than the total flux, hence we got the equation
$$B = \frac{\Phi}{A} = \frac{\mu_{0} NI}{g}$$

+ There's a limit to the flux density at which iron can be operated, at this state will reach a point where the magnetic material in the core become saturated, which means that the material can no longer support the increase in magnetic flux , even though the current (and hence the magnetic field strength) continues to rise.
+ This state is remains true as long thee flux density is remains below about 1.6 - 1.8 T, before saturation is happening.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/761fed3c-d045-4cad-afdc-b19e6459879d"/>
</p>

+ The resultant torque or couple (T) depends on the radius of the rotor (r) and given by, where F is a Total Tangential Force of $BIl$
$$T = Fr$$

+ The Slotting (put the coil in the teeth of a rotor), we enable the reluctance of the magnetic circuit to be reduced and transfer the force from the conductor themself to the sides of the iron teeth. which are robust and well to transmit the resulting torque to the shaft.
+ To maximise the torque, we want as much current in the rotor conductors. Normally, we would use the copper as the highest current density ($2 - 8 A/mm^{2}$), also the cross-sectional area of the slots to accomodate copper as much as possible.

+ In linear system, work is force times distance, but in rotary terms work is torque times angle. Hence, the unit is **newton-metres**, and the angles are measured in **radians**
$$W = F \times (r \times \theta) = (F \times r) \times \theta = T \times \theta$$

+ The one obvious disadvantage of a small high-speed motor and gearbox is that the acccoustic noise (both from the motor itself and from the power transmisson) is higher than it would be from a larger direct drive motor.
+ When noise must be minimised, a direct drive motor is therefore preferred, despite its larger size.
+ In order to link the mechanical and electric worlds, we need to maintain the **stationary condition**, where the current in the conductor is determined by the mass of the mechanical load.
$$T = mg = BIl, I = \frac{mg}{BI}$$

+ The power-balanced from the both heat in the conductor, and the mechanical output power.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/730451df-40bf-4a0b-b85e-13d669da9b43"/>
</p>

+ In the e.m.f, if E is less than the applied voltage V, the current will be positive, and the electrical power will flow from the source, resulting in motoring action. On the other hand if E is larger than V, the current will flow back to the source, and the conductor will be acting as a generator.
+ Motoring implies that the conductors is moving in the same direction as the electromagnetic force (_BIl_) at a speed such that the back e.m.f. (_Blv_) is less that the applied voltage _V_.

## Chapter 2 : Power Electronic Converters For Motor Drives
+ A characteristic of power electronic converters which is shared with most electrical system is that they have very little capacity for storing energy.
+ It would be better if a significant amount of energy could be stored within the converter itself; short-term energy demands could then be met instanly, thereby reducing rapid fluctuations in the power drawn from the mains.
+ Transistor is effectively a controllable resistor, i.e. the resistance between collector and emitter depends on the current in the base-emitter junction.
+ When an inductance _L_ carries a current _I_, the energy stored in the magnetic field (_W_) is given by
$$W = /frac{1}{2}LI^2$$

+ A diode is a one-way valves because it offers very little resistance to the current flowing from anode to cathode. Given the circuit, when the transistor is on, the current _I_ flows through the load, but not through the diode as the on A. Otherwise, when transistor is turned off, the current and the battery drops suddenly to zero. But the stored energy in the inductance means that its current cannot suddenly disappear, as the in the B.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/0d1d9201-2a0b-4c90-af1a-39cd29999772"/>
</p>

+ The vast majority of drives of all types draw their power from constant voltage 50 or 60 Hz mains, and in nearly all mains converters the first statge consist of a rectifier which converts the a.c. to a crude from of d.c.
+ Thyristor is an electronic switch, with two mains terminals (anode and cathode) and a `switch-on` terminal (gate).
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/3523bc80-2e30-40a3-b479-856c89ad8088"/>
</p>

+ THe primary reason for the use of thyristors is that they are cheaper and their is that they are cheaper and their voltage and current ratings to higher levesl than power transistors.
+ Given the converter circuit below that consist of four thyristors, and connected in bridge formation
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/adae8495-b090-4f90-8bb3-2a38e162d9e8"/>
</p>

+ Thyristors T1 and T4 are fired togehter when terminal A of the supply is positive, while on the other half-cycle, when B is positive, thyristors T2
and T3 are fired simultaneously.
+ There are two pulses per mains cycle, hence the desc of `two-pulse` or full-wave. At every instant the load is either connected to the mains by the pair of switches T1 and T4, or it is connected the other way up by the pair of switches t2 and T3, or it is disconnected.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/41fbee30-0cc0-4d6a-b79e-b313c0bf6095"/>
</p>

+ Most power electronic converters emit whining or humming sounds at frequencies correcponding to the fundamental and harmonics of the switching frequency, though when the converter is used to feed a motor, the sound from the motor is usually a good deal louder than the sound from the converter itself.
+ The principal factors which govern the thermal resistance of a heatsink are the total surface area, the condition of the surface and the air flow.
+ Most converters use extruded aluminium heatsinks, with multiple fins to increase the efective cooling surface area and lower the resistance.
+ A typical layout for a medium-power (200 kW) converter are like this.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/b20e6571-7649-42c0-a53b-5b05c412e716"/>
</p>
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/d034f3af-fc9f-45b4-bdbc-fc693305c9d4"/>
</p>
