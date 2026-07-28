# 4dof-steppermotor-arm
NOTES** Whole project is a WIP as of July 27th, and all code was written by either claude sonnet 5, or opus 4.8, I do understand this takes out a huge part of the challenge of the project, but as of right now my understanding of coding is very far from custom windows python based apps, more like a HELLO WORLD type situation with my skills in coding so far, I do plan on learning more, but the focus of this project was the design of the arm, the electronic layout of microcontrollers, and the integration of it all. A future project may be far more software sided, but this is a hardware and design as of right now.
credit for arduino uno firmware gcobos on github

This arm is a 4DOF robotic arm using many parts from a broken creality Ender3 pro printer, all motors, and psu taken directly from that.

  Arm Overview
  This arm has 3 segments of arm, with 4 degrees of freedom with a initial yaw control with the rest rotating on the YZ plane (for the most part with one of the three offset by a bit).
  The motor driving avoids expensive robotic actuators, and instead of servos for arm positioning (still servos in the gripper setup), I use a custom design modular stackable 6 to 1 planetary gear reduction, linked to NEMA17 stepper motors all taken from an Creality ender3 pro printer.
  All motors use a double stacked system of my gearboxes (36 to 1) except my wrist joint which only uses a 6 to 1 setup.
  Load is offset from gearboxes using a rather simple fork design where a aluminum rod on the opposite side of the segment side with the gearboxes is pushed through some bearings in order to drastically reduce load on fragile plastic gearboxes.

  Arm control hardware

  My design currently utilizes several widely available and cheap pcbs in order to deliver power and signal to motors.
    All systems controlled by a 24v psu taken out of a Ender3 printer, with an additional xt60 wired onto another V+ and V- for a separate output for Servo driving.
    Reason I split control over 2 microcontrollers was because gcobos/grbl4axis firmware uses almost all memory on the uno and adding a servo control function by repurposing existing i/o on my cnc shield would be irresponsible, and unstable.
    
      Stepper motor control loop
      Using a Arduino uno flashed with the open source grbl4axis firmware based off of pre 0.9 grbl firmware usually used for Cartesian CNC systems such as pen plotters and 3 axis milling machines, but split to allow for a 4th axis repurposed from a spindle control node.
      Connected to said arduino is a CNC shield v3 with DRV stepper motor drivers with full steps no microstepping, as well as pins D12 and D13 enabled for stepper control in place of a spindle.
      takes in standard grbl gcode for control.
  
      Servo control loop
      Using a arduino nano CH340 clone (doesnt really matter) wired up to a PCA9685 Servo control board, powered by a MP1584 buck converter tuned down from 24v to ~5v for stepper power.

    Arm control software
      Note all software other than grbl4axis firmware for the uno (open source credit gcobos) were written by either claude sonnet 5 or opus 4.8
      before starting up the main app you will need to run the setup which installs necessary libraries

      Communication is all handled by via COM ports from the uno and nano (so yes unfortunately you will need to plug each in separately to i/o on host computer)
      The app sends standard grbl4axis gcode over the uno COM ports, and a custom firmware and communication for the nano (very simple).
      All solving is handled by the host PC not the microcontrollers, simply too much compute for the little ATMEGA on the uno.

        Features: standard FK and IK solving and homing setup with custom DH params, Motion tuning (speed and acceleration), a kinda terrible waypoint IK motion setup, a much cooler text writing setup, and finally gripper control

      Just to talk about the IK solving math I went with since its so cool to me I go with a analytical geometric (no matrices) solver using the law of cosines and simplifying the problem by using a tool angle, and looking at yaw separately.

    Thanks for making a great opportunity to grow as a builder stardance!!
