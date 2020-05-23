---
title: "How I got started in Automated Testing"
original: https://www.utest.com/articles/how-i-got-started-with-automation
published: true
---

My first job in quality assurance was testing a windows desktop product as a manual tester. I really enjoyed getting to setup and test many different operating systems, servers, and mobile phones. The main part of my job was working with a desktop application that interacted with a server and a mobile phone.

After verifying that bugs were fixed and finding some bugs with the installation / uninstallation process I created a simple script (Bash file) which I could run before the software was installed. The script would clean out any of the artifacts left behind after the software was uninstalled. The script initially simply deleted files left in temporary folders. The script eventually became more complicated as it started to delete registry keys and delete files found across the operating system. This ended up being a great time saver and really helped my teammates too.

When I look back on it, that was the first bit of automation I did. It automated deleting of files and by simply guaranteeing(as best I could) that the computer was clean, it greatly assisted with my productivity (I found a bunch of bugs because when uninstalling the software was not setting the system back to a clean state and we were leaving around files we really shouldn't have been)

Eventually I moved on from that team to work on an automation framework and was glad to hear that the script was still being used years later.
