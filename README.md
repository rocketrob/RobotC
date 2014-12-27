#include "JoystickDriver.c"

int precision;

void drive()
{
	getJoystickSettings(joystick);
	// left Drive
	if(joystick.joy1_y1 < 3 && joystick.joy1_y1 > -3)//dead zone
	{
		motor[left] = 0;
	}
	else
	{
		motor[left] = joystick.joy1_y1/precision;  //joystick value divided by 2
	}
	// Right drive
	if(joystick.joy1_y2 < 3 && joystick.joy1_y2 > -3)//dead zone
	{
		motor[right] = 0;
	}
	else
	{
		motor[right] = joystick.joy1_y2/precision;  //joystick value divided by 2
	}
}



task main()

{

	while(1 == 1)
	{
		//Drive motor controls
		getJoystickSettings(joystick);
		if(joy1Btn(0) == 0)
		{
			precision = 2; // standard precision
			drive();
		}

		else if (joy1Btn(0) == 1)
		{
			precision = 6; // sensitive or 'slow' precision
			drive();
		}

	}

}
