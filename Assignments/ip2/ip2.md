---
layout: assignment
title: "Individual Project 2"
permalink: /assignments/ip2
parent: Assignments
nav_order: 2
due_date: "Wednesday Febraury 4, 2026 11:00am (EST)"
submission_notes: Submit through Github Classroom (Commit your work in main branch) and link on Gradescope
---

Welcome back to the Game Nite team! In this second deliverable, you will be implementing new and exciting features to enhance the frontend interface and bring the web application to life. This assignment builds on the foundation you laid in the first project and will deepen your skills in frontend development with TypeScript and React.

The objectives of this assignment are to:

- Investigate and understand a large, existing codebase
- Implement interactive web applications with the React library
- (Optional). Learn to comprehend and work with larger scope tests.

## Changelog
- NA


## 1. Getting Started

Start by accepting our [GitHub Classroom Invitation] TODO TODO XXX TODO. It will create a Github repository for you which will include the starter code for this assignment. Run `npm install` in the root directory to fetch all dependencies for the `client`, `server`, and `shared` folders. 

### 1.1 Optional but Recommended: MongoDB

It can be quite a bit easier to work on the application if restarting the server doesn't reset the entire application to an initial state. 

This codebase has a proper repository layer, which connects to MongoDB through an adapter library called [Keyv] TODO TODO XXX TODO TUTORIAL. You can install MongoDB on your local machine.

