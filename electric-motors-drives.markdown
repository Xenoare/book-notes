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

## Chapter 3 : Conventional D.C. Motors
+ In principle, all that has to done is to alter the number of turns and the size of wire making up the coils in the machine. A 12 V, 4 A motor, for example, is more or less equivalence of 24 V, by winding its **coil twice**.
+ The input power and output power would be unchanged, and externally there would be no change in appearance, except that the terminals might be a bit smaller. 
+ Torque is produced by the interaction between the axial current-carrying conductors on the  rotor and the radical magnetic flux producced by the stator. The flux or `excitation` can be furnished by permanent magnets or by field windings.
+ The advantage of permanent magnets is that this required no electrical supply for the field, hence the overral size of the motor can be smaller. But, the strength of the field cannot be varied, so one possible option for control is ruled out.
+ We should recall that in the Chapter 1, that the mechanical output power actually comes from the field system. The excitation acts like a **catalysts**, making the energy conversion possible but not contributing to the output.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/11ff5a21-0893-4736-a839-d33cb37d68f8"/>
</p>

+ The main power of the circuit consist of a set of idential coils would in the **slots of the motor** (known as the armature). Current is fed into and out of the rotor via carbon `brushes` which make sliding contact with the `commutator`, which consist of insulated cooper segments counted on a cylindrical former.
+ The purpose of the commutator is to ensure that regardlesss of  the position of the rotor, the pattern of current flow in the rotor is always as shown below
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/34d32fc6-9638-4257-b558-68d6bedcc1e8"/>
</p>

+ Current enters the rotor via one brush, flows through all the rotor coils in the directions shown in Figure above and leaves via the other brush.
+ It is straightforward to show that the total torque developed is given by
$$T = K_{T}\Phi I$$

+ Where $\Phi$ is the total produced by the field, and $K_{T}$ is constant for a given motor. We can see that by this eq. the direction of the torque can be reversed by either reversing either the armature current (_I_) or the flux ($\Phi$), let's say when we want to motor to run in reverse.
+ Broadly speaking, the higher the number of coils (and commutator segments) the better, because the ideal armature would be one in which the pattern of current on the rotor corresponded to a `current sheet`, rather than a series of discrete packets of current.
+ Returning on how the commutator work, we note that from the commutator figure, for half a revolution - while side _a_ is under the N pole and the side _b_ is under the S pole. The current needs to be a positive in side _a_ and negative in side _b_ in order to produce positive torque.
+ For the other half revolution, while side _a_ is under the S pole and side _b_ is under the N pole, the current must flow in the opposite direction through the coil for it to continue to produce positive torque.
+  This reversal of current takes place in each coil as it passes through the interpolar axis, the coil being ‘switchedround’ by the action of the commutator sliding under the brush.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/acc595a6-015e-470b-8e02-e3781575dfed"/>
</p>

+ The diagram above shows that a single coil fed via the commutator, and burshes with current that always flows in at the top brush
+ In the left-hand sketch, coil-side _a_ is under the N pole and carries positive current because it is connected to the shaded commutator segment which in turn is fed from the top brush. Side _a_ therefore exposed to a flux density directed from left (N) to right (S) in the sketch, and will therefore experience a downward force.
+ Conversely, side _b_ has negative current but it also lies in a Xux density directed from right to left, so it experiences an upward force. There is thus an anti-clockwise torque on the rotor.
+ When the rotor turns to the position shown in the sketch on the right, the current in both sides is reversed, because side _b_ is now fed with the positive current v3 ia the unshaded commutator segments.
+ The direction of force on each coil also reversed, which is exactly what we want in order for the torque to remain clockwise. Overall, the torque is constant.
+ The main difficulty in achieving good commutation arises because of the sel inductance of the armature coils and the associated stored energy. Because, as we've seen earlier, the inductive circuits **tend to resist change in current**, and if the current reversal has not been fully completed by the time the brush slides off the commutator in question, there will be a spark at the trailing edge of the brush.

+ It has already been mentioned that the flux is usually constant at its full value, that can be written in the form
$$T = K_{t}I$$
$$E = K_{e}\omega$$

+ Where $K_{t}$ is the motor torque constant, and the $k_{e} is the e.m.f constant, where the $\omega$ is the angular speed in `rad/s`.
+ Remember that the torque constant (Nm/A) and the e.m.f constant (V/rad/s) it is a different physical phenomena, where in fact 1 Nm/A = 1 V/rad/s
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/01964e92-9058-4721-aff3-42f3d1eb872f"/>
</p>

