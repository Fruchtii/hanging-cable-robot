# hanging-cable-robot
Python controller for a cable robot that hangs from two motors and moves in 2D space using GRBL firmware


What it does
A cable robot system where a robot head hangs from two cables controlled by stepper motors mounted at the top corners of a work area. The robot can move to any X,Y position within a 70cm × 100cm area by winding and unwinding the cables.
How it works

Two stepper motors with cable spools at top corners
Robot head hangs from intersection of both cables
Python calculates required cable lengths for any position
G-code commands sent to Arduino with GRBL firmware
Uses triangle math (Pythagorean theorem) to convert X,Y coordinates to cable lengths

Hardware Required
Electronics

Arduino Uno R3 - Main controller board
2× NEMA 17 Stepper Motors - 200 steps per revolution
2× DRV8825 Stepper Drivers - With 1/4 microstepping (M0=H, M1=H, M2=L)
12V Power Supply - For stepper motors (minimum 3A)
USB Cable - For Arduino connection to computer
Jumper Wires - For connections
Breadboard or PCB - For wiring

Mechanical Parts

2× Cable Spools - 7.5mm radius (15mm diameter)
Strong Cable/Wire - Non-stretch, 60cm+ length per side
Work Area Frame - 70cm wide × 100cm tall mounting structure
Robot Head/End Effector - Your payload (seed dispenser, pen holder, etc.)
Motor Mounts - To attach motors to top corners
Pulleys (optional) - For cable guidance

Tools Needed

Soldering iron and solder
Wire strippers
Screwdriver set
Drill (for mounting)

Wiring
Arduino → DRV8825 (Motor 1 - Left)
D2 → STEP
D5 → DIR
GND → GND

Arduino → DRV8825 (Motor 2 - Right)  
D3 → STEP
D6 → DIR
GND → GND

DRV8825 Power:
12V+ → VMOT
GND → GND
5V → VDD (from Arduino 5V)
Software Setup
Prerequisites
bashpip install pyserial
Arduino Setup

Install GRBL firmware on Arduino Uno
Connect Arduino to computer
Note the COM port (Windows) or /dev/ttyUSB0 (Linux)

Running the Code
pythonpython main.py
Basic Usage
python# Move to center of work area
move_to_center()

# Move to specific position (in mm)
move_to_position(200, 300)

# Move to corners
move_to_corner("top-left")
move_to_corner("bottom-right")

# Check current position
get_current_position()
Coordinate System

Top-Left (0,0) ----------- Top-Right (700,0)
     |                              |
     |         Robot Head           |
     |            *                 |
     |                              |
     |                              |
     |       Center (350,500)       |
     |            *                 |
     |                              |
Bottom-Left (0,1000) ----- Bottom-Right (700,1000)

Origin (0,0): Top-left corner
X-axis: 0-700mm (left to right)
Y-axis: 0-1000mm (top to bottom)
Work area: 70cm × 100cm

Math Behind It
Cable lengths calculated using Pythagorean theorem:

Left cable: √(x² + y²)
Right cable: √((700-x)² + y²)

Use Cases

Automated vertical planting/seeding
2D positioning on vertical surfaces
Educational robotics projects
Precision drawing/plotting on walls
Research into cable-driven systems

Contributing
Feel free to submit issues and pull requests!
