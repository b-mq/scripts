Applescripts
======================
Collection of Applescripts

## ToggleAudioOutputAirplay
Simple Applescript to toggle between "Internal Speakers" of your Mac and external Airplay device

Note: If your Airplay device name does not start with "Zeppelin", just change the string in line 7 to the name of your device

```applescript
tell application "System Preferences"
	reveal anchor "output" of pane id "com.apple.preference.sound"
	tell application "System Events"
		tell process "System Preferences"
			-- if "Internal Speakers"
			if selected of row 1 of table 1 of scroll area 1 of tab group 1 of window "Sound" then
				set newOut to "Zeppelin"
			else
				set newOut to "Internal"
			end if
			select (row 1 of table 1 of scroll area 1 of tab group 1 of window "Sound" whose value of text field 1 starts with newOut)
		end tell
	end tell
	tell application "System Preferences" to quit
end tell
```

## ToggleScreenSaverPW
Applescript to toggle checkbox in System Preferences -> Security & Privacy -> Require password...

NOTE: this script turns off the screen lock but *KEEPS KEYCHAIN ACTIVE*. If you don't want your Keychain activated you should delete lines 12+13 in order to get the script working
```applescript
			click checkbox 1 of tab group 1 of window 1
			click button 2 of sheet 1 of window 1
```
```applescript
tell application "System Preferences"
	activate
	reveal anchor "General" of pane "com.apple.preference.security"
end tell
tell application "System Events"
	tell process "System Preferences"
		if value of checkbox 1 of tab group 1 of window 1 is 0 then
			click checkbox 1 of tab group 1 of window 1
		else
			click checkbox 1 of tab group 1 of window 1
			click button 2 of sheet 1 of window 1
			delay 1
			click button 1 of sheet 1 of window 1
		end if
	end tell
	quit application "System Preferences"
end tell
```