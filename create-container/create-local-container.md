# Create the MiGA Container

Start Docker if it is not already running.

Open a terminal. If you are running Windows, you can use the **PowerShell** terminal by typing "PowerShell" into the Windows search box in the lower left of the screen and hitting "Enter." Then download the Docker image to your computer by entering the following into the terminal window:

```text
docker pull miga/miga:1.0.2.4
```
**Note:** As of 11 May 2021 the tag must  be specified. 

Create the Miga container and link it to a directory on you drive, **i.e.** external to the image,  with the following: 

```
docker run -p 9090:3000 -it -v D:/miga:/root/miga-data -v db_volume:/miga/db --name miga miga/miga:1.0.2.4 /bin/bash
```
The line above enables file sharing with the container using the directory `D:/miga` on your computer. Edit this part of the command as appropriate. You will use this directory to input files to MiGA, and Miga will output results to this directory.   

by entering the following code into the terminal window one line at a time. In configuring Docker, we enabled file sharing with a directory we created to hold MiGA-Web results. If you are not using D:/miga-web as your results directory, substitute D:/miga-web in the first line with your results directory.

```text
docker run -p 9090:3000 -it -v D:/miga-web:/root/miga-data -v db_volume:/miga-web/db --name miga-web fyuan277/miga-web:v1.3 /bin/bash
cd miga-web/
export SECRET_KEY_BASE=`bundle exec rake secret`
bundle exec rails server -e production -b 0.0.0.0 -p 3000 Puma
```

You must leave this terminal running while you use MiGA-Web.

Open a browser window and enter "localhost:9090" as the URL. The Miga-Web home page will open, asking you to create an account or log in. Create an account by entering a user name, email, and password.

To shut down MiGA-Web, return to the terminal you used above, hold down the **Ctrl key** and type "C." Open a new terminal and enter:

```text
docker stop miga-web
```

The next time you want to use MiGA-Web, open **PowerShell** and enter:

```text
docker start miga-web
docker exec -it miga-web /bin/bash
cd miga-web/
export SECRET_KEY_BASE=`bundle exec rake secret`
bundle exec rails server -e production -b 0.0.0.0 -p 3000 Puma
```

Then start your browser and enter "localhost:9090" as the URL.

