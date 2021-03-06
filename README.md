# git_push-maven_compile-copy_to_karaf
When a developer pushs his code as a Maven project to the given git server. The code will be compiled by Maven on the git server and copied to a remote machine for the running Karaf instance. With the help of Jenkins as a CI/CD tool.

<b>Assumption:</b> Ubuntu/Debian Server with Git server, Python 3 and its package dependecies with pip, Jenkins successfully installed. Communication between Server/Client is working. Developers work with Maven projects and have access to the git repository.

<b>Hint:</b> The installation of Jenkins is described in the file ```Jenkins-Installation.md``` in this repository.

### After installing successfully Tomcat and Jenkins and create an user account inside Jenkins. Now on the VM, there is an account with username: #your-choosing-username and password: #your-password

Open on your client a browser. Type in the link to your server:  ```http://your-ip-adress:8080/jenkins```

It's time to create our chain. First go to "New Item" on the left handside of Jenkins Dashboard:
![Alt Tag](https://user-images.githubusercontent.com/7670731/54187840-b1d47580-44ae-11e9-8f66-42f896bebb17.png)


Then this will apppear:
![Alt Tag](https://user-images.githubusercontent.com/7670731/54187845-b39e3900-44ae-11e9-80ff-80bbd549f0ef.png)


Choose "Freestyle project" and give the project the name. 

Since my first "job" in Jenkins is "Git-Check", I give "Git-Check" as name of a job → click on OK.
![Alt Tag](https://user-images.githubusercontent.com/7670731/54187848-b567fc80-44ae-11e9-9a04-b326e6f91ec7.png)

Scroll down to "Build"

Click on "Add build step".

Select "Execute shell". This will give you a textfield to type in where your shell-script should be.

There I give the path where Jenkins can find my Shell-Script to execute. In this case it is in: 

```/home/localadmin/jenkins-home/scripts/git-check.sh```

The according script file name is: ```git-check.sh```

This file will check if some new source code uploaded to Git, then it will give the status: "new code downloaded" and "nothing to do" otherwise.

After typing in Jenkins where the script can be founded by Jenkins, just hit "Save" to create the first job in Jenkins.

Already you can execute the first job. When you wisch, you can "build" it.

This process you do for two another jobs, namely: Maven-Source and Deploy-Bundle. For the job Maven-Source you need the shell script:  ```maven-build.sh```

and the job Deploy-Bundle needs: ```deploy-bundle.sh```

The shell script ```deploy-bundle.sh``` needs a Python-script to be able to deploy the bundle to a client running Karaf, the file name is ```datacopy.py```


After creating these three jobs you start the first job and the chain will be automatically complete. 

Have fun!
