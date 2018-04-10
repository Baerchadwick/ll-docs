# CREATING A SERVICE FROM A SHELL SCRIPT

## INSTALLING THE TOOLS

There are a couple of command line tools that we use a lot for processing video: [ffmpeg and ffprobe](https://ffmpeg.org/).  They may well be installed on your machine already, so type `ffmpeg -version` and `ffprobe -version` to see if you get results.  If you don't, then follow these steps to install:

1. Download ffmpeg and ffprobe [here](https://evermeet.cx/ffmpeg/). You want to download the latest release (on the right) as a DMG.  Once downloaded, double click and it will mount as a disk image. Drag the file into `~/Development/_tools`.
2. make sure that the path to the folder holding ffmpeg and ffprobe is in your PATH variable. If you type `echo $PATH` into the terminal, you should see `/Users/ll/Development/_tools` (with "ll" being whatever your user name is).  If you don't see this, open/create a file called `.bash_profile` in your home directory:

    ```
    cd ~
    nano .bash_profile
    ```
    Once in there, add `/Users/ll/Development/_tools` to the `$PATH` variable:

    ```
    export PATH="/Users/ll/Development/_tools:$PATH"
    PS1='\W $ '
    ```
3. You should now be able to run ffmpeg and ffprobe from the command line.  To get a whole bunch of information about a video file, type

## CREATING THE MAKE_GIF SHELL COMMAND

If you want to streamline the process of making gifs, why not create a shell command to make it easier?  In Atom, try creating a file called `make_gif.sh` in your `/Development/_tools` folder, and add in the following code:

    ```
    DIR=$(dirname "$1")
    PALETTEPATH="${DIR}/palette.png"
    FILENAME=$(basename "$1")
    FILENAME="${FILENAME%.*}"
    GIFPATH="${DIR}/${FILENAME}.gif"
    ffmpeg -i $1 -vf palettegen $PALETTEPATH
    ffmpeg -i $1 -i $PALETTEPATH -vf scale=640:360 -y $GIFPATH
    rm $PALETTEPATH
    ```


## CREATING THE MAKE_GIF SERVICE

If you REALLY want to streamline the process of making gifs, consider creating an automator service.  

1. open up Automator and, when prompted, select "Service" as the type of thing you'd like to build.
2. for the first step, select "movie files" as the type of file the service will receive (see image below) and select "Finder" as the context within which the service will work.
3. Next, add a new workflow step by selecting "Run Shell Script" from the searchable catalog of options.
4. Paste in the following code:

    ```
    PATH="/usr/local/bin:/Users/mk/Development/_tools:$PATH"
    for f in "$@"
    do
	      /Users/mk/Development/_tools/make_gif.sh $f
        echo "done with ${f}"
    done
    ```
    If you want to know what this does, it first ensures that the `$PATH` variable contains all the paths we need it to contain if it's going to find all the dependencies.  Then it loops through all the files you've selected and runs the `make_gif.sh` shell command.
    [img]()

public/images/screenshots/make_gif_service.png
