---
hide:
  - toc
---

*by Sorgelig*

You have assembled an arcade cabinet and looking for connecting your joysticks and buttons? You don't need to buy any of those expensive adapters. All you need is USB keyboard which you can disassemble.

After disassembling the keyboard you need to find the row and column contacts on board for following keys:
```
		5,         1P coin
		1,         1P start (shift key)
		UP,        1P up
		DOWN,      1P down
		LEFT,      1P left
		RIGHT,     1P right
		LEFTCTRL,  1P button 1
		LEFTALT,   1P button 2
		SPACE,     1P button 3
		LEFTSHIFT, 1P button 4
		Z,         1P button 5
		X,         1P button 6
		C,         1P button 7
		V,         1P button 8

		6,         2P coin
		2,         2P start
		R,         2P up
		F,         2P down
		D,         2P left
		G,         2P right
		A,         2P button 1
		S,         2P button 2
		Q,         2P button 3
		W,         2P button 4
		I,         2P button 5
		K,         2P button 6
		J,         2P button 7
		L,         2P button 8

		9,         Test
		TAB,       Tab (shift + 1P right)
		ENTER,     Enter (shift + 1P left)
		P,         P (pause) (shift + 1P down)
		F1,        Service
		F2,        Test
		F3,        Tilt
```
You can use multi-meter to find the contacts.

Then connect your buttons/joystick to board according to table above. Your hardware part is done.  
Connect your modded arcade keyboard to USB and start Menu core, then go to `Define Joystick buttons`. Press any button, and you will see "Keyboard ID: XXXX:YYYY" where XXXX:YYYY is HW identifier of the keyboard. Press ESC to ext from this dialog.  
Now open MiSTer.ini and add following options there:
```
jamma_vid=XXXX
jamma_pid=YYYY
```
XXXX and YYYY are those IDs you saw for your modded keyboard. Save and restart Menu core.  
Go to `Define Joystick buttons` again and assign buttons using P1 buttons. Note it now writes "Joystick ID: XXXX:YYYY" (instead of Keyboard) which means it recognizes your modded keyboard as jamma 2-player input device. P2 buttons will be automatically assigned the same as for P1.

Now your Arcade input device is ready to use. Unlike normal gamepads/joysticks, this device will always assign P1 and P2 inputs statically regardless P1 or P2 button was pressed first.
