# Tasks
## Time based tasks
### Ticker
```
#include "mbed.h"

Ticker flipper;
DigitalOut led1(LED1);
DigitalOut led2(LED2);

void flip() {
    led2 = !led2;
}

int main() {
    led2 = 1;
    flipper.attach(&flip, 2.0); // Ticks every 2 seconds

    while(1) {
        led1 = !led1;
        wait(0.2);
    }
}
```

### Timer

## Synchronization between tasks
### Mutex
### Semaphore
### Signal

# Threads
## Priority
Priority can go from osPriorityIdle (-3) to osPriorityRealTime (+3)