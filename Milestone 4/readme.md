# Milestone 4
## Add solved method
- Plays tune when solved.
- Reduces speed to 0.

## Record movements
- Write to an array.
- Made solved tune reflect path takes.

## Code
Only new code is included

``` 
char path[50];
int turn_counter = 0;
void loop() {
  line_position = linesensors.readLine(sensor_vals);
  if (sensor_vals[0] > THRESHOLD && sensor_vals[5] > THRESHOLD) {
    solved();
  } else if (sensor_vals[0] > THRESHOLD && sensor_vals[1] > THRESHOLD) {
    path[turn_counter] = 'L';
    turn_counter++;
    turn_left();
  } else if (sensor_vals[4] > THRESHOLD && sensor_vals[5] > THRESHOLD) {
    path[turn_counter] = 'R';
    turn_counter++;
    turn_right();
  } else {
    follow_line();
  }
}

void solved() {
  motors.setSpeeds(0, 0);
  for (int i = 0; i < turn_counter + 1; i++) {
    if (path[i] == 'L') {
      buzzer.playNote(NOTE_G(5), 200, 15);
      delay(400);
    }
    if (path[i] == 'R') {
      buzzer.playNote(NOTE_G(6), 200, 15);
      delay(400);
    }
  }
  while (true) {
    // do nothing so that the main loop() doesn't restart.
  }
}
## Video

[Milestone 4](https://drive.google.com/open?id=1Am49HYI3LnfNHxgviCl8bopG7eUUS0zg)