	██╗███╗   ██╗    ██████╗  █████╗  ██████╗███████╗
	██║████╗  ██║    ██╔══██╗██╔══██╗██╔════╝██╔════╝
	██║██╔██╗ ██║    ██████╔╝███████║██║     █████╗  
	██║██║╚██╗██║    ██╔═══╝ ██╔══██║██║     ██╔══╝  
	██║██║ ╚████║    ██║     ██║  ██║╚██████╗███████╗
	╚═╝╚═╝  ╚═══╝    ╚═╝     ╚═╝  ╚═╝ ╚═════╝╚══════╝
                                                 
	  Hans Heidmann	 Calvin Hicks

	Sean Tranchetti  Madison Rockwell
 

	Description:

	An Arduino wristband that provides information on how the user is pacing
 	themselves during a run, walk or cycling route. It tracks GPS locations
 	and current times to compare the users current performance with previous attempts
	at the route. Other features could include more familiar statistics such as
	total time, heart rate, and calories burned as well as an accompanying app to
 	display this information in a beautiful and clear manner. This is a large 
	project that could be beyond the scope of time set for this class. We will set
	smaller goals that can be met by class end and expand on that if we are ahead
	of schedule. 


	REPO ORGANIZATION:
	./3d Models -> Models for a failed 3D print of a case for our wristband
	./Arduino Code -> All code for the Arduino in our wristband
	./AssingmentPDFs -> All PDFs of the various assignment parts for the class
	./Circuit_Schematics -> Generated images of our wristband circuit layout
	./core-plot -> A graphing library we need for our app
	./doc -> The doxygen-generated documentation for our code
	./Fritzing -> Fritzing files for circuit design
	./Icons and Launch Image -> Icon for our app on the home screen
	./InPace -> Our source code
	./Photo_Documentation -> Various pictures of our project
	./Photoshop App Icon Files -> Photoshop file for our Icons
	./test -> Test framework and test files

	How to Build and Run InPace:

	Step 1 - Clone our Respository

	// git clone https://github.com/H-4-N-5/CS-3308-Project.git

	Step 2 - Open Xcode 

	// Click File -> Open: CS-3308-Project/InPace/InPace.xcodeproj

	Step 3 - Build and Run

	// In Xcode, press COMMAND+R or click Project -> Build and Run




	Running InPace Tests (note that these require clang and GNUSTEP)

	Step 1 - Build the test executable

	// make test

	Step 2 - run the executable

	// ./test/db_test


       ___________________________
	///   						  ///
    ///   BUILDING THE WRISTBAND  ///
    ///___________________________///

    ***  Electronics Parts List  ***
    ---------------------------------
                
    // Arduino Pro Mini (5V/16mHz Version)
    
    // Sparkfun "FTDI Basic" (USB Mini to FTDI programmer, 5V version) 
    
    // Common Anode RGB LED (4 pins, See my pin description below)
    
    // 2 brown-black-red resistors (1KΩ 5% tolerance)
    
    // 3 red-black-brown resistors (200Ω 5% tolerance)
    
    // 2 Momentary Tactile Push Buttons (2 pin)
    
    // 3-pin On/Off Switch
    
    // Adafruit Ultimate GPS Breakout Board
    
    // Adafruit microSD Card Breakout (Input Voltage: 3-5 Volts)
    
    // 3.7 Volt Single Cell 110 mAh LiPo Battery
    
    // Adafruit "MicroLipo" Lipo Charger (3.7 Volt Output)
    
    // Power Booster "DROK® Slim Boost Converter Module"  (DC 2.5-6V to 4-12V Voltage Regulator)

    // Red Bear Labs "BLE Mini v1.1" Bluetooth Module 
    
    
            
    
    ---------------------------------------
     
    Adafruit microSD Card Read/Write Pins
 
    CS -> pin D-10
    MOSI -> pin D-11
    MISO -> pin D-12
    CLK -> pin D-13

    -----------------------------
    
    Adafruit Ultimate GPS_Module Module Pins
    
    RX --> pin D-2
    TX --> pin D-3
    
    -----------------------------
    
    Red Bear Labs BLE 4.0 Bluetooth Module Pins
    
    RX --> TX
    TX --> RX
    
    -----------------------------
    
    Bluetooth push button --> pin 8
    GPS push button --> pin 9
    
    -----------------------------
    
    Four-Pin Addressable G-R-B LED
    
         __   
        /  \
        |___|  <-- flat side
        /| |\
       | | | |
       | | | |
       | | | |
       | | | 4
       1 | 3 
         |  
         2             
  
    (1) RED ground
    (2) 4.5-6V VIN  -->  VCC
    (3) ground  -->  GND
    (4) locic output  -->  (Nothing, but could be used to chain more G-R-B LEDs together.)
    
    
    -----------------------------
    
  
    ////// systemState ////
    
    systemState = 1: Waiting for user interaction
                     - RGB LED should be RED
                     - attemping to get a GPS_Module Satellite fix
    
    
    systemState = 2: Logging GPS_Module data
                     - LED should be GREEN
                     - open dataFile (GPS_Moduledata.txt) for writing to
                     - read in GPS_Module data from software serial pins 2 and 3
                     - write GPS_Module data to the microSD
             
    
    systemState = 3: Sending Data Over Bluetooth
                     - LED should be BLUE
                     - open dataFile (GPS_Moduledata.txt) for reading from
                     - iterate through all the lines of the text file
                     - send each line of the text file through bluetooth as a string
                     - *GPS_Moduledata.txt will be "rebuilt" string by string on the iOS receiving end


