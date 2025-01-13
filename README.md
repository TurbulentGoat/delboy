# Delboy
## The *safer* auto deleter

I created this because I've lost count of the times I've hit rm instead of mv. With Delboy, you can use `del <path/file_name>` just as you would with rm, but instead of permanently deleting the file **instantly**, it gets moved to a hidden `/.trash` folder that you set up. I've set my cron job to run once a day but you can do it as frequently or not as you like.

### Features
Safer Deletion: Files and directories are moved to a `/.trash` folder instead of being permanently deleted to give you some time before it's gone for good! 

Simple Command: Use `del` exactly as you would use `rm`.

Custom Trash Location: Configure the location of your `/.trash` folder based on your preferences.

### Installation
*(These are the paths I put mine in but the timer and `/.trash` folder can go anywhere you want I suppose.)*

**1) Clone the repository:**  
`git clone https://github.com/TurbulentGoat/delboy.git`

**2) Navigate to the directory:**  
Go to the delboy directory you just cloned.
`cd /delboy`

**3) Put the trash in the bin:**  
Put the "del" script in /bin. 
`sudo mv /del /usr/local/bin`

**4) Make it executable:**  
`chmod +x /path/to/del`
Replacing /path/to/ with the actual path obviously.

**5) Start the clock!:**  
Now you've deleted the file/folder/whatever, we need to set up a really simple bash script, which is run by an even simpler cron job.  
Go to `cd /usr/local/bin` and create a new script `vim deltimer.sh` with the following inside:

````
  #!/bin/bash
  #A basic delete/update script to clear out the trash once a day
  rm -rf ${HOME}/.trash/*
  echo "There goes the trash!"
 ````
And make that one executable too.  
`chmod +x /path/to/delTimer.sh`  
Replacing /path/to/ with the actual path obviously.

And finally, the actual timer (it's straightforward, I promise!) :
`crontab -e`

At the bottom, on its OWN LINE:
`59 23  * * * /usr/local/bin/deltimer.sh`

This will make it delete whatever is in the trash folder we set up once a day at 11:59pm. You can change that to any day/time/frequency that you want!

### Usage / removing accidental deletions
It couldn't get any simpler really - Instead of using `rm file.txt`, you would use `del text.txt`

This moves the file to `~/.trash/` instead of deleting it immediately.

If you realise you made a mistake, go to `/usr/local/.trash` and simply move the file to any other location.

### Contribution
Found a bug? Open an issue or create a pull request (or message me on reddit - I don't check there too often though).

Have a feature suggestion? Let me know, or feel free to implement it and submit a pull request.

### Requirements
* Python 3.x
* Bash (or compatible shell)

#### Possible Future Enhancements
No plans currently. Maybe something though, who knows.

#### License
This project is licensed under the MIT License.

#### Contact

For any questions or feedback, feel free to reach out to me on Reddit: [Turbulent_Goat1988](https://www.reddit.com/user/Turbulent_Goat1988/)

Thanks!
Louis.
