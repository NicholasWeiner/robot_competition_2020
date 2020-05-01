# Milestone 3
## Add solved method
- Plays tune when solved.
- Reduces speed to 0.

## Record movements
- Write to an array.
- Made solved tune reflect path takes.

## Code
Only new code is included

``` 
void loop() {
  line_position = linesensors.readLine(sensor_vals);



  if(sensor_vals[0] > THRESHOLD && sensor_vals[1] > THRESHOLD){
    turn_left();
  } else if(sensor_vals[4] > THRESHOLD && sensor_vals[5] > THRESHOLD){
    turn_right();
  } else {
    follow_line();
  }
}

void follow_line() {
  int error = line_position - 2500;
  int error_change = error - last_error;
  int left_speed = BASE_SPEED + PROPORTION_GAIN * error + DERIVATIVE_GAIN * error_change;
  int right_speed = BASE_SPEED + -PROPORTION_GAIN * error + -DERIVATIVE_GAIN * error_change;
  last_error = error;
  motors.setSpeeds(left_speed, right_speed);
}

void ballistic_turn_left() {
  motors.setSpeeds(-400, 400);
  delay(60);
}

void turn_left() {
  motors.setSpeeds(-BASE_SPEED, BASE_SPEED);
  linesensors.read(sensor_vals);
  while(sensor_vals[0] > THRESHOLD && sensor_vals[1] > THRESHOLD){
      linesensors.read(sensor_vals);
  }  
  ballistic_turn_left();
}

void ballistic_turn_right() {
  motors.setSpeeds(400, -400);
  delay(60);
}

void turn_right() {
  motors.setSpeeds(BASE_SPEED, -BASE_SPEED);
  linesensors.read(sensor_vals);
  while(sensor_vals[0] > THRESHOLD && sensor_vals[1] > THRESHOLD){
      linesensors.read(sensor_vals);
  }  
  ballistic_turn_right();
}
## Video

[Milestone 3](https://drive.google.com/open?id=1AcbJRCrNyG7JsWCEA9yCQoSuzKlnQjIr)