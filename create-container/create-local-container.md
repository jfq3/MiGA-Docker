# Create the MiGA Container

Start Docker if it is not already running.

If you are running Mac OS or Linux, open the terminal. If you are running Windows, open the **PowerShell** terminal by typing "PowerShell" into the Windows search box in the lower left of the screen and hitting "Enter." Then download the Docker image to your computer by entering the following into the terminal window:

```text
docker pull miga/miga:1.0.2.0
```

**Note:** As of 11 May 2021 the tag must be specified.

Create the Miga container and link it to a directory on you drive, _i.e._ external to the image, with the following:

```text
docker run -p 9090:3000 -it -v D:/miga:/root/miga-data -v db_volume:/miga/db --name miga miga/miga:1.0.2.0 /bin/bash
```

The line above enables file sharing with the container using the directory `D:/miga` on your computer. Edit this part of the command as appropriate. You will use this directory to input files to MiGA, and Miga will output results to this directory.

The command also sets port 9090 for use with the MiGA-Web like version of the program. It will be accessed by entering the URL `localhost:9090` in your browser.

Create and configure the initialization files by entering the following:

```text
cd miga/
miga init
```

The `miga init` command causes MiGA to check for dependencies and configure some files that it needs to run. When prompted, accept all of the defaults except answer "no" for `Should I include MyTaxa modules?`. MyTaxa is not included in the Docker version of MiGA.

Exit MiGA with the command:

```text
exit
```
