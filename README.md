# 4dof-steppermotor-arm
THIS REPO IS A WIP!!
a simplistic arm using a arduino uno and a cnc shield to control steppe rmotors with gearboxes!
no specific plans for uses for the arm, more general purpose is the idea, but tasks like pick and place, computer vision, and more are ideas.
The brains are a arduino uno with a cnc shield hat with DRV stepper drivers to control stepper motors with custom modular stackable planetary gearboxes made by me!
current plans are for the arm to have a reach of 415mm with a payload capacity of around 90 - 120g.
plans for control are a branch of GRBL firmware usually used for cartestian machines like 3d printers and pen plotters but modified to have a 4th axis (grbl4axis), with a live gcode feed from a larger computer to handle the expensive inverse kinematics.
