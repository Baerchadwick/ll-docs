# AWS CLI How-To

Instructions for getting the Amazon Web Services Command Line Interface running, with special focus on using it for the LL workflow.

## Installing

1. first make sure that you have `pip` installed.  Try typing `pip --version` into your terminal--do you get a version number back?  If not, you'll need to install it.  Do so by typing `sudo easy_install pip` and entering your password (to run the command as a "super user").
2. now use pip to install the command line interface: `pip install awscli --upgrade --user`
3. now aws is there on your computer (assuming you don't see some unforeseen error message), but it may not be easy to figure out precisely where it is.  When you use the `--user` flag to install the cli, it's probably going to end up in `/Users/[YOUR_USER_NAME]/Library/Python/2.7/bin` . . . go ahead and `cd` into that directory and `ls` to see if it's there. If it isn't there, try changing directories into `/Users/[YOUR_USER_NAME]/Library/Python` and see if you have another
4. If indeed it's there, you _could_ just run it by typing `./aws`, but it would be annoying to have to change directories and type that command each and every time.  What you want to do is add this folder to your PATH so that can just type `aws` from anywhere. To do that, get into your home directory (`cd ~`) and type `nano .bash_profile`. If you have a `.bash_profile` file, this will open it; if you don't, this will create it. Inside that file, you need to add the directory you found in step 3 above to your PATH. For instance
    ```
    export PATH="/Users/ll/Development/_tools:$PATH:/Users/ll/Library/Python/2.7/bin"
    ```
    This, for instance, adds `Users/ll/Development/_tools` and `/Users/ll/Library/Python/2.7/bin` to whatever's in the path already.
    Once you've finished installing, you should be able to type `aws --version` and see a result.
5. The next thing you need to do is configure the `awscli` by typing `aws configure`.  For all the details, you can look [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html), but basically you'll then need to enter three things:
    1. your AWS access key
    2. your AWS secret access key
    3. your default region (it's ok to stay with the default for now by hitting enter)
    4. your default output format (it's ok to stay with json as the default)
    You can get your keys from your administrator--do not share them with anyone. In fact, it's completely fine to delete them once you've configured the cli because we can totally get you new keys anytime you want.  This is not like a password--you won't have to enter it every time.  Which now means that your computer password IS the password to our S3 storage.  Which means that it needs to be insanely secure and that you can never leave yourself logged in on any machine.  **NEVER EVER.**
6. You should now have access to the bucket(s) your admin gave you access to.  You'll need to know the name of the bucket for the rest of the steps here, so make sure that you get it.  In the rest of the steps, we'll just call the bucket `my-bucket`.  But wherever you see this in the instructions you'll obviously replace it with the real name of your bucket.
7. To see what's in your bucket, type `aws s3 ls s3://my-bucket`.  Not all of the typical bash commands work with `aws s3`, but this one does.
8. To copy something to your bucket, type `aws s3 cp [path to my file] s3://my-bucket/subfolder/filename.ext`, with `subfolder` and `filename.ext` replaced with what you actually want them to be.
9. Typically, we want to copy very large numbers of files, and to do this we'll be copying folders recursively.  On our team, we often have things that need to go to s3 staged in a folder called `transfer_to_s3`, in which case, the recursive copy command might look something like this:
    ```
    aws s3 cp --recursive mydrive/2017/01 s3://my-bucket/2017/01
    ```
    And that's basically it!
