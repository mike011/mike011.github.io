---
title: "How I added dark mode to SPOKZ"
published: true
---

Spokz is a cycling app that lets you stay connected with your friends while riding. It's for both iOS and Android. Recently with iOS 11, the ability to have apps run in dark mode was added. I'm a huge fan of dark mode and wanted to add it to the Spokz app. This is the story of how I went about adding it.

# Attempt 1

First step was to remove from the plist forcing the app to always be in light mode. Then I launched the app and changed the simulator to dark mode. This made it very obvious where custom options were chosen and inappropriate contrast was showing up. Then I went through all the xibs (about 25) and changed the colors where appropriate to the dark mode friendly versions. For example the background color from custom or white to system background color. Or a text label to system label color.

Next up was to go screen by screen and see what text looked ugly in dark mode and try to fix it This was done by massaging the code to choose another color or not to choose a color at all. The default for a lot of values was white. Then I looked at the assets shown on the screen to update them or provide new ones for dark mode. For example there were some background that didn't look good in dark mode.

Well this didn't turn out well and ended up blowing up in my face as it wasn't appropriate in Spokz to use semantic colors from Apple for the following reasons.
1. Spokz in light mode on some screens had a dark blue background with light text. For dark mode, the text is also light, but I found the background too bright for dark mode. So I tried darkening the background, but this looked ugly. I eventually came to the idea of making the background black and change the text to being the Spokz blue color. This had a nice pop to it and kept some consistency in showing the Spokz blue color.
2. Spokz also has various screens with a blurred out image in the background. The text is also white. But once again felt too bright in dark mode.
3. Spokz also has white backgrounded screens, but with blue Spokz text.
4. There were lots of places in the app where colors by names are referenced. This doesn't work in the semantic color world as you are now supposed to reference colors by purpose. For example instead of spokzBlueColor is should be textColor.

# Attempt 2

So I started a second time and my plan was going with point 3 and first remove all references to colors by name and replace them with there purpose. spokzBlue is used over 250+ times in the app with many overloaded meanings, sometimes it means a background, a tint, or a text color. But this ended up not working because I didn't know what spokzBlue meant in the context and so I backed off from this plan.

# Attempt 3

Now onto my third attempt and I have been going screen by screen creating having a consistent dark and light mode for each of the 4 above different type of screens. Also using semantic colors to define the names and have them defined in the asset catalog so it's easy to see. This has still been tricky getting the subtleties right and trying to make the app more consistent across the board.

Well the Code was originally all in Objective-C so I continued that trend, but this seemed so backwards. And after talking to the owner of the repo, he really wanted new code in Swift. This really wasn't a lot of new code, but massaging old code, but I didn't want it in Objective-C. So I spent hours rewriting the Objective-C code in Swift and add all the @objc identifiers when needed or importing the bridging header into the Objective-C files. This greatly help identify the locations where the old color name(spokzBlueColor for example) was still being used. So this made it easier to cleanup.

After this I reviewed it with the owner of the repo and he wasn't happy with how the colors looked in dark mode and wanted a simpler solution. The problem was that some screens had certain nuances where special variants were needed. So next step was to go through those screens and remove the nuances. This is taking forever so I've taken some time off. I was hoping to have this wrapped up by now, but is turning out to be a huge change. Now that change is too big and dangerous, so a simpler approach needs to be created.

# Attempt 4

After being so frustrated with the first 3 attempts and the amount of rework need this has never happened as of yet. Maybe one day.
