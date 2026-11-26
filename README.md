# Smart-Bank-Locker-System
# Smart Bank Locker Access System with Password and RFID Authentication using LPC2129

## 1. Project Overview

The Smart Bank Locker Access System with Password and RFID Authentication is an embedded systems project developed using the ARM7 LPC2129 microcontroller.

The system provides two-level security authentication using an EM-18 RFID reader and a 4×4 keypad. The RFID reader reads the unique identification number (UID) of an RFID card and transfers the data to the LPC2129 microcontroller through UART0 communication.

The microcontroller compares the received RFID UID with the authorized UID stored in the program. If the RFID authentication is successful, the system requests the user to enter a four-digit password using the keypad.

The entered password is verified with the predefined password stored in the program. If both authentication stages are successful, the microcontroller activates a DC motor to open the locker.

A green LED indicates successful authentication. If the RFID card or password is incorrect, the system displays an error message and activates the red LED and buzzer.

The system allows three incorrect password attempts. After three unsuccessful attempts, locker access is denied.

A 16×2 LCD is used to display authentication messages, and UART0 is used for serial communication and monitoring through a PC.

## 2. Objectives

- To develop a secure bank locker access system using the LPC2129 ARM7 microcontroller.
- To implement two-level authentication using RFID and password verification.
- To interface the EM-18 RFID reader with the LPC2129.
- To receive RFID data using UART0 communication.
- To interface a 4×4 keypad for password entry.
- To verify the RFID UID and password using Embedded C programming.
- To control the locker mechanism using a DC motor.
- To indicate successful authentication using a green LED.
- To indicate unauthorized access using a red LED and buzzer.
- To implement a three-attempt password security mechanism.
- To display system status using a 16×2 LCD.
- To transmit authentication messages through UART communication.

## 3. Features

- Two-level security authentication.
- RFID-based user identification.
- EM-18 RFID reader interfacing.
- 12-character RFID UID verification.
- Four-digit password authentication.
- 4×4 matrix keypad interfacing.
- Automatic locker opening using a DC motor.
- Green LED indication for successful authentication.
- Red LED indication for incorrect password.
- Buzzer-based security alert.
- Three password attempts.
- LCD-based status display.
- UART0 serial communication.
- Modular Embedded C programming.

## 4. Hardware Requirements

| Component | Purpose |
|---|---|
| LPC2129 ARM7 Microcontroller | Main processing unit |
| EM-18 RFID Reader | Reads RFID card UID |
| RFID Card | User identification |
| 4×4 Matrix Keypad | Password entry |
| 16×2 LCD Display | Displays system messages |
| DC Motor | Locker opening mechanism |
| Motor Driver | Controls DC motor |
| Green LED | Successful authentication indication |
| Red LED | Incorrect password indication |
| Buzzer | Security alert |
| Power Supply | Provides operating voltage |
| Connecting Wires | Hardware connections |

## 5. Software Requirements

| Software / Technology | Purpose |
|---|---|
| Keil µVision | Embedded C coding and compilation |
| Flash Magic | Programming the LPC2129 |
| Embedded C | Microcontroller programming |
| UART Protocol | Serial communication |
| ARM7 Architecture | Microcontroller platform |

## 6. Pin Connections

The LPC2129 communicates with external devices using GPIO pins and UART0 communication.

### LCD Connections

| LCD Pin | LPC2129 Pin | Function |
|---|---|---|
| D4–D7 | P0.14–P0.17 | LCD data |
| RS | P0.12 | Register selection |
| E | P0.13 | Enable control |
| RW | GND | Write operation |

### Keypad Connections

| Keypad Pin | LPC2129 Pin | Function |
|---|---|---|
| C0 | P1.23 | Column 0 |
| C1 | P1.24 | Column 1 |
| C2 | P1.25 | Column 2 |
| C3 | P1.26 | Column 3 |
| R0 | P1.27 | Row 0 |
| R1 | P1.28 | Row 1 |
| R2 | P1.29 | Row 2 |
| R3 | P1.30 | Row 3 |

### Other Peripheral Connections

| Component | LPC2129 Pin | Function |
|---|---|---|
| EM-18 RFID TX | P0.1 (UART0 RXD) | RFID data reception |
| UART0 TXD | P0.0 | Serial data transmission |
| Green LED | P0.4 | Successful authentication |
| Red LED | P0.24 | Incorrect password indication |
| DC Motor Control | P0.18 | Motor control signal |
| Buzzer | P0.23 | Audio alert |

The DC motor must be interfaced through a suitable motor driver circuit.

