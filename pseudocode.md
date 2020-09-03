START

//Begin Program
INIT()

Patron.provideMoney(25)
Intake.recievedMoney(25)
Controller.moneyDeposited(25)

if(Intake.changeRequested)
	Intake.changeDispense

if(Controller.hasCorrectAmount)
	Timer.setTime
	Claw.start
	while(Timer.notOut || Controller.buttonControl(patronInputButton))
		Timer.changeDisplay
		Controller.joystickControl(patronInputJoystick)
	Claw.end

//end Program

//Define Objects, Functions

Patron

	INIT
		Set up Variables
			directionalArray array
			buttonPress	bool
			changeButtonPress bool

	takeChange
	provideMoney
	patronInputButton

	patronInputJoystick
		if(input left or right)
			directionalArray [1,0] if right or [-1,0] if left
		if(input up or down)
			directionalArray [0,1] if up or [0,-1] if down
		else
			directionalArray [0,0]
		return directionalArray



INIT function

	CREATE Controller
	CREATE Intake
	CREATE Timer
	CREATE Patron
	CREATE Display
	CREATE Claw

Controller

	INIT

		Set Up Variables
			moneyDeposited
			changeToReturn

		hasCorrectAmount
			if(moneyDeposited == 50)
				return TRUE
		addMoney

		joystickControl(patronInputJoystick)
			if(patronInputJoystick != [0,0])
				Claw.moveClaw(patronInputJoystick)

		buttonControl(patronInputButton)
			if(patronInputButton == TRUE)
				claw.dropClaw
				return TRUE

		changeDispense
			dispense changeToReturn = moneyDeposited

Intake

	INIT Set Up Variables
		recievedMoney

	changeRequested(changeButtonPress)
		change button pressed

	changeDispense()
		Controller.changeDispense

Timer

	INIT Set Up Variables
		time

	changeDisplay
		Display.changeTime(time)

	setTime
		time = 45

	notOut
		if(time == 0)
			return TRUE

Claw

	INIT

	start
		move claw to start position

	end
		move claw to end position
		open claw

	moveClaw
		move claw in array direction

	drop Claw
		drop claw
		after time close claw
		lift claw to top

Display

	changeDisplay(time)
		changes display to correct time
