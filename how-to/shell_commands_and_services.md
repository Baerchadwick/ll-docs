# CREATING A SERVICE FROM A SHELL SCRIPT

## CREATING THE MAKE_GIF SHELL COMMAND

If you want to streamline the process of making gifs, why not create a shell command to make it easier?  In Atom, try creating a file called `make_gif` (no extension) in your `/Development/_tools` folder, and add in the following code:

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


public/images/screenshots/make_gif_service.png