1. Follow the [instructions in the official MongoDB documentation](https://www.mongodb.com/docs/manual/administration/install-community/) to install the free community edition.
2. Choose 'Install on Linux', 'Install on macOS', or 'Install on Windows', depending on your system. (the following steps are for Windows)
3. Scroll down to the section labeled 'Install MongoDB Community Edition.' and click on [MongoDB Download Center](https://www.mongodb.com/try/download/community?tck=docs_server).
4. For Windows, in the Package dropdown, select `msi`. Then download and run the installer.
5. On Windows, select the _“Install MongoDB as a Service”_ checkbox and install. This will start MongoDB as a background service.
6. Install "MongoDB Compass" if prompted.
7. Verify if the MongoDB server is running using the Windows Services app.

Mongo offers several methods of interacting with your Mongo databases.

- MongoDB Compass is an interactive application for creating, modifying, and querying MongoDB connections. It should be started as part of the installation process, showing a connection to `mongodb://localhost:27017/`.

  For Windows, install MongoDB Compass using the instructions above.

  For Mac:

  - Download the dmg file from https://www.mongodb.com/try/download/compass. Once the application starts:
    1.  Click on "Add new connection" in the left sidebar.
    2.  Make sure the URI field contains `mongodb://localhost:27017`
    3.  Click on "Connect" - MongoDB will need to be running as a macOS service

- Mongo shell (_mongosh_) provides a command-line interface that can be used to interact with databases in MongoDB.

  For Windows:

  - Download it [here](https://www.mongodb.com/try/download/shell) using the msi package. You can also use _mongosh_ to see if the MongoDB server is running. Try the MongoDB Community Edition and the command `show dbs`; you should see a list of existing databases in your local instance.

  For Mac:

  - Mongo shell is automatically installed with MongoDB through the Mac installation instructions. To use it, make sure MongoDB is running as a macOS service, then type `mongosh` into the terminal.

### 1.2 Setting Up the Server To Use MongoDB

Create a file called `server/.env` — the dot before the "env" is important! Include the following text:

```
MONGODB_STR=mongodb://127.0.0.1:27017
```

This tells your server how to connect to the local MongoDB instance that you got running in the previous step. Now, you can start the application as before: in one terminal, run:

```
ip2-me $> npm run dev -w=server
```

Leaving that running, open another terminal and run:

```
ip2-me $> npm run dev -w=client
```

## 2. Project Submission

You will submit your code by pushing the final version into your repository (add/commit/push). In this assignment, you should only be making, committing, and pushing changes to the `main` branch of your repository. Be sure to check if the correct version is submitted before the deadline.

On Gradescope, you will submit a plain `.txt` file containing two things:

 1. The link to your project's GitHub repo (e.g. `https://github.com/neu-cs4530/ip2-robsimmons`)
 2. The written responses and cURL commands requested in Task 3.

We will grade your code on GitHub by using the "Feedback" PR that is automatically created when the assignment is. The Feedback PR can be found under the "Pull requests" menu, like this:

![image]({{site.baseurl}}{% link /Assignments/ip1/github-pr.png %})

If you don't see your Feedback PR for the assignment, let us know on Piazza (be sure include your GitHub username).

Grades will be assigned on Gradescope and synced to the Canvas Gradebook.

### TypeScript ESLint, Vitest, and Configuration Files

The GitHub project contains a number of configuration files you **may not modify**: `package.json`, `package-lock.json`, `.prettierrc`, `tsconfig.json`, `vitest.config.mjs`, and `vite.config.mjs` are configuration files, as is everything in the `.github` directory. If you change any of these files, take care to change them back; the list of changes in the feedback PR should not show any changes to these files. You also may not include `eslint-disable` commands to disable ESLint's checks in your final submission.

The code you submit must pass GitHub's automatic checks, which mostly just amount to the TypeScript typechecker, the ESLint linter, and the tests. You can run these yourself like this:

```
ip1-me $> npm run check --workspaces
ip1-me $> npm run lint --workspaces
ip1-me $> npm run test --workspaces
```

When you push your code to GitHub, you can see the status icon for your most recent submission. It's initially a yellow circle, like this:

![image]({{site.baseurl}}{% link /Assignments/ip1/github-ci.png %})

After the tests run, this will turn into a red ❌ or a green ✅. Clicking on the icon will let you see details of the tests we ran.

The Actions tab on GitHub has the results of previous runs.

![image]({{site.baseurl}}{% link /Assignments/ip1/ActionsTab.png %})

**Up to 25% of your total grade on the assignment may be deducted for CI failures (5% for prettier failures, 10% for TypeScript failures, and 10% for ESLint failures). In severe cases we may decline to grade your assignment entirely. Give yourself sufficient time to find and fix any errors.** ESLint _warnings_ do not cause CI to fail will not automatically lead to a deduction, but it is bad practice to have lots of console statements in your code, and this can lead to a point deduction if it makes it hard for a TA to understand your code.

## 3. Implementation Tasks

### Task 1: Navigating to Other Profiles

Currently, going to the "Profile" link at the top of your page takes you to the path `/profile/<yourusername>`. Change `client/src/components/MessageList.tsx` so that clicking on the users' display name in chat takes you to `/profile/<theirusername>`. For example, if you are logged in as `user0` and you see a chat message from Yāo, that should be a `<NavLink>` that takes you to `/profile/user1`. 

This task is worth 10 points, based on checking that chat navigation works as expected.

### Task 2: Viewing Other Profiles

Change `client/src/pages/Profile.tsx` so that, you are logged in as `user0` and navigate to `/profile/user1`, you see a page that allows you to see _but not edit_ that user’s username, display name, and when their account was created.

You may want to split this file into two or three new files, since the route to profile pages is now being used for two different purposes: viewing your own profile, and editing other profiles.

This task is worth 25 points:
 - 10 points will be based on functionality.
 - 15 points will be based on appropriately refactoring your code into multiple files with appropriate [code style]({{ site.baseurl }}{% link style.md %}).

### Task 3: More Profile Navigation

The code you changed in Task 1 was only one place where user display names were referenced. Here are some others:

 - The "(DisplayName) entered chat/left chat" messages in chat
 - The "Player #2 is (DisplayName)" messages in the game panel
 - "Posted by (DisplayName)" in forum messages
 - "Reply by (DisplayName)" in forum comments
 - "(Display name) created 1 day ago" on the home page and the game list and forum list pages

For this task, you'll make three changes to all display name locations:

 - Consistently refer to the current logged-in user by the second-person pronoun "you," instead of by their display name. (The exception is the "signed in as (DisplayName)" message in the header — leave that alone.)
 - Create a consistent visual style for distinguishing references to "you," the current logged-in user, and references to other users.
 - Consistently link other users' usernames to their profile. References to the current user should not link to their profile.

This task is worth 15 points: one point for each of the three changes in each of the five places where display names occur. You should make this task easier on yourself by thinking about how to organizing your code in a way that minimizes duplication, and unnecessary duplication may lead to a deduction of up to 5 points.

### Task 4: Mine Finder

The backend has been implemented for Mine Finder, a game with a strong but legally-permissible resemblance to Microsoft's [Minesweeper](https://apps.microsoft.com/detail/9wzdncrfhwcn?hl=en-US&gl=US) game.

In Mine Finder, your game starts with a 6x6 or 7x5 grid containing six randomly-placed mines. Clicking on a grid position sweeps it, revealing how many of the eight adjacent grid positions contain mines — or exploding and ending the game if there is a mine in that positions! When a grid position is revealed to have zero mines, all eight adjacent grid positions are automatically swept.

The backend logic for Mine Finder 


### Task 5: Marking Mines

### Task 6: Mine Difficulty





After you have done this, profile links will appear in chat messages. You can also 

Your own messages 

 use MongoDB as the NoSQL database to store data related to this application.


You should not install any additional dependencies: **'package.json' must be unchanged**. You should also not delete the **package-lock.json** file.

{: .note }
**Note:** You may see warnings about vulnerabilities after running npm install. These should be ignored. Do NOT run `npm audit fix` or `npm audit fix --force` as this will change your package-lock.json file. 

{: .note }
Refer to [IP1](https://neu-se.github.io/CS4530-Fall-2025/assignments/ip1) for instructions related to setting up MongoDB, setting environment variables, and running the client and server.

{: .note }
**System-level dependencies:** The libraries used for React require some native binaries to be installed -- code written and compiled for your computer (not JavaScript). If you run into issues with `npm install` not succeeding, please try installing the following libraries using either [Homebrew (if on Mac)](https://brew.sh), apt-get, or your favorite other package manager: `pixman`, `cairo`, `pkgconfig` and `pango`. For example, on a Mac, after installing Homebrew, run `brew install pixman cairo pkgconfig pango`. **You should not continue with the installation until this succeeds.** On Windows: Students have reported seeing the failure `error /bin/bash: node: command not found` upon `npm install` in the `client` directory. If you encounter this error, please try to delete the `node_modules` directory and re-run `npm install` in the `client` directory from a bash shell instead of a windows command prompt.

These are some convenience scripts that you can use while working on the assignment:

1. `npm run dev` (client + server) - This can be used to start the client or server in the respective directory the command is run. Both the client and server will reload every time a file is saved, reflecting any changes live.
2. `npm run debug-test` (server)- This runs the test command with coverage.
3. `npm run lint` (client + server) - This can be used check style errors in both client and server. Note the client starter code has lint errors you are expected to fix. Don't fix them immediately as some of the errors are due to hints provided in the starter code, which will be helpful to complete the implementation tasks. In fact, you can run lint to and inspect the errors to figure out the hints.
4. Make you sure the MongoDB process `mongod` is running. You can check this by running `mongosh`. If this isn't running then the client won't be able to connect to the database through the server.

## Implementation Tasks

This deliverable has 2 parts; each part will be graded by its own rubric provided in the "Grading" section. You're recommended to complete this assignment one task at a time, in the order provided. For this assignment, follow test-driven development (TDD). Read the tests in the server to understand how the server endpoints are expected to behave and use that understanding to inform the implementation of the client. Do **not** change the provided server tests to match your implmentation. The repository README also documents the server endpoints.

The client implementation has a service layer in `services`. Review the existing code in that layer to understand how the 
client interacts with the server endpoints. You will need to create your own client service for the implementation tasks.

### Task 1: Collections Frontend Implementation (90 points)

In IP1, you implemented the backend functionality for Collections. In this task, you will build the frontend components to allow users to interact with collections through the user interface.

#### Steps to Achieve This

##### In Client


**Create `useAllCollectionsPage` custom hook**

Create a new file `./client/src/hooks/useAllCollectionsPage.ts`. In this file, you will implement the `useAllCollectionsPage` custom hook, which manages the state and logic for displaying all collections belonging to a user. The hook should fetch collections when the component mounts using the `getAllCollectionsByUsername` service function and handle loading states.

**Complete the `AllCollectionsPage` component**

In `./client/src/components/main/collections/allCollectionsPage/index.tsx`, update the component to use the `useAllCollectionsPage` hook. Implement state management using the `useAllCollectionsPage` hook. Use the returned values from the hook to display the collections list.

**Create `useCollectionPage` custom hook**

Create a new file `./client/src/hooks/useCollectionPage.ts`. This hook manages the state for viewing a single collection, including fetching the collection details by ID and handling real-time updates via socket events sent from the server.

**Complete the `CollectionPage` component**

In `./client/src/components/main/collections/collectionPage/index.tsx`, use the `useCollectionPage` hook for state management.

**Create `useDeleteCollectionButton` custom hook**

Create a new file `./client/src/hooks/useDeleteCollectionButton.ts`. Implement logic for deleting a collection with confirmation handling.

**Complete the `DeleteCollectionButton` component**

In `./client/src/components/main/collections/deleteCollectionButton/index.tsx`, create a button component that handles collection deletion. Use the `useDeleteCollectionButton` hook for the deletion logic.

**Create `useNewCollectionPage` custom hook**

Create a new file `./client/src/hooks/useNewCollectionPage.ts`. Implement the hook to manage form state for creating a new collection. Create a `postCollection` function within this hook that validates inputs and submits using the `createCollection` service.

**Complete the `NewCollectionPage` component**

In `./client/src/components/main/collections/newCollectionPage/index.tsx`, create the form for adding a new collection. Use the `useNewCollectionPage` hook. Implement state management using the `useNewCollectionPage` hook.

**Create `useSaveToCollectionModal` custom hook**

Create a new file `./client/src/hooks/useSaveToCollectionModal.ts`. This hook manages the modal state for saving questions to collections, including fetching user collections and toggling question membership.

**Complete the `SaveToCollectionModal` component**

In `./client/src/components/main/collections/saveToCollectionModal/index.tsx`, implement the modal that allows users to save/unsave questions to their collections. Display checkboxes for each collection showing current save status.

**Update the menu in the sidebar to render collection of a username**

Review the code in `src/components/main/sideBarNav/index.tsx`. Verify that the route for collections is setup correctly to render the collections for a particular username.

**Implement collection service functions**

In `./client/src/services/collectionService.ts`, implement the following service functions:

- `getAllCollectionsByUsername`: Fetches all collections for a user
  - The getAllCollectionsByUsername function retrieves all collections for a specific user with proper authorization. Make a GET request using api.get(). The usernameToView is a path parameter, while currentUsername is a query parameter for permissions. Check for status 200 and throw "Error when fetching all collections" if it fails. Return res.data, containing an array of PopulatedDatabaseCollection objects.

- `getCollectionById`: Fetches a single collection by ID
  - The getCollectionById function fetches a single collection by ID with user authorization. Use api.get(), where the collectionId is specified as the path parameter and the username is included as the query parameter. Verify status 200 and throw "Error when fetching collection" on failure. Return res.data with the PopulatedDatabaseCollection object.

- `createCollection`: Creates a new collection
  - The createCollection function creates a new collection by sending a POST request with the collection object as the request body. Use api.post() to send the request and check if the response status is 200; if it is not, throw an error with the message "Error when creating collection." Return res.data containing the created collection object.

- `deleteCollection`: Deletes a collection
  - The deleteCollection function permanently removes a collection with user verification. Use api.delete() with collectionId as a path parameter and username as a query parameter. The request URL should be formatted as `/api/collection/delete/${collectionId}?username=${username}`. Verify status 200 and throw "Error when deleting collection" on failure. Return res.data with the deletion confirmation.

- `toggleSaveQuestion`: Adds or removes a question from a collection
  - The toggleSaveQuestion function adds or removes questions from collections using toggle logic. Send a PATCH request using api.patch(), passing { collectionId, questionId, username } as the request body. Check for status 200 and throw "Error when toggling save question" if failed. Return res.data with the operation result.


**Create a Save to an Existing Collection Button in Question Component**

In `.client/src/components/main/questionPage/question/index.tsx`, add a button that opens the modal to save a question to an existing collection.The button must have the className='collections-btn'. Clicking this button should  open the modal, which will allow the user to add a question to one of its collections.



#### Grading (90 points)

- `useAllCollectionsPage` hook = 8 points
- `AllCollectionsPage` component = 8 points
- `useCollectionPage` hook = 10 points
- `CollectionPage` component = 6 points
- `useDeleteCollectionButton` hook = 5 points
- `DeleteCollectionButton` component = 3 points
- `useNewCollectionPage` hook = 8 points
- `NewCollectionPage` component = 5 points
- `useSaveToCollectionModal` hook = 7 points
- `SaveToCollectionModal` component = 15 points
- Collection service functions = 15 points

### Task 2: Communities Frontend Implementation (90 points)

In IP1, you implemented the backend functionality for Communities. In this task, you will build the frontend components to allow users to interact with communities through the user interface.

#### Steps to Achieve This

##### In Client

**Create `useAllCommunitiesPage` custom hook**

Create a new file `./client/src/hooks/useAllCommunitiesPage.ts`. This hook manages the state for displaying all communities. It should fetch communities using the getCommunities service function and handle updates to existing communities.

**Complete the `AllCommunitiesPage` component**

In `./client/src/components/main/communities/allCommunitiesPage/index.tsx`, we've defined a component to display all communities. Update the component to use the `useAllCommunitiesPage` hook. Implement state management using the `useAllCommunitiesPage` hook.

**Create `useCommunityCard` custom hook**

Create a new file `./client/src/hooks/useCommunityCard.ts`. This hook manages the render logic to display all communities. Private communities cannot be viewed by non members.

**Complete the `CommunityCard` component**

In `./client/src/components/main/communities/communityCard/index.tsx`, implement the component to display community information. Use the `useCommunityCard` hook for state management.

**Create `useCommunityMembershipButton` custom hook**

Create a new file `./client/src/hooks/useCommunityMembershipButton.ts`. This hook manages the join/leave functionality for communities.

**Complete the `CommunityMembershipButton` component**

In `./client/src/components/main/communities/communityMembershipButton/index.tsx`, create a button that handles joining and leaving communities. Use the `useCommunityMembershipButton` hook.

**Create `useCommunityPage` custom hook**

Create a new file `./client/src/hooks/useCommunityPage.ts`. Implement the hook to manage state for viewing a single community, including fetching community details and handling real-time updates.

**Complete the `CommunityPage` component**

In `./client/src/components/main/communities/communityPage/index.tsx`, implement the component to display community details and members. Use the `useCommunityPage` hook.

**Create `useNewCommunityButton` custom hook**

Create a new file `./client/src/hooks/useNewCommunityButton.ts`. Implement logic for showing the new community creation button.

**Complete the `NewCommunityButton` component**

In `./client/src/components/main/communities/newCommunityButton/index.tsx`, create a button component that navigates to the new community page.

**Create `useNewCommunityPage` custom hook**

Create a new file `./client/src/hooks/useNewCommunityPage.ts`. Implement the hook to manage form state for creating communities. Create a `postCommunity` function within this hook that validates inputs and submits using the `createCommunity` service.

**Complete the `NewCommunityPage` component**

In `./client/src/components/main/communities/newCommunityPage/index.tsx`, create the form for adding a new community. Use the `useNewCommunityPage` hook for state management.

**Implement community service functions**

In `./client/src/services/communityService.ts`, implement the following service functions:

- `getCommunityById`: Retrieves a single community by ID
  - The getCommunityById function fetches one community using its ID. Use api.get() with the communityId as a path parameter. Verify the response status is 200; otherwise, throw "Error when fetching community". Return res.data as a DatabaseCommunity object.
- `getCommunities`: Retrieves all communities
  - The getCommunities function returns the full list of communities. Make a GET request with api.get(). Check for status 200 and throw "Error when fetching all communities" if it fails. Return res.data, which should be an array of DatabaseCommunity objects.
- `changeCommunityMembership`: Toggles user membership in a community
- The changeCommunityMembership function adds or removes a user from a community using toggle logic. Send a POST request via api.post()  with { communityId, username } in the request body. Confirm status 200; if not, throw "Error while changing community membership". Return res.data containing the updated community.
- `createCommunity`: Creates a new community
  - The createCommunity function creates a community by sending a POST request with the new Community object as the request body using api.post() to an endpoint. Ensure the response status is 200; otherwise throw "Error when creating community". Return res.data containing the created DatabaseCommunity.
- `deleteCommunity`: Deletes a community
  - The deleteCommunity function removes a community permanently by ID. Use api.delete() with the communityId as a path parameter. Verify status 200; if it fails, throw "Error when deleting community". Return res.data with the deletion confirmation or result.

#### Points to note

- The client starter code has lint errors which you are expected to fix. They will go away when you implement the hints.
- Run the server and the client and render the client in the browser to get a sense of the user interface.
- Do not change the classNames of React components in the starter code. We will use the classNames in automated tests.

#### Grading (90 points)

- `useAllCommunitiesPage` hook = 10 points
- `AllCommunitiesPage` component = 8 points
- `useCommunityCard` hook = 4 points
- `CommunityCard` component = 5 points
- `useCommunityMembershipButton` hook = 4 points
- `CommunityMembershipButton` component = 4 points
- `useCommunityPage` hook = 8 points
- `CommunityPage` component = 12 points
- `useNewCommunityButton` hook = 3 points
- `NewCommunityButton` component = 2 points
- `useNewCommunityPage` hook = 9 points
- `NewCommunityPage` component = 6 points
- Community service functions = 15 points


## Submission Instructions & Grading

You will submit your code by pushing the final version into your repository thru Github Classroom (add/commit/push). **All commits must be visible on the main branch on GitHub classroom to receive credit.** Be sure to check if the correct version is submitted before the deadline. On Gradescope, you will submit a plain .txt file containing

This submission will be scored out of 200 points, 180 of which will be awarded for implementation of tasks and accompanying tests, and the remaining 20 for following style guidelines.

Your code will automatically be evaluated for linter errors and warnings.

- Each lint error or warning will result in a deduction of -2 points (up to a maximum of 30 points).
- This will not affect the 20 style points.
- Line endings will not be counted as errors.

The starter code comes with some lint problems, You are expected you to fix these linter problems, many of them will be fixed as you implement the tasks.

**The use of `eslint-disable` statements is NOT allowed. Each instance outside what is provided in the starter code will have points deducted.**

You can run the following command within the client or server to fix some common lint errors

```
npm run lint:fix
```

#### Testing

You will be provided with starter code that includes a set of tests. Your task is to ensure that all existing tests pass and to create additional tests to cover any new functionality or edge cases in the server. You do not need to write Jest tests for socket code in the server (e.g. `socket.emit` statements in `collection.controller.ts` or `community.controller.ts`). However, you will be able to identify if it's working correctly by interacting with the frontend client.

You do not need to write automated tests for the frontend, but are encouraged to extensively manually test your implementation.
##### Cypress Tests

**Please Note -  Running Cypress tests is optional. Cypress tests require significant system resources, and without them, the tests may be flaky. We will run similar (not the same) tests for grading.**

The Cypress tests (located in the `testing/` directory) are provided as an example of GUI and end-to-end (E2E) tests. They can be used to check the correctness of your implementation, but **you are not expected to write** Cypress tests. Please see the README for full instructions on running the Cypress tests.

##### Running the Cypress tests (optional)

These are end-to-end (E2E) tests and are provided to help validate the existing features. Follow the steps below to set up and run them.

1. Install dependencies for the tests
```bash
cd testing
npm install
```
2.Create the .env file used by the tests
```bash
# in the testing/ directory create a .env file containing:
MONGODB_URI=mongodb://127.0.0.1:27017
```
3. Start the server and client
4. Open the Cypress UI
```bash
# from the testing/ directory
npx cypress open
```
5. Run tests via the Cypress UI
- choose "e2e testing", then click Start, and click any test file to run it


### Manual Grading

Your code will be manually evaluated for conformance to our [course style guide](https://neu-se.github.io/CS4530-Spring-2026/policies/style/). **Do not wait to run the linter until the last minute**. To check for linter errors, run the command `npm run lint` from the terminal. The handout contains the same ESlint configuration that is used by our grading script.

This manual evaluation will account for 10% of your total grade on this assignment. We will manually evaluate your code for style on the following rubric:

To receive all 20 points:

- All new names (e.g. for local variables, methods, and properties) follow the naming conventions defined in our style guide
- There are no unused local variables
- All public properties and methods (other than getters, setters, and constructors) are documented with JSDoc-style comments that describe what the property/method does, as defined in our style guide
- The code and tests that you write generally follows the design principles discussed in week one. In particular, your design does not have duplicated code that could have been refactored into a shared method.
- No duplicate code is allowed.

We will review your code and note each violation of this rubric. We will deduct 4 points for each violation, up to a maximum of deducting all 20 style points.

#### GitHub Actions for Test and Lint Output

Once your submission is pushed to your main branch, GitHub will automatically run linting and the tests in `server/tests` for your submission. Check the Actions tab on GitHub classroom to see the output of the run. This output will be used for grading, so ensure there are no errors in the Actions run.

![image]({{site.baseurl}}{% link /Assignments/ip1/ActionsTab.png %})


#### Debugging

If you need help troubleshooting a problem, be sure to follow all the steps outlined in the course's [debugging policy]({{ site.baseurl }}{% link debugging.md %}). This will ensure you have exhausted all initial debugging strategies before reaching out for assistance from the TAs.

### Academic Integrity

Please refer to the [course policy page](https://neu-se.github.io/CS4530-Spring-2026/policies/#academic-integrity) for more details.

**For this assignment, the use of autocomplete tools or generative AI technologies such as ChatGPT is not allowed.**