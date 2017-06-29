
https://www.r-bloggers.com/how-to-install-r-on-linux-ubuntu-16-04-xenial-xerus/

* to run R: R  # default install: R must be capitalized 
* should use "sudo R" if you want to install packages easily
 - otherwise, create your own package directory

```
sudo R
```
```R
install.packages(c("dplyr","tidyr","RPostgreSQL"))
```

RPostgreSQL download failed...

Want to use RPostgreSQL?  Need Java...
```
sudo apt-get install openjdk-9-jre
```
Still can't install RPostgreSQL...
Trying advice found [here](https://stackoverflow.com/questions/22202141/installing-rpostgresql-on-linux)
```
sudo apt-get install libpq-dev
```

Oh yay!  It worked: this allowed me to successfully install RPostgreSQL.

