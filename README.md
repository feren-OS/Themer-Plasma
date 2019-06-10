# Themer Plasma
The Feren OS Themer Utility for the KDE Plasma Desktop Environment

<h2>What is Themer?</h2>
Themer is a utility for Feren OS that manages the transformation of the user's desktop to transform it into whatever the user desires, as long as it's a theme made for Themer. Starting life as a small utility in Cinnamon that simply changed the themeing of the Cinnamon Desktop to match a specific Operating System, eventually growing into a whole theme and panel layout changer for Cinnamon that integrated into Cinnamon and then even going as far as changing some external applications' look and feels as well, Themer has taken the concept of Zorin Appearance from Zorin OS and has expanded greatly on the idea, making even custom themes compatibility a possibility.

As for its role in the Plasma version, Themer runs in conjunction with the application of a Look & Feel package in Plasma to expand the array of configurations that a Look & Feel package affects, as well as adding some extra benefits to the L&F system.

<h2>How does Themer work?</h2>
As elaborated into earlier, Themer runs as a background process to scan for a change in the value of the setting in Plasma that determines the Look & Feel that Plasma knows to have last been applied. When a change is detected, it will run its main script, themer-file-apply-kde, to apply any extra settings provided by the theme, if there are any.
If a standard Look & Feel is applied, Themer will warn the user that this Look & Feel does not support Themer so the extra capabilities of Themer will not be used, outside of setting the icon theme and cursor theme in GTK Applications.

However, this current implementation is flawed. For one, Themer has no idea if the user chose for the Look & Feel's desktop layout to also be applied or not and for two it cannot detect the application of a Look & Feel if a L&F is re-applied after being applied in the past. If anyone can figure out a method to get around these quirks, a Pull Request would be welcomed.

<h2>How would a standard Look & Feel theme be made fully compatible with Themer?</h2>
To make a Standard L&F fully compatible with Themer, you need to create a folder in the Look & Feel's 'contents' folder called 'feren-themer' followed by a file in there called 'details'.

Here's an example of what should be inserted into 'details':
```
[THEMER THEME]
GTKTheme=Breeze
WMLayout=M:IAX
DockType=None
LatteTheme=Default
FilesStyle=ferenOS
AppLauncher=False
MaximisedTitlebarHide=False
LatteMetaFocus=False
DarkWMColour=BreezeDark
```

As for what the values you can use do:

- GTKTheme - Sets the GTK Theme for GTK 2 and 3 Applications to the value of this setting
- WMLayout - Sets the Titlebar Layout for KWin and GTK Headerbars. The value should be the KWin Window Order value, as the scripts will handle the translation of this value when applying it to GTK+ Applications.
- DockType - Setting to control the dock used. Either Docky, Latte or None
- LatteTheme - Setting to control which Latte Dock layout is used by Latte Dock
- FilesStyle - Value for Feren OS that changes the Look & Feel of the Nemo File Manager
- AppLauncher - Soon-to-be depreciated setting
- MaximisedTitlebarHide - Whether or not KWin should hide the titlebars of maximised windows, comes in handy for Ubuntu Unity layouts
- LatteMetaFocus - Whether or not Meta should be assigned to Latte Dock's applets instead of Plasmashell's Applets (this current integration might be usless under the latest available Latte Dock Unstable Version)
- DarkWMColour - Feren OS setting for deciding which colour scheme should be used for the titlebars of supported always-dark-themed applications

Of course, some of these options might be useless inclusions for your purposes, but this was designed strictly for Feren OS, which these options could come in handy for.

<h2>Forking</h2>
Given that this is designed for Feren OS exclusively, you may have to tweak a few things about Themer Plasma to make it work for you outside of Feren OS, but as long as you're willing to keep to the GPLv3 license, go ahead and see what you can do with it. I'd be all for this level of features being integrated upstream into Plasma someday, too.

<h3>Extra Notes</h3>

- For DarkWMColour to work, you'll need to create a Window Rule called 'Feren Themer GTK Dark Titlebars Workaround' with 'Titlebar colour scheme' on 'Force' with any colour you desire. As long as those criteria are met, any other changes can be made safely to this Window Rule and it should work as intended through this utility.
