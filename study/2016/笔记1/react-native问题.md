#Port already in use red-screen

Something is probably already running on port 8081. You can either kill it or try to change which port the packager is listening to.

Kill process on port 8081 

$ sudo lsof -n -i4TCP:8081 | grep LISTEN

then

$ kill -9 <cma process id>

Change the port in Xcode 

Edit AppDelegate.m to use a different port.

# Cannot read property 'root' of null
```brew update && brew unlink watchman && brew install watchman -HEAD```


AsyncStorage


