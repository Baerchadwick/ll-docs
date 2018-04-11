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
3. You should now be able to run ffmpeg and ffprobe from the command line.  To get a whole bunch of information about a video file, type `ffprobe path/to/my/movie.mov`, replacing that path with the actual path to your file (you can actually DRAG the file from Finder into the terminal window and when you let go the path will magically appear).  To get nicely formatted, more readable JSON, type `ffprobe -v quiet -print_format json -show_format -show_streams path/to/my/movie.mov`, again substituting your path for that placeholder.  That JSON output is what we use throughout [thelocalworkflow](https://github.com/learninglab-dev/thelocalworkflow) to get information on the video files we want to manipulate.
4. To transcode a video and strip the audio, for instance, you can type `ffmpeg -i input.mov -c:v libx264 -preset slow -crf 22 -an output.mp4`, and this sort of conversion is one of the things ffmpeg is great for.
5. To take a short piece of video and turn it into a `.gif` file you COULD enter `ffmpeg -i input.mov output.gif`, but if you try that you'll see that you end up with a monstrously large gif. Typically you'll want to reduce the resolution and maybe even the frame rate.
6. To reduce the framerate, try adding `-vf scale=480:270` to your command.  This will reduce each dimension to 25% of the original 1920x1080 file.  The complete command is now `ffmpeg -i input.mov -vf scale=480:270 output.gif`.
7.  If you want to take your gif-making seriously, you'll want to generate a `palette.png` file from the colors that are present in your image. Read [this link](http://blog.pkh.me/p/21-high-quality-gif-with-ffmpeg.html) if you want to learn more, but the tldr of it is that you can only use 256 colors in your gif, and instead of just choosing the 256 that run across the entire spectrum, you should choose 256 that actually correspond best to your image (a gif of Donald Duck needs yellow-oranges and blues, but no reds, for instance). To accomplish this you actually need to run two commands:

    ```
    ffmpeg -i input.mov -vf palettegen palette.png

    ffmpeg -i input.mov -i palette.png -vf scale=480:270 output.gif
    ```
    This should get you a relatively small gif that will work well on slack.

## CREATING THE MAKE_GIF SHELL COMMAND

If you want to streamline the process of making gifs, why not create a shell command to make it easier?  In Atom, try creating a file called `make_gif.sh` in your `/Users/ll/Development/_tools` folder, and add in the following code:

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
Here we find the directory that contains the video file (so that we can put the gif there), then we find the base file name and use it to generate a path for the gif.  Then we run our two gif-creation commands, and finally get rid of the palette we generated.
To run the script, you'll need to make it executable by entering `chmod 755 make_gif.sh` (making sure that you are in the right directory when you type this). If you've put the script in `/Users/ll/Development/_tools` (and you've followed the above steps to put that path in your `$PATH`) then you should be able to type `make_gif.sh /path/to/your/video.mov` and end up with a gif called `/path/to/your/video.gif`.

## CREATING THE MAKE_GIF SERVICE

If you REALLY want to streamline the process of making gifs, consider creating an automator service.  

1. open up Automator and, when prompted, select "Service" as the type of thing you'd like to build.
2. for the first step, select "movie files" as the type of file the service will receive (see image below) and select "Finder" as the context within which the service will work.
3. Next, add a new workflow step by selecting "Run Shell Script" from the searchable catalog of options.
4. Paste in the following code:

    ```
    PATH="/usr/local/bin:/Users/ll/Development/_tools:$PATH"
    for f in "$@"
    do
	      /Users/ll/Development/_tools/make_gif.sh $f
        echo "done with ${f}"
    done
    ```
    If you want to know what this does, it first ensures that the `$PATH` variable contains all the paths we need it to contain if it's going to find all the dependencies.  Then it loops through all the files you've selected and runs the `make_gif.sh` shell command.
    [img]()

public/images/screenshots/make_gif_service.png
