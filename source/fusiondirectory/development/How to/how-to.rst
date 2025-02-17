=============================
How to Start Your Development Journey
=============================

This guide will help you get started with development within our GitLab environment.
It covers account creation, issue reporting, branch creation, and submitting a Merge Request (MR).

------------------------------
1. Create a GitLab Account
------------------------------

1. Go to our GitLab instance: `<insert_gitlab_url_here>`
2. Click on **Register** or **Sign In** if you already have an account.
3. Follow the registration process, and once your account is active, sign in.
4. Ensure you have the necessary permissions to access projects. If not, request access from an administrator.

------------------------------
2. Select a Project
------------------------------

1. After logging into GitLab, click on **Projects** in the top navigation bar.
2. Select **"Explore Projects"** or **"Your Projects"** to find the relevant repository.
3. Most developments take place in the **plugins** section, so navigate there if applicable.

------------------------------
3. Create an Issue
------------------------------

To report a new feature or a bug, follow these steps:

1. Navigate to the **Issues** section within the selected project:
   - In the project repository, click on **Issues** in the left sidebar.
   - Click on the **New Issue** button.

2. Fill in the issue details:
   - **Title**: A short and clear summary of the issue.
   - **Description**: Provide a detailed explanation of the issue or feature request.
   - **Template**: Use the available issue template and ensure all sections are completed properly.

3. Click **Submit Issue** to create it.

------------------------------
4. Create a New Branch
------------------------------

When you create an issue, you should also create a branch for your development:

1. Open the newly created issue.
2. In the right-hand sidebar, locate the **"Create merge request"** button and click on it.
3. A dialog will appear:
   - Keep the source branch name descriptive (e.g., `feature-new-plugin` or `fix-bug-xyz`).
   - The target branch should be the project's development branch (e.g., `develop`).
   - Check **"Start a new merge request"** to begin tracking progress.
4. Click **Create Branch**.

------------------------------
5. Checkout Your Branch Locally
------------------------------

Once the branch is created, you can start developing:

1. Open your terminal and navigate to your local repository.
2. Run the following command to fetch the latest changes:

