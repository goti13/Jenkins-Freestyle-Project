# Jenkins-Freestyle-Project
Creating a Jenkins Freestyle Project

Jenkins Job
In Jenkins, a job is a unit of work or a task that can be executed by the Jenkins automation server.
A Jenkins job represents a specific task or set of tasks that needs to be performed as part of a build or deployment process. Jobs in Jenkins are created to automate the execution of various steps such as compiling code, running tests, packaging applications, and deploying them to servers. Each Jenkins job is configured with a series of build steps, post-build actions, and other settings that define how the job should be executed.

# Creating a Freestyle Project
Let's create our first build job

i. From the dashboard menu on the left side, click on new item

![image](https://github.com/user-attachments/assets/21cb7518-59b3-4e2d-86f2-1e85f78d6cd2)

ii. Create a freestyle project and name it "my-first-job"

![image](https://github.com/user-attachments/assets/43751108-683f-4602-8861-d3510eac6352)

# Connecting Jenkins To Our Source Code Management

Now that we have created a freestyle project, let connect jenkins with github.

i.  Create a new repository called jenkins-scm with a README.md file

ii. Connect "jenkins' to 'jenkins-scm' repository by pasting the repository url in the area selected below. Make sure your current branch is 'main'


<img width="1173" alt="image" src="https://github.com/user-attachments/assets/42e051db-960e-4980-a26d-52642f028d96" />


<img width="1220" alt="image" src="https://github.com/user-attachments/assets/491afcf0-cc18-4da4-beed-9f754e3cdd60" />


iii. Save configuration and run "build now" to connect jenkins to our repository

<img width="1031" alt="image" src="https://github.com/user-attachments/assets/30b88a44-236c-4b9a-b1ef-6560bdad2549" />

We have successfully connected jenkins with our github repository (jenkins-scm)

Configuring Build Trigger

As a engineer, we need to be able to automate things and make our work easier in possible ways. We have connected "jenkins' to 'jenkins-scm', but we cannot run a new build with clicking on

'Build Now'. To eliminate this, we need to conflure a build trigger to our jenkins job. With this, jenkins will run a new build anytime a change is made to our github repository

i. Click "Configure" your job and add this configurations

ii. Click on build trigger to configure triggering the job from GitHub webhook

![image](https://github.com/user-attachments/assets/9fbd2376-4a42-4c0d-bf58-9804229802e9)

iii. Create a github webhook using jenkins ip address and port

<img width="945" alt="image" src="https://github.com/user-attachments/assets/633eb70e-54fb-47cc-8c47-d1c39609380a" />

![image](https://github.com/user-attachments/assets/6bb3d016-1093-4565-a3b0-91ebbd428ccb)

Now, go ahead and make some change in any file in your GitHub repository (e.g. README.MD file) and push the changes to the master branch.
You will see that a new build has been launched automatically (by webhook).


NOTE:

If you installed docker on a local host, Adding the localhost address to the "payload url" of your github will not work. You will need to use a tool Called ingrok.

What is ngrok?
ngrok is a tool that creates a temporary public URL that forwards requests to your local machine.

**Steps to Use** ngrok **for GitHub Webhooks**

1. Install ngrok (if not already installed)

```
brew install ngrok  # macOS (using Homebrew)
sudo apt install ngrok  # Ubuntu/Debian
choco install ngrok  # Windows (Chocolatey)
```
2. Start an ngrok tunnel for your Jenkins instance running on 8080

```
ngrok http 8084
```
3.  Get the Public URL

After running the command, you’ll see output like this:

```
Forwarding    https://random-name.ngrok.io -> http://localhost:8084

```
Use the https://random-name.ngrok.io URL in your GitHub webhook’s "Payload URL"

4. Configure the Webhook in GitHub

* Go to your GitHub repo → Settings → Webhooks → Add webhook
* In Payload URL, enter:
  
  ```
  https://random-name.ngrok.io/github-webhook/
  
  ```
* Set Content type to application/json
* Set Events to Just the push event (or customize)
* Click Add webhook
Now, GitHub will send webhooks to your localhost via ngrok.
