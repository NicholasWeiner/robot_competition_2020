# Milestone 1
## Get the robot to move
- Assembled robot.
- Created Github repo.
- Installed ZumoSheild library.
- Added instructions to make wheels move, completing Milestone 1.

## Code

``` 
#include <ZumoSheild.h>

ZumoMotors motors;

void setup() {
  // put your setup code here, to run once:

}

void loop() {
  // put your main code here, to run repeatedly:
  motors.setSpeeds(100, 100);
}```
## Video