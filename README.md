# Node Todo App with CI/CD: Level Up Your Productivity Game

Are you ready to ditch the pen and paper, embrace the digital realm, and conquer your to-do list like a boss?  This Node.js-powered todo app, with its slick Express framework and EJS templating engine, is about to become your new productivity BFF.  And to keep things deploy-tastic, we've got Jenkins and Docker Compose on board for continuous integration and deployment (CI/CD) – fancy talk for making sure your app is always up-to-date and ready to rock.


## But first, things first:

To run this app, you need to have:

- Git it? You'll need Git installed to snag a copy of this awesome app from GitHub. Think of it like your personal transporter to the land of code.
- Jenkins jammin'? Make sure you have Jenkins up and running on your machine or server. It's your mission control center for CI/CD. 
- Docker dreams? Docker and Docker Compose are like the dynamic duo of containerization, keeping your app's environment tidy and consistent.
  
## Ready to clone and rock? Let's do this:

### Step 1: Clone the Repository

To clone the repository, open a terminal or command prompt and run the following command:

```bash
git clone https://github.com/devopscloudlabs/nodejs-todo-cicd.git
```

This will create a folder named `node-todo-cicd` in your current directory.

### Step 2: Webhook wizardry (Add a Webhook):

To add a webhook, go to your GitHub repository and click on **Settings**. Then click on **Webhooks** and then on **Add webhook**.

Fill in the form as follows:

- Payload URL: Enter your Jenkins URL followed by `/github-webhook/`. For example, `http://example.com/github-webhook/`.
- Content type: Select `application/json`.
- Secret: Leave it blank.
- SSL verification: Select `Enable SSL verification` if your Jenkins URL uses HTTPS, otherwise select `Disable SSL verification`.
- Which events would you like to trigger this webhook?: Select `Just the push event`.
- Active? Absolutely! Check that box to activate the webhook. ✅
Click "Add webhook" to complete the ritual. You can test it by clicking "Edit" and then "Test" – a green check mark means webhook success!

### Step 3: Deployment dojo (Deploy the App)

Time to unleash your app to the world! In your Jenkins dashboard, click on **New Item**.

Enter a name for your job (e.g., Node Todo App) and select **Freestyle project**. Then click **OK**. Add some flavor to your project with a detailed **description**.

Under **Source Code Management**, select **Git** and enter the repository URL: [https://github.com/devopscloudlabs/nodejs-todo-cicd.git]. You can leave the other fields as default.

Under **Build Triggers**, select **GitHub hook trigger for GITScm polling**. This will enable the job to be triggered by GitHub webhooks.

Under **Build**, click on **Add build step** and select **Execute shell** (or **Execute Windows batch command** if you are using Windows). This will allow you to run any shell or batch command as part of your job.

In the text area that appears, enter the command `docker-compose up -d --build` to build and run the app using Docker Compose. The `-d` flag runs the container in detached mode and the `--build` flag forces a rebuild of the image if there are any changes.

Click **Save** to save your job.

Now, whenever you push any changes to your GitHub repository, your Jenkins job will be triggered automatically and deploy your app using Docker Compose.

You can also manually trigger your job by clicking on **Build Now** on your Jenkins dashboard.

You can see the status and details of your job under **Build History**. You can also click on **Console Output** to see the logs of your job.

You can verify that your app is running by going to your browser and typing `http://localhost:8000`. You should see a todo app where you can add, edit, and delete tasks.
