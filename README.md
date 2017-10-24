# Deliver it Well - Circle CI

## Introduction

Circle CI is a SaaS tool that easily allows a programmer to add **continuous integration** to their projects. By writing unit tests in a project, a development team is able to merge and push code several times a day without running into merge conflicts or broken code on production.

After integrating Circle CI with your project and writing unit tests, any push or merge to the `master` branch will kick off a few events:

- Circle CI will check for a .yml file describing the machine and what branches to deploy
- A server will be spun up to run your app
- All of your dependencies will be installed on that server
- The app will start running
- Any tests located in your test suite will all be automatically run
- The image of your app will be destroyed on the server and the server itself will be spun down
- If **all** of your tests passed, your merge or push will be allowed to happen. If one fails you will be notified and the code will not merge into your `master` branch.

This is a really useful approach for developments teams. As each developer integrates their branch into the master branch it enforces unit testing which can prevent a lot of bugs, especially if you have a well written test suite.

----

In this project we're going to:
 - Sync Circle CI to our Github account
 - Write a new test
 - Have Circle CI run your tests every time you push up a new change to the `master` branch
 - Automatically push your project to Heroku after a passing build


### Step 1 - Sync Circle CI
1. Using git, initialize this project to point to a Github directory on your Github account.
2. Make an account at [Circle CI](https://circleci.com), using Github as your login.
3. Click on the "Projects" tab on the left.
4. Click "Setup Project" on Github project you pushed from step 1 of this section.
5. Select **Linux**, **1.0**, and **Node** for the platform and language you want to deploy to.
6. In your project folder, make a `circle.yml` file. This will configure how Circle CI will deploy and test your project. Use the following to fill it out, keeping in mind that indentation matters:
```
deployment:
  prod:
    branch: master
    heroku:
      appname: your-heroku-app-name
machine:
  node:
    version: 8.1.4
```


7. Commit and push this file to your Github repo.
8. Now when you make pushes to `master` on your Github account, it will trigger the Circle CI service.

### Step 2 - Link to Heroku
1. In your Circle CI user settings, find the option for "Heroku API Key" and paste in your Heroku API key.
2. Back in your "Projects" tab, click on the project you setup in the previous step (Sync Circle CI) and click on the gear shaped icon to access its settings.
3. Associate a Heroku user with your account. This usually just consists of clicking the teal button of adding yourself as a Deploy User.
4. Make sure the 'appname' key in your `circle.yml` file matches the name of your Heroku app exactly.

### Step 3 - Write a New Test
1. We have a couple of basic tests in your repo folder for this exercise. Take a look inside `server.spec.js`. You'll see that it check that a 200 response comes back from your app and that "Hello World" is inside an `<h1>` tag.
2. We'd like to setup another test. You can copy the last test on line 32 and change what it's looking for to be a string that you can define.
3. In `/public/index.html` change the text in between the `<h2>` tag to match the new string you're testing for in Step 2.

### Step 4 - Continuously Integrate
1. Open up your Circle CI dashboard so you can see the process in real time in our next step.
2. Commit your changes and push them to your repo on Github.
3. In your Circle CI dashboard you can watch the process as your container is provisioned, your app is started, tested, and then broken down.
4. If your tests pass green, if you missed something and your tests fail, Circle CI will prevent the commit from merging and alert you.

## Exit Criteria
- Your Github account is linked to your Circle CI accoun
- You wrote a new test to check for text on an HTML page served by the Express provided app
- When you push a commit or merge to the `master` branch of your repo, Circle CI runs your tests and lets you know if they passed
- Your project gets automatically deployed to Heroku

## Bonus
- Figure out how to deploy to AWS instead of Heroku
