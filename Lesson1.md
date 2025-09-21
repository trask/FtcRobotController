# Lesson 1: First Time Setup Guide for Tank Drive Teleop

## What is Tank Drive?

Tank drive is one of the simplest and most common driving methods in robotics. It's called "tank drive" because it mimics how military tanks move:

- **Left joystick** controls the **left wheels** of your robot
- **Right joystick** controls the **right wheels** of your robot
- Push both joysticks forward → robot moves forward
- Pull both joysticks backward → robot moves backward
- Push left joystick forward, pull right joystick backward → robot turns right
- Push right joystick forward, pull left joystick backward → robot turns left

Tank drive gives you precise control but requires coordination between both hands. It's perfect for learning because the code is simple and the behavior is predictable.

---

## Step 1: Install Required Software

### 1.1 Install GitHub Desktop
1. Go to [https://desktop.github.com/](https://desktop.github.com/)
2. Download and install GitHub Desktop
3. When GitHub Desktop opens and asks you to sign in, click **"Skip this step"** or **"Continue without signing in"**
4. You can still clone public repositories without an account!

**Note:** You can always sign in later if you want to contribute back to the community or create your own repositories.

### 1.2 Install Android Studio
1. Go to [https://developer.android.com/studio](https://developer.android.com/studio)
2. Download Android Studio
3. Run the installer and follow the setup wizard
4. When prompted, install the Android SDK and additional components

---

## Step 2: Get the FTC Robot Controller Code

### 2.1 Clone the Repository with GitHub Desktop
1. Open GitHub Desktop
2. Click "Clone a repository from the Internet"
3. In the URL tab, paste: `https://github.com/FIRST-Tech-Challenge/FtcRobotController`
4. Choose where to save it on your computer (remember this location!)
5. Click "Clone"

**Note:** Even without signing in, you can clone any public repository (like this FTC one). GitHub Desktop will download all the code to your computer.

### 2.2 Open the Project in Android Studio
1. Open Android Studio
2. Click "Open an Existing Project"
3. Navigate to where you cloned the repository
4. Select the `FtcRobotController` folder
5. Click "OK"
6. Android Studio will take a few minutes to load and sync the project

---

## Step 3: Create Your Tank Drive Code

### 3.1 Copy the Sample Code
1. In Android Studio's Project panel (usually on the left), navigate to:
   ```
   FtcRobotController → src → main → java → org.firstinspires.ftc.robotcontroller.external.samples
   ```
2. Find `BasicOpMode_Linear.java`
3. Right-click on it and select "Copy"

### 3.2 Paste into TeamCode
1. Navigate to:
   ```
   TeamCode → src → main → java → org.firstinspires.ftc.teamcode
   ```
2. Right-click in the teamcode folder and select "Paste"
3. The file will be copied as `BasicOpMode_Linear.java` - that's fine, no need to rename it!

### 3.3 Modify the Code for Tank Drive

Open your newly copied file and make these changes:

#### Change 1: Remove @Disabled
Find these lines at the top:
```java
@TeleOp(name="Basic: Linear OpMode", group="Linear OpMode")
@Disabled
public class BasicOpMode_Linear extends LinearOpMode
```

Simply comment out or delete the `@Disabled` line:
```java
@TeleOp(name="Basic: Linear OpMode", group="Linear OpMode")
// @Disabled  <- Comment out or delete this line
public class BasicOpMode_Linear extends LinearOpMode
```

That's it! No need to change anything else in this section.

#### Change 2: Switch from POV to Tank Drive
In the `runOpMode()` method, inside the `while (opModeIsActive())` loop, find these lines:
```java
        // POV Mode uses left stick to go forward, and right stick to turn.
        // - This uses basic math to combine motions and is easier to drive straight.
        double drive = -gamepad1.left_stick_y;
        double turn  =  gamepad1.right_stick_x;
        leftPower    = Range.clip(drive + turn, -1.0, 1.0) ;
        rightPower   = Range.clip(drive - turn, -1.0, 1.0) ;

        // Tank Mode uses one stick to control each wheel.
        // - This requires no math, but it is hard to drive forward slowly and keep straight.
        // leftPower  = -gamepad1.left_stick_y ;
        // rightPower = -gamepad1.right_stick_y ;
```

Comment out the POV lines and uncomment the Tank lines:
```java
        // POV Mode uses left stick to go forward, and right stick to turn.
        // - This uses basic math to combine motions and is easier to drive straight.
        // double drive = -gamepad1.left_stick_y;
        // double turn  =  gamepad1.right_stick_x;
        // leftPower    = Range.clip(drive + turn, -1.0, 1.0) ;
        // rightPower   = Range.clip(drive - turn, -1.0, 1.0) ;

        // Tank Mode uses one stick to control each wheel.
        // - This requires no math, but it is hard to drive forward slowly and keep straight.
        leftPower  = -gamepad1.left_stick_y ;
        rightPower = -gamepad1.right_stick_y ;
```

---

## Step 4: Upload Code to Robot

### 4.1 Connect to Robot
1. Connect your laptop to the Control Hub using a USB cable
2. Make sure the Control Hub is powered on
3. Wait for Android Studio to recognize the device (you should see it in the device dropdown)

### 4.2 Build and Deploy
1. In Android Studio, click the green "Run" button (play icon)
2. Select your Control Hub device from the list
3. Android Studio will build the app and install it on the Control Hub
4. Wait for "BUILD SUCCESSFUL" message (may take up to a minute the first time)

---

## Step 5: Connect Driver Hub to Robot

### 5.1 Wireless Connection
1. On the Driver Hub, touch the settings (gear icon) or three dots (⋮) in the upper right corner
2. Select **Settings** (you may need to scroll down)
3. Tap **Pair With Robot Controller**
4. Tap **WiFi Settings**
5. You should see a screen that looks like Android WiFi settings
6. Select your Control Hub's WiFi network (usually named something like "FTC-XXXX" where XXXX are numbers)
7. Wait for the connection status to show green
8. **Verification:** If connected successfully, you should see the robot's name displayed in red text on the WiFi Settings page

**Battery Status:** While on the Driver Hub home screen, you can monitor your robot's health. The Driver Hub shows:
- **Driver Hub battery percentage** (top of screen)
- **Robot battery voltage** (displayed to the right) - Green indicates a healthy, charged battery (~12V). Yellow or red means the battery should be replaced.

---

## Step 6: Configure Motors on Driver Hub

### 6.1 Access Robot Controller App
1. On the Driver Hub (the separate touchscreen device), open the "FTC Robot Controller" app
2. The app should show that the robot is ready and connected

### 6.2 Configure Hardware
1. Touch the three dots (⋮) in the upper right corner
2. Select "Configure Robot"
3. If no configuration exists, touch "New" and give it a name
4. Touch "Control Hub Portal"
5. Touch "Control Hub"

### 6.3 Configure Motors
1. Look at your physical robot and identify which ports your drive motors are connected to
2. Touch "Motors" to access the motor configuration screen
3. Touch the port number where your left motor is connected (for example, port 0 is at the top)
4. Select "DC Motor" from the list
5. Name it exactly `left_drive` (this must match the name in your code)
6. Touch "Done"
7. Repeat for the right motor, naming it exactly `right_drive`
8. Touch "Save" to save your configuration

**Important:** The motor names in your configuration MUST match the names in your code:
- Code says: `leftDrive = hardwareMap.get(DcMotor.class, "left_drive");`
- Configuration must have a motor named: `left_drive`

---

## Step 7: Connect and Test Drive

### 7.1 Connect the Gamepad
1. Connect your gamepad to the Driver Hub (usually via USB cable)
2. Press **Start + A** on the gamepad to initialize it
3. On the Driver Hub, the gamepad should appear as "Gamepad 1"

### 7.2 Start Your Program
1. On the Driver Hub, open the teleop menu
2. You should see your "Basic: Linear OpMode" program in the list
3. Select it by touching it
4. Press the "INIT" button
5. Once initialization is complete, press "START" (it's the play button ▶)

### 7.3 Test Drive!
1. Gently push the left joystick forward → left wheels should move forward
2. Gently push the right joystick forward → right wheels should move forward
3. Push both joysticks forward → robot should move forward
4. Try different combinations to test turning

---

## Understanding Your Tank Drive Code

Let's walk through the important parts of your code:

### Motor Declaration
```java
private DcMotor leftDrive = null;
private DcMotor rightDrive = null;
```
These lines create variables to control your motors. Think of them as remote controls for each motor.

### Hardware Initialization
```java
leftDrive  = hardwareMap.get(DcMotor.class, "left_drive");
rightDrive = hardwareMap.get(DcMotor.class, "right_drive");
```
This connects your code variables to the actual physical motors you configured. The strings "left_drive" and "right_drive" must match exactly what you named them in the configuration.

### Motor Direction
```java
leftDrive.setDirection(DcMotor.Direction.REVERSE);
rightDrive.setDirection(DcMotor.Direction.FORWARD);
```
Most robots need one side reversed because the motors face opposite directions. If your robot drives backward when you want forward, change `REVERSE` to `FORWARD` or vice versa.

### The Main Drive Loop
```java
// run until the end of the match (driver presses STOP)
while (opModeIsActive()) {
    // Tank Mode uses one stick to control each wheel.
    leftPower  = -gamepad1.left_stick_y ;
    rightPower = -gamepad1.right_stick_y ;

    // Send calculated power to wheels
    leftDrive.setPower(leftPower);
    rightDrive.setPower(rightPower);
}
```

This is the heart of tank drive in a LinearOpMode:
1. The `while (opModeIsActive())` loop runs continuously until the match ends
2. `gamepad1.left_stick_y` reads how far forward/backward the left joystick is pushed (-1 to +1)
3. `gamepad1.right_stick_y` reads how far forward/backward the right joystick is pushed (-1 to +1)
4. The minus sign (`-`) flips the direction because pushing forward gives negative values
5. `leftPower` and `rightPower` store these values
6. `setPower()` sends the power levels to the actual motors

### Telemetry (Data Display)
```java
telemetry.addData("Motors", "left (%.2f), right (%.2f)", leftPower, rightPower);
telemetry.update();
```
This shows the motor power values on the Driver Hub screen while your program is running. The `addData()` line prepares the information to display, and `telemetry.update()` actually sends it to the screen. You'll see something like "Motors: left (0.75), right (-0.50)" displayed on the Driver Hub screen, which is helpful for debugging.

---

## Helpful Tips and Troubleshooting

### Driver Hub Issues
- **Error messages (yellow or red):** Try restarting the robot first
- **Power cycling:** Turn off the hub, wait 30 seconds, then turn it back on. This can resolve many connection issues
- **Driver Inspection Report:** In settings, there's a page called "Driver Inspection Report" that shows WiFi connections and Driver Station version - useful for troubleshooting

### Configuration Problems
- **"Could not find left_drive" error:** Check that motor names in configuration match exactly (case-sensitive)
- **Robot drives backward:** Change motor directions in code from `FORWARD` to `REVERSE` or vice versa
- **Robot only turns in circles:** One motor direction is wrong, or check that both motors are connected and configured

### Visual Resources
- **Screenshots and videos:** The original Project Robotica tutorial at https://projectrobotica.wiki/wiki/FTC:Driver_Hub_Tutorial contains helpful screenshots of each configuration step and a video guide for creating configurations.

---

Remember: Programming robots involves lots of trial and error. Don't get discouraged if something doesn't work the first time - debugging is part of the learning process!
