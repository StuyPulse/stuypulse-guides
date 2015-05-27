# Java Command Based Programming Guide Team 694

Java: Command Based Programming in Eclipse

## General

- How to Create a New Robot Project
	1. Scroll over “File” on the menu bar.
	2. Scroll over “New” and click on option called “Project…” near the top.
	3. Under “WPILib Robot Java Development,” select “Robot Java Project” and click “Next.”
	4. Create a project name, select the Command-Based Robot option, and click “Finish.”

- How to Import a Robot Project from GitHub
	1. Scroll over “File” on the menu bar and click “Import.”
	2. Under “Git,” select the option “Projects from Git” and press “Next.”
	3. Select “Existing local repository” and click “Next.”
	4. Click “Add…”, click browse, and choose a file that contains an existing repository.
	5. Click “Finish” and the local repository should appear on the list. Select it and press “Next.”
	6. Press “Next” and then “Finish.”
*If there is a red exclamation point next to the newly created robot project, create a new robot project in Eclipse, and it should work.

## Example Subsystems

### Pneumatics

- If you are using a single solenoid, it's basically the same thing but use one solenoid variable

```
package edu.stuy.subsystems;

import edu.wpi.first.wpilibj.Solenoid;
import edu.wpi.first.wpilibj.command.Subsystem;
import edu.stuy.commands.ExampleCommand; 

public class Pneumatics extends Subsystem {

   // Put methods for controlling this subsystem
   // here. Call these from Commands.

    private Solenoid shortPistonOut;
    private Solenoid shortPistonIn;
    private Solenoid longPistonOut;
    private Solenoid longPistonIn;

    public Arms() {
        shortPistonOut = new Solenoid(1);
        shortPistonIn = new Solenoid(2);
        longPistonOut = new Solenoid(3);
        longPistonIn = new Solenoid(4);
    }

    public void initDefaultCommand() {
        // Set the default command for a subsystem here.
        //setDefaultCommand(new MySpecialCommand());
	setDefaultCommand(new ExampleCommand());
    }

    private void setShortPistonOut(boolean out) {
        shortPistonOut.set(out);
        shortPistonIn.set(!out);
    }

    private void setLongPistonOut(boolean out) {
        longPistonOut.set(out);
        longPistonIn.set(!out);
    }
}
```
### Drivetrain:

- Though this example uses CANTalon's, similar formats can be used for other motor controllers

```
package edu.stuy.subsystems;

import edu.stuy.commands.TankDriveCommand;
import edu.wpi.first.wpilibj.CANTalon;
import edu.wpi.first.wpilibj.RobotDrive;
import edu.wpi.first.wpilibj.command.Subsystem;

public class Drivetrain extends Subsystem {

    private CANTalon frontLeftMotor;
    private CANTalon rearLeftMotor;
    private CANTalon frontRightMotor;
    private CANTalon rearRightMotor;
    private RobotDrive robotDrive;

    public Drivetrain() {
        frontLeftMotor = new CANTalon(1);
        rearLeftMotor = new CANTalon(2);
        frontRightMotor = new CANTalon(3);
        rearRightMotor = new CANTalon(4);
        robotDrive = new RobotDrive(frontLeftMotor, rearLeftMotor, frontRightMotor, rearRightMotor);
    }

    public void initDefaultCommand() {
        setDefaultCommand(new DrivetrainTankDriveCommand());
    }

    public void tankDrive(double leftSpeed, double rightSpeed) {
        robotDrive.tankDrive(leftSpeed, rightSpeed);
    }

    public void arcadeDrive(double moveValue, double rotateValue, boolean squaredInput) {
        robotDrive.arcadeDrive(moveValue, rotateValue, squaredInput);
    }
}
```

## Example Commands

### Pneumatics:

```
package edu.stuy.commands;

import edu.stuy.Robot;
import edu.stuy.util.ArmsPosition;
import edu.wpi.first.wpilibj.command.Command;

public class PneumaticsCommand extends Command {

    public PneumaticsCommand() {
        // Use requires() here to declare subsystem dependencies
        // eg. requires(chassis);
        requires(Robot.pneumatics);
    }

    // Called just before this Command runs the first time
    protected void initialize() {
    	// Put this in init so it is run once and before isFinished()
        Robot.pneumatics.setShortPistonOut(true);
        Robot.pneumatics.setLongPistonOut(true);
    }

    // Called repeatedly when this Command is scheduled to run
    protected void execute() {
    }

    // Make this return true when this Command no longer needs to run execute()
    protected boolean isFinished() {
    // Return true so execute only runs once
        return true;
    }

    // Called once after isFinished returns true
    protected void end() {
    }

    // Called when another command which requires one or more of the same
    // subsystems is scheduled to run
    protected void interrupted() {
    }
}
```

### Tank Drive:

```
package edu.stuy.commands;

import edu.stuy.Robot;
import edu.wpi.first.wpilibj.command.Command;

public class TankDriveCommand extends Command {

    public TankDriveCommand() {
        requires(Robot.drivetrain);
    }

    protected void initialize() {
    }

    protected void execute() {
	Robot.drivetrain.tankdrive(Robot.oi.driverPad.getLeftY(), Robot.oi.driverPad.getRightY()
    )
    
    // Make this return true when this Command no longer needs to run execute()
    protected boolean isFinished() {
        // Because this is a default command for a subsystem (Drivetrain)
        // it should not end when the button is de-pressed.
        return false;
    }

    // Called once after isFinished returns true
    protected void end() {
    }

    // Called when another command which requires one or more of the same
    // subsystems is scheduled to run
    protected void interrupted() {
    }
}
```

### Arcade Drive:

```
package edu.stuy.commands;

import edu.stuy.Robot;
import edu.wpi.first.wpilibj.command.Command;

public class ArcadeDriveCommand extends Command {

    public ArcadeDriveCommand() {
        requires(Robot.drivetrain);
    }

    protected void initialize() {
    }

    protected void execute() {
	Robot.drivetrain.arcadedrive(Robot.oi.driverPad.getLeftY(), Robot.oi.driverPad.getRightX()
    )

    protected boolean isFinished() {
        return false;
    }

    protected void end() {
    }

    protected void interrupted() {
    }

```


## Deploying Code Onto roboRIO

- To load code onto the roboRIO:
	1. Press the run button (first green play button from the left) on the tool bar.
	2. Choose the “WPILib Java Deploy” option.
	3. Press “OK.”
- Unlike the incompetent cRio, the code will deploy to the roboRIO in around ten to fifteen seconds.


## Pro Tips
- Don't use LabView
- Document your code as you write it


## Other Resources
FIX LATER
- Screensteps: [https://wpilib.screenstepslive.com/s/4485](https://wpilib.screenstepslive.com/s/4485)
- WPI Robotics Library Documentation: http://users.wpi.edu/~bamiller/WPIRoboticsLibrary/main.html