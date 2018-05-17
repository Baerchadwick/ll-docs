# Ingesting and Renaming Raw Footage

This guide is intended to help you through the workflow of ingesting raw footage and logging it into our database.

## Step 1: Importing
Shoots that need to be imported are placed into the Nicholas Cage (left) side of the card bin at the MPA station. Each clear bin will contain all of the cards associated with a shoot, as well as a label with the __Shoot ID__.

Each __Shoot ID__ begins with the date of the shoot, followed by what number that shoot was that day, and the label that identifies what the shoot was for.

In this example, I'll be ingesting a shoot labeled *20180511_001_LLS_Planning*.

Based on the label, we know it happened on May 5th, 2018, which was a Friday. The _001_ tells us it was the first shoot of the day, and *LLS_Planning* labels it as a planning meeting for the Learning Lab.

Grab a clear plastic bin to begin your adventure!



1. Open the drive in Finder. Since I'm importing a Friday shoot, I'm using the Friday drive. It should look similar to this when you open up a daily drive.
![Friday Drive layout](https://raw.githubusercontent.com/ll-fellows/ll-docs/master/screenshots/FridayDrive_001.png)
   - Inside the footage tab, I've created a folder labeled with the date. This folder will be where will will be putting all the shoots that we import from the day.

2. Open Final Cut Pro X! Before we can import, we need to create a new library so our footage will copy directly to the Friday drive and not to the desktop or a random RAID or Hoth.
    -  File > New > Library will bring us to this: ![New Ingest Library](https://raw.githubusercontent.com/ll-fellows/ll-docs/master/screenshots/IngestLibrary.png)
    - You can see that I have the __Ingest__ folder selected so the library saves to the Friday drive and not to the desktop or to a random RAID or Hoth.

3. When selected on the library, a menu for it will show up on the right. If you don't see this, select this little thing on the top right: ![levels](https://raw.githubusercontent.com/ll-fellows/ll-docs/master/screenshots/Levels.png)

   - Now hit __Modify Settings__ next to Storage Locations, and under __Media__ select the __Ingest__ folder again!
![ingest modify](https://raw.githubusercontent.com/ll-fellows/ll-docs/master/screenshots/Modify_Settings.png)

4. Connect some cards! An import window should pop up in Final Cut.

    - On the right side, it will say the library that the footage is about to be imported to, and the location where the footage is going to be stored. This should match up with the library and settings that we've just modified.
![import dialogue box](https://raw.githubusercontent.com/ll-fellows/ll-docs/master/screenshots/Import_Dialogue.png)

   - You can see that the event corresponds to the event inside the library, and the files will be copied into the __Ingest__ folder.

5. SPECIAL TIP! For cards coming from a C300 (our studio cameras, the files usually start with A, B, or C) feel free to use the viewer in the box to select specific point to import if there are long periods of time with no action. This helps us cut down on file sizes.
![trimming imports](https://raw.githubusercontent.com/ll-fellows/ll-docs/master/screenshots/Selecting%20imports.png)

6. For SSD's, which typically come from the overhead camera (GH4), we can't trim before import. Instead, we will select the "Leave files in place" option under __Files__ and click import.
   - These files will show up immediately in our library. You can now select them, and create specific in and out points in the viewer.

   ![SSD select imports](https://raw.githubusercontent.com/ll-fellows/ll-docs/master/screenshots/Selecting%20GH4%20exports.png)

   - Once you've selected what you'd like to import, we can export this clip as a master file.

   ![master file save]()

7. Once files are done importing, you should see a folder called __Final Cut Original Media__ created in our Ingest folder.
   - Bring these files into their shoot folder, and place each into a file that corresponds to the camera that it came from.
   ![footage in folder]()

8. Open a new tab in terminal, and ensure you are in __thelocalworkflow__ directory. If the directory is not connected, refer to the (GITHUB INSTRUCTIONS) to see how to connect!
   - Copy the path to the folder containing the footage and enter __node thelocalworkflow --rename (path)__
![renaming script]()

   - Hit __Enter__ and you should see the script running! If it's successful your footage should look like this now!
   ![successfully renamed footage]()

9. That's it! Now that the footage is renamed it can be backed up to the Synologies and RAIDS.
