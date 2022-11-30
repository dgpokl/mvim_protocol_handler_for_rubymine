# mvim_protocol_handler_for_rubymine
MacVim (mvim:...) protocol handler for RubyMine. Allows opening mvim:// links (used in honeybadger.io, etc) in RubyMine by converting them to x-mine: URLs and opening those.

I chose to implement the mvim: protocol because I also use textmate and didn't want to lose TextMate support by taking over txmt: or have to fight with TextMate to own that scheme.

The difference seems to be that mvim expects a "url" parameter and that looks like url=file:///Blah/blah while RubyMine expects a "file" parameter and that looks like file=/Blah/blah. Note: I made an assumption that the "url" parameter will be the first parameter - if it's not, this will break.

## Requirements
1. Rubymine, version unknown (5.4+??) but the x-mine: URLs work fine in version 8. See https://youtrack.jetbrains.com/issue/RUBY-484
2. You probably shouldn't have MacVim installed. I don't know how to resolve the conflict if you have 2 apps trying to implement the same scheme. Probably one will work and one won't.

## Background

Honeybadger can be configured to render links with a custom protocol in order to launch an editor. If you use Honeybadger, you can set this up here: https://app.honeybadger.io/users/edit - Use the "MacVim" option :)

## How to use

#### Option 1: Build it yourself:

1. Open the Script Editor
2. Use the contents of the main.scpt file here
3. Save it in /Applications or ~/Applications
4. Add in this section to your application's info.plist:
````
    <key>CFBundleURLTypes</key>
    <array>
    	<dict>
    		<key>CFBundleURLName</key>
    		<string>mvim protocol handler</string>
    		<key>CFBundleURLSchemes</key>
    		<array>
    			<string>mvim</string>
    		</array>
    	</dict>
    </array>
````
5. Open your app once and accept any warning. It will just exit without doing anything after you do this.
6. Test it by clicking a link in your browser, or, by doing something like this on the terminal:
````
    open 'mvim://open/?url=file:///path/to/file/file.rb&line=3'
````

#### Option 2: Pre-built app

I've already built a working copy of this for ease of distribution, but you should probably examine the scpt file in the "Package Contents" before running this app on your system to make sure it only does what it says it does.

1. Find and unzip pre-built app in the 'release' folder of this repository.
2. Put it in /Applications or ~/Applications
3. Open your app once and accept any warning. It will just exit without doing anything after you do this.
4. Test it as above.

## Acknowledgements
Credit to https://yourmacguy.wordpress.com/2013/07/17/make-your-own-url-handler/ for the tutorial
