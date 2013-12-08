# Chrome Bookmarks Online


This project allows you to have an online copy of your Google Chrome bookmarks.
You just need a regular Dropbox account for accessing bookmarks page through
a [Dropbox](https://www.dropbox.com/) public folder.
Since Dropbox disabled the public folder you can use
[Dockbox](http://www.dockbox.io) for a public interface.
This is a fork of the original project
[gornostal/Chrome-Bookmarks-Online](https://github.com/gornostal/Chrome-Bookmarks-Online)
it adds encryption support and instructions for dockbox usage.

##Installation
* Clone the project into a new or empty dropbox folder.

```sh
git clone https://github.com/jandob/Chrome-Bookmarks-Online.git $HOME/Dropbox/USER.dockbox
```

###Dockbox
* Invite `web@dockbox.io` to share the folder with you (via Dropbox web interface).
* Wait until a folder called `dockbox` appears in the shared folder.
* Open the file `$HOME/Dropbox/USER.dockbox/dockbox/hostnames.txt`.  Here all
your dockbox.io subdomains are managed. Add a new line:
`USER.dockbox.io`
* Verify its working by pointing your browser to `http://USER.dockbox.io`

### Syncing & Encryption

* This fork suppports encryption of the bookmark file, encrypt it with openssl.
  The PASSWORD is the one you will use in the webinterface to access your
  bookmarks.

```sh
openssl enc -aes-256-cbc -in Bookmarks -out Bookmarks.enc -pass pass:"PASSWORD" -e -base64
```
* Under linux you can use this crontab entry to automate the syncing (every full hour).

```sh
BKM="$HOME/.config/chromium/Default/Bookmarks"
BKMENC="$HOME/Dropbox/USER.dockbox/Bookmarks.enc"
0 * * * *  openssl enc -aes-256-cbc -in $BKM -out $BKMENC -pass pass:"PASSWORD" -e -base64
```

##Configuration
You can enable (or disable) favicons by setting `loadFavicons` to
`true` (or `false`) in file `index.html` at `line 16`. Without favicons
page loads much faster.


P.S.
----

Will be glad to get any advice on how to improve the project.