+ Under the motoring conditions, the motional e.m.f. E is alawys opposes the applied voltage V, and for this reason it is referred to as the `back e.m.f.`, hence for the current to be force into the motor, voltage V must be greater than the e.m.f E, the armature circuit voltage eq. is given by.
$$V = E + IR + L\frac{d\textit{I}}{d\textit{t}}$$

+ Where the last term represent the inductive volt-drop due to the armature self-inductance.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/0059d93b-0d86-4f6b-9f40-1156ac7100ac"/>
</p>

+ The motor can operate at any speed up to base speed, and at any
torque (current) up to the rated value by appropriate choice of armature
voltage.
+ To run faster than the base speed, then the field flux must be reduced as indicated by this eq. where _n_ is the speed
$$V = E = K_{E}\Phi n$$ that is equivlent to $$n = \frac{V}{K_{E}\Phi}$$

+ This operation is known as the `field wweakening`. For example, that by halving the flux (keeping the armature voltage at its full value), the no-load speed is doubled.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/b7df203f-fab9-4df1-ab55-3494693cbd58"/>
</p>

+ The increase in speed is however obtained at the expanse of available torque, which is proportional to `flux` times `current`.
+ To sum up, the speed is controlled by these.
    1. Below base speed, the Xux is maximum, and the speed is set by the armature voltage. Full torque is available at any speed.
    2. Above base speed, the armature voltage is at (or close to) maximum and the flux is reduced in order to raise the speed. The maximum torque available reduces in proportion to the flux.

## Chapter 4 : D.C. Motor Drives
+ For the motors up to a few kilowatts the armature converter can be supplied from either single-phase or three-phase mains (but generally speaking, for the larger motors three-phased is always being used).
+ The smoothing effect of the armature inductance is important proces in achieving succsfull motor operation i.e. that the armature acts as a low-pass filter, blocking most of the rippl , and leading to a more or less constant armature current.
+ There wil come a point where the current ripple will touches the zero-current line (such as the  discountinuous current) in the continuous d.c. motors operator from any given the converter delay angle.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/4616f8ff-0e54-47bd-be27-c19368cdc06e"/>
</p>

+ Typical armature voltage and current waveforms in the discountinuous mode are given in the graph below. The armature current consisting of the discrete pulses of current that occour only while the armature is connected to the supply, with zero current for the period (representated with $\theta$).
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/7fcfc50b-ed03-4f3b-8ab4-c4a95041e7b8"/>
</p>

+ So faw, we've looked at the converter as a `rectifier`, where it supplying power from the a.c. mains to a d.c. machine running in the positive direction and acting as a `motor` (This stuff is called as one quadrant operation by the reference to quadrant 1 of the complete torque-speed plane)
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/3ee6c37c-fef5-45da-b304-26cf2e6805f8"/>
</p>

+ What if the case that we want to reverse or achieve regenerative braking. The good news is that the `machine` itself is a `bidirectional` energy converter, where as if we apply a positive voltage `V` greater (`>`) than `E`. Hence, the current flows into the armature and the machine as the motor.
+ Based on this, if we reduce the voltage `V`, then the `E` is less, the torque and power automatically rever direction, and the machine acts as a generator. Converting the mechanical energy into electrical energy.
+ When the motor is running at full speed forward, the converter delay angle will be small, and the converter output voltage `V` and current `I` will both be positive, as the Figure shown below.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/d07eafb4-baee-4654-ade4-931adefe7181"/>
</p>

+ In order to brake the motor, the torque has to be reversed, the only way this can be done is by reversing the direction of the armature current. (The converter can only supply positive current, so to reverse the motor torque, we have to reverse the armature connection either by using `switch` or `contactor`)
+ One of the drawbacks of a converter-fed d.c. drive is that the supply power factor is very low when the motor is operating at the high torque (i.e. `high current`) and low speed (i.e. low `armature voltage`), and it less than unity even at base speed and full load.

+ The closed-loop current controller, or current loop is at the heart of the drive system and is indicated by the `shaded region` in the figure above.
<p align="center">
    <img width="450" height="150" src="https://github.com/Xenoare/book-notes/assets/67181778/baca8fd0-7ad0-405a-a120-e9a06219ee5a"/>
</p>

+ The purpose of the current loop is to make the actual motor curerent follow the current reference signal ($I_{ref}$), it does this by comparing a feedback signal of actual motor current with the current reference signal, and amplifying the difference to control the firing angle $\alpha$.
