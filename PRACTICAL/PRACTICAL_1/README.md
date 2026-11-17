# Session 1 Java Examples

The Java examples from the supplied AOOP sheet are included, with the
negative-ID example corrected to enforce a positive ID.
Each example is separate because the sheet reuses the same class names.

This folder contains Session 1 only. Session 2's five invariant doorways and
protected-booking demonstrations are in [PRACTICAL_2](../PRACTICAL_2/README.md).
The existing case-study documents in this folder are unchanged.

| Folder | Sheet pages | Example |
| --- | --- | --- |
| [01-basic-parking](Object_Invariants/01-basic-parking/Main.java) | 6 | Basic parking spot and `Main` |
| [02-encapsulation](Object_Invariants/02-encapsulation/Main.java) | 7-8 | Private fields, constructor validation, vehicle assignment |
| [03-unvalidated-id](Object_Invariants/03-unvalidated-id/ParkingSpot.java) | 10 | Corrected: accepts a positive ID and demonstrates rejection of a negative ID |
| [04-single-field-invariant](Object_Invariants/04-single-field-invariant/ParkingSpot.java) | 10-11 | Validates a positive parking spot ID |
| [05-multi-field-invariant](Object_Invariants/05-multi-field-invariant/ParkingSpot.java) | 12-13 | Protects availability and vehicle number together |
| [06-temporal-invariant](Object_Invariants/06-temporal-invariant/Booking.java) | 15-17 | Booking moves from CREATED to CONFIRMED to ACTIVE to COMPLETED |

Page numbers refer to the PDF's page order.

The sheet's `ParkingSpot1` declaration on page 7 is corrected to `ParkingSpot`
to match its constructor and the supplied `Main`. Example 03 now validates its
ID in the constructor and keeps it private and final so it cannot be changed
to an invalid value afterward. Its original folder name is retained.
The single-field example prints `Spot ID: 101`, as its code specifies, although
the sheet's output omits that label.

The six studio projects were only named in the sheet, so their implementations,
custom tests, helpers, and scripts have been removed. The page 9 exercise is not
implemented because it supplies requirements rather than example code.

## Run an example

Use JDK 11 or newer (`String.isBlank()` requires Java 11). Compile and run one
folder at a time; do not compile all examples into the same output directory.

```sh
cd Object_Invariants/01-basic-parking
javac Main.java
java Main
```

For examples 03-05, compile `ParkingSpot.java` and run `java ParkingSpot`.
For example 06, compile `Booking.java` and run `java Booking`.

Compiling every source file together produces duplicate-class errors because
these independent examples reuse `Main` and `ParkingSpot`.

## Expected outputs

### 01 - Basic parking

```text
Spot ID: 101
Location: Hyderabad
Available: true
```

### 02 - Encapsulation

```text
Spot ID: 101
Vehicle: TS08AB1234
Occupied: true
```

### 03 - Corrected ID validation

```text
Spot ID: 101
Rejected: Spot ID must be positive
```

### 04 - Single-field invariant

```text
Spot ID: 101
```

### 05 - Multi-field invariant

```text
Spot ID: 101
Location: Hyderabad
Available: false
Vehicle: TS09AB1234
```

### 06 - Temporal invariant

```text
Booking ID: 501
Status: COMPLETED
```
