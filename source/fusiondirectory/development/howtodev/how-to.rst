========================
Your Development Journey
========================

This guide will help you get started with development within our GitLab environment.
It covers account creation, issue creation, project forking, and submitting a Merge Request (MR).

-----------------------------------
1. Create a FusionDirectory Account
-----------------------------------

We have a fully automated process to grant you the necessary permissions for contributing to our projects.

Follow the link below to register:
`https://iam.fusiondirectory.org/publicform.php?form=register`

Once registered, go to our GitLab instance: `https://gitlab.fusiondirectory.org/` to log in and access projects.

------------------------------
2. Select and Fork a Project
------------------------------

1. After logging into GitLab, click **Projects** in the top navigation bar.

   .. note::
      The default project is **FusionDirectory**, located here:
      `https://gitlab.fusiondirectory.org/fusiondirectory/`

2. Click **"Explore Projects"** to browse available repositories or **"Your Projects"** to view assigned projects.
3. Most development work occurs in the **fd-plugins** section, so navigate there if applicable.
4. In the top-right corner of the project page, click **Fork Project**. This will create a copy of the full project within your namespace.

   .. image:: images/ForkFdPlugins.png

5. Select the project URL, ensuring your username is included, as shown in the example below. You may change the **Project Slug**, but we recommend leaving it unchanged.

   .. image:: images/ForkFdPlugins2.png

6. Click **Fork Project**.

You will be automatically redirected to your own space, where you can now modify the project and create your first Merge Request.

------------------------------
3. Create a Development Branch
------------------------------

Now, let's create a **new merge request** for your forked project.

1. Go to the **Merge Requests** section in the left sidebar and click **"New Merge Request"**.

   .. image:: images/NewMergeRequest.png

2. On the new page, ensure the settings are correct:

   - **Source project**: Your personal fork (`[username]/[project-name]`)
   - **Target project**: The original repository (`fusiondirectory/[project-name]`)

   .. image:: images/MergeRequestFromTo.png

   Click **Compare Branch and Continue**.

3. In the dialog that appears:

   - Leave the branch name as suggested. We recommend using the same branch name as the issue title.
   - Ensure the target branch is the development branch (e.g., `dev`).

   .. image:: images/FromTo.png

4. Fill in the optional fields:

   - **Assignee**: Assign the MR to yourself.
   - **Reviewer**: Assign another contributor or a FusionDirectory developer as a reviewer.
   - **Milestone**: Select a milestone if applicable.
   - **Labels**: These will be set automatically—leave them unchanged.
   - **Merge options**:

     - Select **"Delete source branch when merge request is accepted"**, which is the default setting.

   .. image:: images/MergeRequestOptions.png

5. Click **Create Merge Request** to begin tracking progress.

-------------------------------
4. Checkout Your Branch Locally
-------------------------------

Once the branch is created, you can start development.

1. Click the **Code** button in the top-right corner of the page.
2. Click **Check out branch** to view checkout instructions.

   .. image:: images/Checkout.png

3. Copy the provided Git command and execute it in your local repository to switch to your branch.

   .. note::
      Ensure your new branch is available locally. If not, clone your forked repository before running the above command.

----------------------------------------
5. Create an Issue on the Origin Project
----------------------------------------

Once you have completed your development and your merge request is ready, you need to create an issue on the original project.

1. Navigate to the **Issues** section of the original project:

   - In the project repository, click **Issues** in the left sidebar.
   - Click the **New Issue** button.

2. Fill in the issue details:

   - **Title**: Provide a concise and clear summary of the issue.
   - **Description**: Explain the issue or feature request in detail, including expected behavior.
   - **Template**: Use the available issue template and ensure all sections are completed correctly.

3. In the **Description**, make sure to link your Merge Request from your personal fork.
This allows the FusionDirectory developers to review your code and integrate it into the original codebase.

4. Click **Submit Issue** to create it.

---

That's it!
We look forward to your contributions and innovations!
