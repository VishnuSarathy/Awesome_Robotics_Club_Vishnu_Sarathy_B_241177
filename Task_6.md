<h1> Part A </h1>
PART-A: Initially, we will need to figure out a reliable and efficient way to detect which chess piece moves from which square to which. We’re specifically looking for solutions that don’t involve computer vision, RFID, or magnetic sensors. Present your solution in the form of a detailed explanation of the mechanism with diagrams.

Solution 1:
  Rough idea : we are gonna use a touch sensor like structure for sensing piece like there will be 2 open ends of in each square and a metal plate in bottom of piece when it is placed on a square the circuit closes and current passes so we can detect the piece.
  Now, let us take each row as a seperate circuit, now there will be 8 squares in each row, leaving 8 pair of open ends(1 for 1 square). below the open ends we will attach resistors of different resistance(ohms) below each square.
  let us take the volatage ant starting point is Y Volt(y<5). now if no piece is in the row then the end volt will be X Volt. if any one of the piece is placed on the board then the resistor below the square gets shorted so the end volt will get increased. like this we will get different voltage for different No. of pieces placed in the row.
  now to identify how many pieces are placed in the row and on which position, we will take the help of sidon sets -- sum distinct sets. eg:- (1,2,4,8,16,32,64,128). we will calculate the resistance of each square such that the voltage accross the square is one of the unique element of the above set(1st sq gets 1/k and second sq gets 2/k,etc. k  to scale down the voltage). the property of sidon set is the sum of elements in any subset if sidon set is unique. that is the sum can't be reproduced by any other combination of numbers from the set. so if the X - Y = 7, then exactly square 1,2,3 are occupied.
  with the initial arrangement of chess board known, we can trace and remember the movemnts of pieces to keep track of the borad. I hope this solves the entire project, if some points are not cleare pleace contact me so that i can explaioin - 9500728429
  Flaws:-
  there are only 6 analog input in aurdino but there are 8 rows so to detect voltages we will be needing 8 analog pins, so we should be using esp32 or aurdino mega.
  "int rawValue = analogRead(sensorPin); 
  float voltage = rawValue * vRef / 1023 * scaleFactor;"
  

<h1> Part B </h1>
PART-B: Now, let’s assume you’ve chosen a mechanism to detect the movement of the pieces. To simplify the problem, suppose this mechanism works such that each square outputs a signal of 1 when a piece is lifted from it—let’s define this event as an “activation.”
Given that there are 64 squares on a chessboard, but our poor Arduino has only about 20 I/O pins, how would you detect exactly which square has been activated using the minimum number of pins? Present your answer in the form of a detailed explanation of the solution with diagrams wherever necessary.

Solution 1:
  Forgetting the solution i gave for 1st part, as per question let us assume we have 64 digital pins, each one of them signals one if it is activated and 0 otherwise. first we will start addressing them. like a1 = 0, a2 =1, ... , h8 = 63.
  Now to represent a number < 64 we need only 6 bits i.e. 2^6 = 64. 6 bits == 6 digital pins.
  by using combination of gates we can do this as i have attached picture for 4 to 2 converter, the combination is already made as encoders we and use 64 to 6 encoder or make that with help of 8 to 3 encoders.
  the issue is encoders give 000000 for both 0 and 1 in 0th pin. i.e.. we cant find of the 0th pin is activated or not. to avoid this we will be using an extra pin V. V turns up if atleast 1 of the pin is activated and turns down if none of them are activated.
  So totally we need 7 pins.
  Flaws:-
  This cant handle multiple activations at same time.
Solution 2:
  We can use MCP23017 port extenders. this uses I2C protocal and ectends upto 16 pins form just two pins this makes the required pins to 8, but aurdino has now 2 pair for i2c pins but we need 4 so i think this is not possible. also i dont have exact idea how this works i am looking into that.