## 7. Working Principle

The system works by performing two-level authentication using RFID card identification and password verification.

### Step 1: System Initialization

- Initially, the LPC2129 microcontroller is powered ON.
- UART0 is initialized for RFID communication.
- The LCD is initialized to display system messages.
- GPIO pins are configured for the keypad, LEDs, buzzer, and motor control.
- The system displays the project title on the LCD.
- The system waits for an RFID card.

### Step 2: RFID Card Detection

- The user scans an RFID card near the EM-18 RFID reader.
- The RFID reader reads the unique identification number of the card.
- The RFID data is transmitted to the LPC2129 through UART0.
- The microcontroller receives 12 characters of RFID data.
- The received UID is stored in an array for verification.

### Step 3: RFID Authentication

- The LPC2129 compares the received RFID UID with the authorized UID stored in the program.
- The authorized RFID UID used in this project is `0600680EE989`.
- If the received UID matches, the LCD displays the RFID verification message.
- The system proceeds to password authentication.
- If the UID does not match, the LCD displays NOT VERIFIED.
- The system denies access and waits for another RFID card.

### Step 4: Password Entry

- After successful RFID authentication, the LCD displays ENTER PASSWORD.
- The user enters a four-digit password using the 4×4 keypad.
- The keypad scanning function identifies the pressed row and column.
- A lookup table is used to identify the corresponding key value.
- The entered password is stored in a character array.
- The LCD displays asterisks instead of the actual password digits.

### Step 5: Password Verification

- The LPC2129 compares the entered password with the predefined password stored in the program.
- The password used in this project is `1234`.
- If the password matches, authentication is successful.
- If the password is incorrect, the attempt counter is incremented.
- The LCD displays WRONG PASSWORD.
- The red LED and buzzer are activated to indicate authentication failure.

### Step 6: Three-Attempt Security Mechanism

- The system allows a maximum of three incorrect password attempts.
- After the first incorrect attempt, another attempt is allowed.
- After the second incorrect attempt, the user gets the final attempt.
- After the third incorrect attempt, the LCD displays FAILED TO OPEN.
- The system denies locker access and returns to RFID scanning.

### Step 7: Locker Opening

When both RFID and password authentication are successful:

- The LCD displays LOCKER OPENED.
- The green LED indicates successful authentication.
- The buzzer remains OFF.
- The LPC2129 activates the DC motor control signal.
- The motor operates through the motor driver to open the locker.
- The motor control signal is switched OFF after the programmed delay.

## 8. RFID Module – EM-18

The EM-18 is an RFID reader module used for identifying RFID cards.

It operates at a frequency of 125 kHz and reads the unique identification number of compatible RFID cards.

In this project, the EM-18 RFID reader is used as the first level of authentication.

The RFID reader transmits the card UID as serial data to the LPC2129 microcontroller through UART0 communication.

The microcontroller receives 12 characters of RFID data and compares the received UID with the authorized UID stored in the program.

### RFID Authentication Details

| Parameter | Value |
|---|---|
| RFID Module | EM-18 |
| Operating Frequency | 125 kHz |
| Communication | UART |
| Data Length | 12 characters |
| Authorized UID | 0600680EE989 |
| Microcontroller Interface | UART0 |

### RFID Authentication Process

| Condition | System Response |
|---|---|
| Authorized RFID card | Requests password |
| Unauthorized RFID card | Displays NOT VERIFIED |
| No RFID card detected | Waits for scanning |

## 9. Communication Protocol

### UART (Universal Asynchronous Receiver Transmitter)

UART is a serial communication protocol used to transfer data between electronic devices.

In this project, UART0 is used for communication between the LPC2129 microcontroller and the EM-18 RFID reader.

### UART0 Communication

- The EM-18 RFID reader reads the RFID card UID.
- The RFID reader transmits the UID through its TX pin.
- The LPC2129 receives the serial data through UART0 RXD.
- The received RFID data is stored in an array.
- The microcontroller verifies the received UID.
- UART0 TXD is also used to transmit status messages to a connected PC.

### UART Configuration

| Register | Configuration | Purpose |
|---|---|---|
| PINSEL0 | 0x05 | Selects UART0 pins |
| U0LCR | 0x83 | Enables divisor latch access and configures 8-bit data |
| U0DLL | 97 | Baud-rate divisor |
| U0DLM | 0 | Upper divisor value |
| U0LCR | 0x03 | Configures 8-bit data, 1 stop bit, no parity |

The UART baud rate is approximately 9600 bps when the peripheral clock is 15 MHz.

