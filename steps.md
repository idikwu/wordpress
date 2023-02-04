Step1:
 create a Relational Database
Search for RDS
select create database
select mysql for engine type
template select free tier
enable public access

Step2:
Provision an Ubuntu EC2 instance 
ssh into the ec2 instance
ssh -i <keypair name.pem> ubuntu@<publicip of your EC2 instance>

Next you will need to install an apache2 web server to do this follow the steps below

sudo apt install apache2 php php-mysql php-curl mysql-client libapache2-mod-php unzip    //this line of script will install your lamp webserver i.e apache2,php,mysql,and their dependencies.

copy the EC2 Public ip adress and paste on a new tab it will open an apache server page

cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz        //this line of script will download a zip wordpress file to the /var/www/html directory
sudo tar xzf latest.tar.gz                //this will unzip it
when you run ls you will see that the file latest.tar.gz has been unzip and you have a wordpress folder

sudo mv wordpress/* .     //you move all the files in your wordpress folder to your current directory which is /var/www/html
                  
sudo rm latest.tar.gz     // delete the zip wordpress folder
sudo rm -r wordpress	  //delete the unzip wordpress folder
sudo rm index.html        //delete the index.html file that carries details about your apache so when you reload the public ip address of the EC2 instance it will load the index.php page for the wordpress

step3:
connect wordpress with rds
configure the wordpress
enter database name from your mysql RDS you created earlier
enter your username
enter password
for the database host enter the mysql RDS endpoint

STEP 4
push the wordpress directory to github
    Initialize a Git repository in the WordPress directory:
ensure you are at the /var/www/html directory then

git init

    Create a new repository on GitHub and note the repository's URL.

    Add the GitHub repository as a remote to the local repository:
git remote add origin https://github.com/username/repository.git

    Add all the WordPress files to the local repository:

git add .

    Commit the changes to the local repository:

git commit -m "Initial commit"

    Push the local repository to the GitHub repository:
git push -u origin master
