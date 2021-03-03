# Instructions to get started with projects

1. [Creating Repositories](#creating-your-repositories-step-by-step)
2. [Express Scaffolding](#express-scaffolding-step-by-step)
3. [React Scaffolding](#react-scaffolding-step-by-step)
4. [Full Stack App Scaffolding](#full-stack-app-step-by-step)
5. [Git Collaboration](#git-collaboration-steps)
   - [Option 1 - Forks](#option-1-forks)
   - [Option 2 - Branches](#option-2-branches)

## Creating your repositories step by step

1. On your GitHub page, select the `+` sign in the top right corner, and select `New repository`
2. Choose your project name (ideally in lower case)
3. Make this private (you can change it to public later on)
4. Initialize with a README if you haven’t already created one locally
5. Select `Create Repository`
6. Invite your instructor as a collaborator
7. Clone file as usual and start working!

## Express Scaffolding Step by Step

1. In your project repository on the terminal, run `npx express-generator` to scaffold the Express application
2. Open the folder in VSCode and remove the `/views` folder (we don’t use it)
3. Remove the view engine setup in app.js file (lines 12-14), because we’re not using any backend template renderers
4. Change `res.render('error')`; to `res.send('error')`; (again, we’re not rendering anything from the backend, we’re just sending responses back to the client)
5. Install packages that you may use, such as MySQL, Nodemon, or Dotenv: `npm install mysql nodemon dotenv`
6. In file `package.json`, remove jade from the dependencies list
7. Install dependencies with `npm install` or `yarn`
8. Copy the model folder from your previous projects. This contains the `helper.js` (which contains a nice wrapper around DB connections, so we can use the db() function from within our code), and it also contains the `database.js` file, which is the migration file for our project (you will need to modify this file so it contains YOUR database tables definitions and dummy data)
9. Add a new script into your `<package.json>` file, that we will use to run our migrations: `"migrate": "node model/database.js"`. Eventually, when you want to run migrations, you will need to run `npm run migrate` or `yarn migrate`
10. Modify the start script so it uses nodemon instead of node: `"start": "nodemon ./bin/www"`
11. In the file `./bin/www`, change the default port to `5000` (around line 15)
12. If you need to store private data and passwords (such as your DB pass), create a `<.env>` file in the Express project root.
13. Add a `.gitignore` file to your project. It should contain at least your `node_modules` and your `.env` file: `/node_modules` `.env`
14. Happy coding!

## React Scaffolding Step by Step

1. Create React app with `npx create-react-app my-app`. (Change `my-app` to the name of your app, e.g. `npx create-react-app emefa-mvp`.
2. In VSCode, in `src` folder, delete the `App.test.js`, `serviceWorker.js`, `setupTests.js` and `logo.svg` files.
3. In `index.js`, remove serviceWorker setup (lines 9-12), and the import from line 5.
4. In `App.css` remove the default styling, but keep the file for if you will use some css styling later.
5. In `App.js`, remove the logo import in line 2, and the header content in lines 8 - 21.
6. Change the functional component into class component, so you can add some state later on.
7. If creating a **front-end only** app, simply navigate into your app folder (`cd folder-name`) and `yarn start` to run the app and begin coding
8. If building a **full-stack app**, continue with the steps below

## Full Stack App Step by Step

1. Scaffold Express as above, and React steps 1-6
2. In `package.json` in your React app, add a proxy for the back end in line 34; `"proxy": "http://localhost:5000"`.
3. Back in the terminal, inside your React app, run `rm -rf .git` to avoid the folder being pushed to GitHub as a sub-module of your main repo.
4. In your Express app, create a new folder named `client`, and copy all the contents of your React app into this folder.
5. You have a full stack app! Happy coding!

## Git Collaboration Steps

### Option 1: Forks

1. Fork the repo
2. Clone it
3. In your terminal, run `git remote add upstream [url]` (original url)
4. Still in the terminal, run `git checkout -b staging`

**You will only need to do the first 4 steps the first time you clone the repo**

**The following steps are for your daily workflow:**

_Each time you need to work on some new stuff, make sure you pull latest things from upstream: This brings you up to date with the most recent version of the project. Run the following in your terminal_

5. `git pull --rebase staging` **(if there are merge errors, you will need to resolve them manually in VSCode before continuing. Always read the error message :) )**

   _Work on your stuff locally, then:_

6. `git add .`
7. `git commit -m "whatever"`
8. `git push origin staging` (You’re pushing to YOUR repository, not the upstream)
9. Create a new Pull Request (PR) in staging of your repo to original repo’s staging branch
10. Repeat the cycle from 5 - 9 ;)

### Option 2: Branches

1. Clone the repo
2. To work on a new feature, create a new branch with `git checkout -b feature-name`
3. Work on your feature
4. `git add .`
5. `git commit -m "whatever"`
6. `git push`
7. Create a new Pull Request (PR) on GitHub, from your branch to the main/development branch
8. Ideally, have another member of your team review that pull request. They can `git pull` and `git checkout feature-name` to review your code.
9. If the code is good, the PR can be accepted and merged on GH. You can optionally delete the branch after mergin (GitHub gives you that option)
10. If the code needs changes, you can request them in the PR, adding comments to it. The person responsible for that PR can commit new changes into their branch, which will be added automatically to the PR.
11. A common strategy is also to create **issues** on GH, and name your branches like `issue-14`, or `bug-14` or similar things.