### GPIO (General Purpose Input/Output)

GPIO pins are used to interface the LCD, keypad, LEDs, buzzer, and motor control signals.

- Keypad GPIO pins are used for row and column scanning.
- Green LED indicates successful authentication.
- Red LED indicates incorrect password.
- Buzzer generates an audio alert.
- DC motor control is provided through a GPIO output.

## 10. Expected Output

The system produces different outputs depending on the authentication conditions.

### Case 1: Authorized RFID Card

Input: Authorized RFID card.

Expected Result:

- RFID UID is received successfully.
- LCD displays RFID verification successful.
- System requests password entry.

### Case 2: Unauthorized RFID Card

Input: Unauthorized RFID card.

Expected Result:

- RFID UID does not match the authorized UID.
- LCD displays NOT VERIFIED.
- Locker access is denied.
- System waits for another RFID card.

### Case 3: Correct Password

Input: Correct password `1234`.

Expected Result:

- Password verification is successful.
- LCD displays LOCKER OPENED.
- Green LED turns ON.
- DC motor is activated.
- Locker opening mechanism operates.

### Case 4: Incorrect Password

Input: Incorrect password.

Expected Result:

- LCD displays WRONG PASSWORD.
- Red LED turns ON.
- Buzzer is activated.
- Password attempt counter is incremented.
- Locker remains locked.

### Case 5: Three Incorrect Password Attempts

Input: Three consecutive incorrect password attempts.

Expected Result:

- LCD displays FAILED TO OPEN.
- Red LED and buzzer indicate authentication failure.
- Locker access is denied.
- System returns to RFID scanning.

## 11. Applications

- Bank locker security systems.
- Digital locker systems.
- Home security systems.
- Office access control systems.
- College laboratory security.
- Electronic cabinet locking systems.
- Restricted area access control.
- Personal storage security systems.

## 12. Limitations and Future Enhancements

### Limitations

- The system depends on RFID card availability.
- Only the predefined authorized RFID UID is accepted.
- Password security depends on the predefined password.
- The system supports compatible 125 kHz RFID cards.
- The basic implementation does not provide remote monitoring.
- The system does not store user access history.
- The motor requires a suitable driver circuit.

### Future Enhancements

- Integrate GSM for SMS notifications.
- Add fingerprint authentication.
- Implement OTP-based authentication.
- Add IoT-based remote locker monitoring.
- Store access history in external memory.
- Add mobile application integration.
- Implement administrator-controlled password updates.
- Add multiple authorized RFID cards.
- Implement a timed security lockout after repeated failed attempts.

## 13. Advantages

- Provides two-level security authentication.
- Improves locker security using RFID and password verification.
- Prevents unauthorized access.
- Provides automatic locker operation.
- Implements a three-attempt password security mechanism.
- Provides visual and audio alerts.
- Displays system messages using an LCD.
- Supports serial communication through UART0.
- Uses an ARM7 microcontroller.
- Demonstrates practical Embedded C programming and peripheral interfacing.

## 14. How to Run the Project

1. Download or clone the project repository from GitHub.
2. Open the project using Keil µVision.
3. Add all required Embedded C source files and header files.
4. Select the LPC2129 microcontroller as the target device.
5. Configure the required GPIO pins and UART0 communication.
6. Build the project and verify that there are no compilation errors.
7. Generate the HEX file from the Keil project.
8. Connect the EM-18 RFID reader to the UART0 interface.
9. Connect the LCD, keypad, LEDs, buzzer, and motor driver according to the pin connections.
10. Ensure that all components receive their required operating voltages.
11. Program the LPC2129 using Flash Magic.
12. Power ON the system.
13. Scan the authorized RFID card.
14. Enter the correct four-digit password using the keypad.
15. Observe the LCD message and green LED indication.
16. Verify that the DC motor activates the locker mechanism.
17. Scan an unauthorized RFID card and verify that access is denied.
18. Enter an incorrect password three times and verify the security alert.

## 15. Conclusion

The Smart Bank Locker Access System with Password and RFID Authentication using LPC2129 provides a two-level security mechanism for locker access.

The system uses an EM-18 RFID reader for card identification and a keypad for password verification. The LPC2129 ARM7 microcontroller processes both authentication stages and controls the locker mechanism using a DC motor.

The system also provides security alerts through LEDs and a buzzer. The three-attempt password mechanism helps prevent unauthorized locker access.

This project demonstrates the practical implementation of Embedded C programming, ARM7 microcontroller interfacing, UART communication, GPIO control, RFID technology, keypad scanning, and LCD interfacing.
