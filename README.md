Description
===

This is the code I have for my university final year project.

Bascially, we are attempting make a GPS enabled walking stick (with a giant handle) to aid blind/partially blind people by using vibrations to guide them in the right direction. 

Pictures are available on: ****https://github.com/Paperwerk/GPS/blob/master/GPS.pdf****

I am responsible for the GPS part. 


How does the code work?
===

When it boots up, it does the initializtions in ****setup()**** first. 

Then afterwards, the function ****loop()**** repeats the following 4 procedures every second. (delay(1000)))

1. ****compassreading()****; getting the compass readings from the onboard HMC6352 GPS module. 

2.  ****angle()****; using the compass readings to calculate the angle between the user and the destination. 

  Note that the following 
  
  heading = atan2(sin(x2lon-flon1)*cos(x2lat),cos(flat1)*sin(x2lat)-   sin(flat1)*cos(x2lat)*cos(x2lon-flon1))/2*3.1415926535; 

  is an implementation of ****https://en.wikipedia.org/wiki/Haversine_formula****

3.   Since this walking stick is operating on a checkpoint system (not included in my code as that is the work of someone else), the function ****check_for_next_waypoint()****, checks whether the user is close enough (<5m) and will switch to the next checkpoint after it has reached that close. 

4.  ****left_or_right()**** is translating the results from ****angle()**** to one of the following 5 scenarios, which can be refined as needed. 

	a)Go straight ahead, no vibrations. 

	b) Strongly need to turn right, right motor vibrations to maximum strength 

	c) Lightly need to turn right, mild right motor vibrations 

	d) Strongly need to turn right, right motor vibrations to maximum strength

	e) Lightly need to turn right, mild right motor vibrations  

Questions:
===

Q: Does this compile?

A: This requires a specific Arduino flavo(u)r-ed C compiler. I have tried to compile it under GCC and it doesn't work.

Q: Hardware used?

Standard issue Arduino UNO. GPS module is HMC6352.

Q: Does this always work?

A: There are 2 situations that I have tested does not work:

  1.   Underground. 
  2.   In elevators. The metallic frame of the elevator makes it a Faraday cage which blocks all sorts of EM waves.

  The GPS readme also states these situations will disable the GPS (because of the potential that someone could use this $20 USD GPS part to make a home made cruise missle). 
  3.  Above 60000 feet
  4.  When the GPS module is moving faster than 1000 meters per sec.

  Apparently just from the above code, I know enough of about GPS (really?) that my professor/supervisor got someone from the University to give me a stern talk about the implications of making a nuke from this.  

  Looking behind, I should feel honoured. Half of my class can't even design an Amplifier, let alone make a WMD.


Q: Where are the rest of the code, for example, the haptic feedback/vibration parts or the use of ArrayCounter?

A: I have no secured my teammates' approvals to post their codes. Hence I can only demonstrate the code I have written myself. 


