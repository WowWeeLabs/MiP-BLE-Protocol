RoboMe iOS SDK
===============

The RoboMe iOS SDK lets you send and receive commands to and from your [RoboMe robot](http://www.wowwee.com) in apps you build for iPad, iPhone, and iPod touch devices.

Documentation of the SDK is available here: http://www.wowweelabs.com/robome/ios/docs/index.html

Support is available at the RoboCommunity forums: http://www.robocommunity.com.

For Android or Unity SDKs visit: http://www.wowweelabs.com/. 

For information on WowWee products visit: http://www.wowwee.com/.

Getting Started
---------------------------------------

Download the [RoboMe iOS SDK](https://github.com/WowWeeLabs/RoboMe-iOS-SDK).

The quickest way to get started is to open the sample app under the SampleProject directory. The RoboMe sample app starts listening to events from RoboMe and prints these to the text view. It also displays buttons to send a few movement commands to RoboMe. For a full list of commands see RoboMeCommands.h.

Creating your own app using the RoboMe iOS SDK
-----------------------------------------------

Here are the basic steps in creating your own app:

1. In XCode, create a new project. The simplest application is a Single-View application.

2. Open the project navigator in Xcode.

3. Drag the RoboMe-iOS-SDK directory from the Mac OS Finder to the Frameworks directory for your project in XCode. This directory contains the framework and bundle file required.

4. The RoboMe framework requires a few other frameworks and libraries to be added to your project. The easiest way to add them is
to copy them from the RoboMe Sample app under the SampleProject directory.

	Open the RoboMe sample app in XCode. Drag all of the additional frameworks from the frameworks folder (in the project navigator)
	of the RoboMe sample project into the frameworks folder of your project.
	
	The additional frameworks and libraries include the following: AudioToolbox.framework, AVFoundation.framework, AudioToolbox.framework, MediaPlayer.framework, Security.framework.

Next steps:

1. In the ViewController.h file, add the following line (after `import <UIKit/UIKit.h>`):

		#import <RoboMe/RoboMe.h>

2. Edit the `@interface` declaration in the ViewController.h file to the following:

		@interface ViewController : UIViewController <RoboMeDelegate>

3. Add a property for the RoboMe object.

		@property (nonatomic, strong) RoboMe *roboMe;

4. Rename ViewController.m to ViewController.mm (required because the RoboMe SDK uses some c++ libraries)

5. In the ViewController.mm viewDidLoad method, add the following code to initialize and start the connection to RoboMe.

		self.roboMe = [[RoboMe alloc] initWithDelegate: self];
		[self.roboMe startListening];
		

6. Implement the required method for RoboMeDelegate commandReceived.

		- (void)commandReceived:(IncomingRobotCommand)command {
			// handle incoming command
		}

License
-----------------------------------------------

RoboMe iOS SDK is available under the Apache License, Version 2.0 license. See the LICENSE.txt file for more info.