# flexo setup

## Pre-Wipe

### Configs to back-up
Ensure destination of all files is the __Download__ dir for scripted backup to file\_cache.

|App                        |Backup Instructions                                                                                                        |Saved Filename                             |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------|-------------------------------------------|
|andOTP                     |Menu -> Backup -> Create Backup (encrypted) -> Save -> Password -> Save                                                    |otp\_accounts.json.aes (#)                 |
|AntennaPod (Subscriptions) |Menu -> Settings -> Storage -> Import/Export -> OPML export -> Save -> OK                                                  |antennapod-feeds.opml (#)                  |
|AntennaPod (Database)      |Menu -> Settings -> Storage -> Import/Export -> Database export -> Save -> OK                                              |AntennaPodBackup.db (#)                    |
|OsmAnd+                    |Menu -> My Places -> Favourites Menu -> Share -> Nextcloud Dev -> Upload -> (Ugh DL from nextcloud and move to Download)   |favourites.gpx                             |
|NewPipe (Subscriptions)    |Subscriptions screen -> Subscriptions menu -> Export to File -> Download -> Save Symbol                                    |newpipe\_subscriptions\_############.json  |
|NewPipe (Database)         |Menu -> Settings -> Content -> Export Database -> Download -> OK                                                           |NewPipeData-########\_######.zip           |
|Wireguard                  |Menu -> Export tunnels to zip file                                                                                         |wireguard-export.zip                       |

### Backup
Run backup script to copy useful files to file\_cache.

##  Post Install

### apks
|App        |URL                                        |
|-----------|-------------------------------------------|
|Magisk     |https://github.com/topjohnwu/Magisk/       |
|F-Droid    |https://f-droid.org/                       |
|Signal     |https://signal.org/android/apk/            |
|ProtonMail |https://protonapps.com/protonmail-android  |

### Repos to add to F-Droid
|Repo       |URL                                        |
|-----------|-------------------------------------------|
|Bitwarden  |https://mobileapp.bitwarden.com/fdroid/    |

### F-Droid Apps
- AdAway
- andOTP
- AntennaPod
- Arcticons
- Aurora
- Barinsta
- Bitwarden
- DAVx5
- Dawn
- DuckDuckGo Privacy Browser
- Easy XKCD
- Fennec
- Firefox Klar
- Forecastie
- Fritter
- Frost for Facebook
- Hacker's Keyboard
- Home Assisstant
- Kore
- M.A.L.P.
- Material Files
- Materialistic
- motionEye
- NewPipe
- Nextcloud Dev
- Nextcloud Notes
- OpenDocument Reader
- OsmAnd~
- Pdf Viewer Plus
- PhoneTrack
- SolitaireCG
- Subtracks
- Tasks.org
- Termux
- Termux:API
- Termux:Styling
- Termux:Widget
- VLC
- Wireguard
