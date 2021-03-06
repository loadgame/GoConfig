GoConfig
========
##About
GoConfig is a easy-use comments-support configuration file(.ini) parser for the Go Programming Language.
It's based on [goconf](http://code.google.com/p/goconf/).

##Features:
- It simplified operation processes, easy to use and undersatnd; therefore, there are less chances to have errors. 
- It uses exactly the same way to access a configuration file as you use windows APIs, so you don't need to change your code style.
- It supports configuration file with comments each section or key which all the other parsers don't support!!!!!!!
- It Compiles!! It works with go version 1 and later.

##Example(Comments Support!!!!)
###Config.ini
	; Here are Comments
	[Demo]
	# This symbol can also make this line to be comments
	key1=Let's us GoConfig!!!
	
	[What's this?]
	; Not Enough Comments!!
	name=try one more value ^-^
###Code Fragment
```go
	// Open and read configuration file
	c, err := GoConfig.LoadConfigFile("Config.ini")
	
	// GetValue
	value, _ := c.GetValue("Demo", "key1")	// return "Let's us GoConfig!!!"
	// GetComments
	comments := c.GetKeyComments("Demo","key1")	// return "# This symbol can also make this line to be comments"
	
	// SetValue
	c.SetValue("What's this?", "name", "Do it!")	// Now name's value is "Do it!"
	// You can even edit comments in your code
	c.SetKeyComments("Demo","key1", "More comments")
	
	// Don't need that key or comments any more? Pass empty string "" to remove! that's all!'
	c.SetValue("What's this?", "name", "") // If your key was removed, its comments will be removed too!
	c.SetKeyComments("Demo","key1", "")
	
	// Finally, you need save it
	SaveConfigFile(c, "Config.ini")
```

###More Information
- All characters are CASE SENSITIVE, BE CAREFULL!
- If you use other operation systems instead of windows, you may want to change global variable [ LineBreak ] in conf.go, replace it with suitable characters, default value "\r\n" is for windows only. You can also use "\n" in all operation systems because I use "\n" as line break, it may look strange when you open with Notepad.exe in windows, but it works anyway. 