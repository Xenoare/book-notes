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

