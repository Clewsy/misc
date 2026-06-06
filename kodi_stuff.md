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

