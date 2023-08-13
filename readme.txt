Checking to execute job2 master branch after commit

#Create Jenkins job2 (you can copy from job1 and make changes for git branch specifier and description, dockerbuild port is 82 to avoid conflict with test environment)
#description: This a project to execute the job2 in Sritest using git hubwebhooks and using Master branch
#git hub project:https://github.com/andhukuri/Capstone.git/
#rescrict where this project can run: sritest
#Branchspecifier: */master

#below is the build command
#List all stopped containers, Get the container IDs of all stopped containers,Remove all stopped containers, regardless of whether they are running or have unsaved data.
sudo docker rm -f $(sudo docker ps -a -q)
# Create the Docker image
sudo docker build /home/ubuntu/jenkins/workspace/sritestjob2 -t masterapp
# Run the Docker image in a container
sudo docker run -itd -p 82:80 masterapp

#After successful run of job2 add post build steps to run job3 for final release


#Job 3
#description: this a project to execute job3 in sriprod using git hubwebhooks and using the Master branch after job 2 or sritestjob2 is executed successfully.
#git hub project:https://github.com/andhukuri/Capstone.git/
#rescrict where this project can run: sriprod
#Branchspecifier: */master


#List all stopped containers, Get the container IDs of all stopped containers,Remove all stopped containers, regardless of whether they are running or have unsaved data.
sudo docker rm -f $(sudo docker ps -a -q)
# Create the Docker image
sudo docker build . -t finalrelease
# Run the Docker image in a container
sudo docker run -itd -p 82:80 finalrelease


