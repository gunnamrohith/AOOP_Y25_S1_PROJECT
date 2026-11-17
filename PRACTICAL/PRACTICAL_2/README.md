# Session 2 - The Five Invariant Doorways

These are the six complete executable programs from pages 17-26 of the
Session 2 PDF. Session 1 examples are in
[PRACTICAL_1](../PRACTICAL_1/README.md), not in this practical.

The classes labeled `Bad`, `Half`, `MutableEq`, `Leaky`, and `PremiumBooking`
deliberately demonstrate broken invariants. They are retained for comparison,
not presented as correct implementations. Each program also demonstrates its
corresponding fix; the final program combines all five protections.

| Program | PDF pages | Source |
| --- | --- | --- |
| Public setters | 17-18 | [Doorway1Demo.java](Door_Ways/01-public-setters/Doorway1Demo.java) |
| Escaping references | 18-20 | [Doorway2Demo.java](Door_Ways/02-escaping-references/Doorway2Demo.java) |
| Mutable collections | 20-21 | [Doorway3Demo.java](Door_Ways/03-mutable-collections/Doorway3Demo.java) |
| Equality and hash codes | 21-23 | [Doorway4Demo.java](Door_Ways/04-equality/Doorway4Demo.java) |
| Constructor leaks | 23-24 | [Doorway5Demo.java](Door_Ways/05-constructor-leaks/Doorway5Demo.java) |
| Protected booking | 24-26 | [ProtectedBookingDemo.java](Door_Ways/06-protected-booking/ProtectedBookingDemo.java) |

## Corrections and safeguards

- The earlier PDF fragments' stray `a`, `Parking Lot` class-name typo, and
  missing supporting methods are avoided by using its complete executable
  programs, rather than combining incomplete fragments.
- Mutable dates are copied before validation and when returned. Safe time
  constructors explicitly reject null arguments.
- Safe factory construction validates the ID and registry before publication.
- Safe wallet credits reject arithmetic overflow without changing history.
- The missing `hashCode` in `HalfSpot` is intentional; its compiler warning is
  suppressed only on that demonstration class. Its lookup result is not
  guaranteed: identity hash codes can collide, so the PDF correctly says
  "almost always false." All other output below is deterministic.
- `CANCELLED` is retained from the PDF's enum; no cancellation operation is
  added because the complete program defines only confirmation, activation,
  and completion.

## Compile and run

Use JDK 17 or newer. From this practical's folder:

```sh
cd Door_Ways/01-public-setters
javac Doorway1Demo.java
java Doorway1Demo
```

For the other programs, change to their respective folder and substitute the
source and main-class names from the table. Compile and run each folder
separately. Do not mix these default-package classes with Session 1's classes.

## Outputs

### 1. Public setters

```text
--- Broken: public setters ---
BadSpot[id=-5, available=true, vehicle=TS09AB1234]
--- Fixed: behaviour methods ---
SafeSpot[id=101, available=false, vehicle=TS09AB1234]
Rejected: Spot already occupied
SafeSpot[id=101, available=true, vehicle=null]
```

### 2. Escaping references

```text
--- Broken: escape on the way out ---
start=1000 end=0 valid=false
--- Broken: escape on the way in ---
end=0
--- Fix 1: defensive copies ---
end=5000
--- Fix 2: immutable LocalDateTime ---
end=2026-11-09T12:00 (no setter exists, nothing to attack)
```

### 3. Mutable collections

```text
--- Broken: exposed list ---
consistent=false
--- Fixed: List.copyOf ---
Blocked: list is read-only
consistent=true credits=[500]
--- Copy on input ---
lot size=2 (still 2)
```

### 4. Equality and hash codes

The second line is a representative result, not a guaranteed value.

```text
Default equality  : size=2 (same spot booked twice)
equals w/o hashCode: contains=false (almost always false)
Mutable equality  : contains=false (object lost)
Identity equality : size=1 contains=true
```

### 5. Constructor leaks

```text
--- Broken: leaking this ---
Registry sees: id=0, status=null
--- Fixed: static factory ---
Registry sees: id=502, status=CREATED
--- Broken: overridable method in constructor ---
NullPointerException: subclass field was not initialised yet
```

### 6. Protected booking

```text
Booking[501, COMPLETED, 2026-11-09T10:00 -> 2026-11-09T12:00]
notes=[Level 1, near lift]
Rejected: Only CONFIRMED can be activated
Rejected: notes are read-only
Rejected: End must follow start
```
