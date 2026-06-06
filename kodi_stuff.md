# miscellaneous notes for configuring kodi

## jellyfin integration

### Install the jellyfin add-on repository for kodi.

1. Navigate to *Settings* -> *File Manager* -> *Add Source*.
2. Add **https://kodi.jellyfin.org**.  Name it something like *jellyfin_repo*.
3. Navigate to the add-ons *Install from Zip File* option.
4. If prompted, enable *Unknown Sources*.
5. Select the data source added above.
6. Install *repository.jellyfin.kodi.zip*.

### Install the Jellyfin add-on

1. Navigate to *Add-on Browser*.
2. Select *Install from Repository*.
3. Select the repo you added: *jellyfin_repo*.
4. Select *Video Add-ons*.
5. Select the *Jellyfin Add-on*.

### Reccomended: Install the *Kodi Sync Queue* plugin on the Jellyfin Server

1. Navigate to the web front-end, e.g. *https://zapp:8096"*.
2. Navigate *User* -> *Dashboard* -> *Plugins* -> *Available*.
3. Search for *kodi*.
4. Install *Kodi Sync Queue*.
5. Restart the server.

## youtube add-on for kodi

### Install the add-on

1. Navigate to *Settings* -> *Add-ons* -> *Install from Repository* -> *Kodi Add-on Repository* -> *Video Add-ons* -> *Youtube* -> *Install*.
2. **Failing that** - (inputstream.adaptive dependency failed to install) we need to manually install the dependency.
3. The dependency is supposed to be in the kodi repo, but I can't find it.  The add-on can be installed with apt though:
``` bash
$ sudo apt install kodi-inputstream-adaptive
```
5. Return to step 1. and try again.

### Configure the add-on

Need to add the api keys.  Two options:

#### Option one - webui
1. In the add-on configuration options, navigate to *API* and enable the option *Enable API Configuration Page*.
2. From a browser, navigate to the API config page.  E.g. **http://localhost:50152/youtube/api**
3. Enter the credentials.

#### Option two - command line
1. Directly edit te config file that stores the credentials.
``` shell
$ vim ~/.kodi/userdata/addon_data/plugin.video.youtube/api_keys.json
```
2. Add the credentials to the file.



