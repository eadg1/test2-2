### Jenkins+Nginx automatic deployment demo (via containers)
### This project is supposed to demonstrate the automatic site checkout from git and deployment to web server by Jenkins upon successfull bild
### It will run two vagrant boxed, one for Web server and one for Jenkins.
Requirements:
  #### OS: 
   * Linux w/ kernel version 5.x or later
  #### Software:
   * vagrant v.2.2.10
   * git client (optionally)
  #### Harwdare minimum/recommended:
   * RAM: 4 GB / 8 GB
   * HDD: 8 GB
   * CPU @2Hhz / @3Hhz
   
#### How to use:

1 Clone this project to some directory on you host
 * git clone https://github.com/eadg1/test2-2
 
or download as zip archive and extract to target directory

2 Navigate to /docker/setup/secrets folder

3 Rename key.pub.sample and privatekey.sample to key.pub and privatekey accordingly

4  Navigate to your keypair location (cd ~/.ssh) or generate a keypair if you don't have one:
 * on linux: Create RSA keypair, leaving the passphrase empty (just press Enter)
 
   * ssh-keygen -t rsa
   
 * on other OS: please refer your OS documentation
 
 5 Copy and id_rsa.pub contents into 'key.pub' file , and id_rsa contents - into 'privatekey' file or simply copy files under designated name to  the /docker/setup/secrets folder
 
 6 Copy /docker/setup/.env.sample as .env and fill out the environment variables.
 
 7 Navigate to root folder of the project and run 'vagrant up'
 
 8  Wait till boxes are up and running
 
 9 Navigate to http://192.168.2.10:8080 and login to Jenkins with credentials from step #6
 
 10 Wait till job run&execute (you may select build running on left and watch the process under 'Console output')
 
 11 Navigate to http://192.168.2.21/
  * You should see 'Hello World!' 
