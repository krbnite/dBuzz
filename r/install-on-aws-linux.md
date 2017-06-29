
https://www.r-bloggers.com/how-to-install-r-on-linux-ubuntu-16-04-xenial-xerus/

* to run R: R  # default install: R must be capitalized 
* should use "sudo R" if you want to install packages easily
 - otherwise, create your own package directory

```
sudo R
```
```R
# I'm doing a "light installation" here, which basically means
#   install anything Hadley
install.packages(c("dplyr","tidyr","stringr","ggplot2","lubridate","RPostgreSQL"))
```

RPostgreSQL download failed...

Want to use RPostgreSQL?  Need [Java](http://openjdk.java.net/install/)...
```
sudo apt-get install openjdk-9-jre
```
Still can't install RPostgreSQL...
Trying advice found [here](https://stackoverflow.com/questions/22202141/installing-rpostgresql-on-linux)
```
sudo apt-get install libpq-dev
```

Oh yay!  It worked: this allowed me to successfully install RPostgreSQL.

Important:  If you have a .RProfile that loads custom functions, libraries, etc, which
you are used to having, then make sure to sftp-put it in your AWS linux home directory.

