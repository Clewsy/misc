# flexo setup

## Pre-Wipe

### Configs to back-up
Ensure destination of all files is the __Download__ dir for scripted backup to file\_cache.
|App				|Backup Instructions														|Saved Filename					|
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------|
|andOTP				|Menu -> Backup -> Backup (encrypted) -> __Download__ -> Save -> __Password__ -> Save						|otp\_accounts.json.aes (#)			|


|AntennaPod (Subscriptions)	|Menu -> Settings -> Storage -> Import/Export -> OPML export -> *Download* -> Save -> OK					|antennapod-feeds.opml (#)			|
|AntennaPod (Database)		|Menu -> Settings -> Storage -> Import/Export -> Database import/export -> EXPORT -> *Download* -> Save -> OK			|AntennaPodBackup.db (#)			|
|OsmAnd+			|Menu -> My Places -> Favourites Menu -> Share -> Nextcloud Dev -> Upload -> (Ugh DL from nextcloud and move to *Download*)	|favourites.gpx					|
|NewPipe (Subscriptions)	|Subscriptions screen -> Subscriptions menu -> Export to File -> *Download* -> *Save Symbol*					|newpipe\_subscriptions\_############.json	|
|NewPipe (Database)		|Menu -> Content -> Export Database -> *Download* -> OK										|NewPipeData-########\_######.zip		|

### Backup
Run backup script to copy useful files to file\_cache.

##  Post Install

### apks
|App		|URL						|
|---------------|-----------------------------------------------|
|F-Droid	|https://f-droid.org/				|
|Signal		|https://signal.org/android/apk/		|
|ProtonMail	|https://protonapps.com/protonmail-android	|

### Repos to add to F-Droid
|Repo		|URL						|
|---------------|-----------------------------------------------|
|Bitwarden	|https://mobileapp.bitwarden.com/fdroid/	|

### F-Droid Apps
- andOTP
- AntennaPod
- AnySoftKeyboard
- Aurora
- Binary Eye
- Bitwarden
- DAVx5
- DuckDuckGo Privacy Browser
- Easy XKCD
- Fennec F-Droid
- Forecastie
- Frost for Facebook
- Hacker's Keyboard
- InstaGrabber
- Kore
- M.A.L.P.
- Maps & GPS Navigation OsmAnd+
- NewPipe
- Nextcloud Dev
- Nextcloud Notes
- PhoneTrack
- Simple Calculator
- Simple Calendar Pro
- Simple Clock
- Simple File Manager
- Simple Thank You
- SolitaireCG
- Tasks.org
- Termux
- Termux:API
- Termux:Styling
- Termux:Widget
- Ultrasonic
- VLC
- Wireguard
