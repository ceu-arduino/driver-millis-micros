# Time Utilities

Basic access to time.

## API

### Includes

```
#include "time.ceu"
```

### Output

#### TIME_GET_MILLIS

Gets the number of elapsed milliseconds since the board reset.

```
output &u32 TIME_GET_MILLIS;
```

1. `&u32`: reference to write the value

#### TIME_GET_MICROS

Gets the number of elapsed microseconds since the board reset.

```
output &u32 TIME_GET_MICROS;
```

Parameters:

1. `&u32`: reference to write the value

### TIME_DELAY_MILLIS

Freezes the whole program for a given number of milliseconds.

```
output u32 TIME_DELAY_MILLIS;
```

Parameters:

1. `u32`: number of milliseconds

### TIME_DELAY_MICROS

Freezes the whole program for a given number of microseconds.

```
output u32 TIME_DELAY_MICROS;
```

Parameters:

1. `u32`: number of microseconds

### Code Abstractions

#### Time

Initializes the Time subsystem.

```
code/await Time (none) -> NEVER;
```

Parameters:

- `none`

Return:

- `NEVER`: never returns

## Examples

### Print Current Time

Print current time on every occurrence of `INT0`:

```
#include "int0.ceu"
#include "time.ceu"

spawn Time();

var u32 ms = _;
var u32 us = _;

{ Serial.begin(9600); }

loop do
    emit TIME_GET_MILLIS(&ms);
    emit TIME_GET_MICROS(&us);
    await INT0;
    {
        Serial.print("MS ");
        Serial.println(@ms);
        Serial.print("US ");
        Serial.println(@us);
        _DELAY(50);
    }
end
```
