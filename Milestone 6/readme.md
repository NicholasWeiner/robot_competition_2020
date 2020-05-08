# Milestone 6
## Repeat Maze
- Added path shortener
- Added perfect maze replay

## Code
Only new code is included

``` 

void solved(){
  motors.setSpeeds(0,0);
  path_reduce();
  for(int i=0; i<turn_counter+1; i++){
    if(path[i] == 'L'){
      buzzer.playNote(NOTE_C(6), 100, 15);
      delay(200);
    }
    if(path[i] == 'R'){
      buzzer.playNote(NOTE_E(6), 100, 15);
      delay(200);
    }
    if(path[i] == 'S'){
      buzzer.playNote(NOTE_G(6), 100, 15);
      delay(200);
    }
    if(path[i] == 'U'){
      buzzer.playNote(NOTE_C(7), 100, 15);
      delay(200);
    }
  }
  
  button.waitForButton();

  buzzer.play("O6 d32a32");
  delay(1000);
  
  runSolvedMaze();
}

void runSolvedMaze(){
  int solved_path_location = 0;
  while(true){
    line_position = linesensors.readLine(sensor_vals);
  
    bool intersection_detected = sensor_vals[0] > THRESHOLD || sensor_vals[5] > THRESHOLD;
    
    if(intersection_detected) {
      if(solved_path_location == turn_counter){
        motors.setSpeeds(0,0);
        buzzer.play("!T250 O4 L8 g O5 ceg O6 ceg4.e4. O4 a- O5 ce-a- O6 ce-a-4.e-4. O4 b- O5 dfb- O6 df b-4r MS b-b-b- ML O7 c2.");
        break;
      }
      
      motors.setSpeeds(BASE_SPEED, BASE_SPEED);
      get_intersection_type(); // just to get through the intersection
    
      if(path[solved_path_location] == 'S'){
        follow_line();
      }
      if(path[solved_path_location] == 'L'){
        turn_left();
      } 
      if(path[solved_path_location] == 'R'){
        turn_right();
      } 
      
      solved_path_location++;
    } else {
      follow_line();
    }
  }
  button.waitForButton();

  buzzer.play("O6 d32a32");
  delay(1000);
  
  runSolvedMaze();

}

void path_reduce(){
  bool flag = false;  
  for(int path_location=2; path_location < turn_counter; path_location++){
    if(flag){
      path[path_location-2] = path[path_location];
    } else if(path[path_location-1] == 'U'){
      char a = path[path_location - 2];
      char b = path[path_location];
      char c = ' ';
      int total_angle = 180;
      if(a == 'L'){
        total_angle += 270;
      }
      if(a == 'U'){
        total_angle += 180;
      }
      if(a == 'R'){
        total_angle += 90;
      }
      if(b == 'L'){
        total_angle += 270;
      }
      if(b == 'U'){
        total_angle += 180;
      }
      if(b == 'R'){
        total_angle += 90;
      }
      total_angle = total_angle % 360;
      if(total_angle == 0){
        c = 'S';
      }
      if(total_angle == 90){
        c = 'R';
      }
      if(total_angle == 180){
        c = 'U';
      }
      if(total_angle == 270){
        c = 'L';
      }
      path[path_location - 2] = c;
      flag = true;
    }
  }
  if(flag){
    turn_counter = turn_counter - 2;
    path[turn_counter] = ' ';
    path[turn_counter + 1] = ' ';
    path_reduce();
  } else {
    return;
  }
}
```

## Video

[Milestone 6](https://drive.google.com/open?id=1BFFxxolGlV_48Z9oL9SnSUlgG9izps1n)