### Creating a pull request via the command line for Windows users can be done using two methods: with the GitHub CLI or without it. I'll guide you through both processes.

### Method 1: **Using GitHub CLI**

The GitHub CLI (`gh`) simplifies the process of creating pull requests directly from the command line.

#### **Step-by-Step Guide with GitHub CLI**

1. **Install GitHub CLI**:
   Download and install GitHub CLI from the official website:

   - Go to [GitHub CLI releases page](https://github.com/cli/cli/releases).
   - Download the latest Windows installer and run it.

2. **Authenticate GitHub CLI**:
   After installing, open Command Prompt or PowerShell and run:

   ```bash
   gh auth login
   ```

   Follow the instructions to log in to your GitHub account.

3. **Navigate to Your Repository**:
   Change to the directory of the repository where you want to create a pull request:

   ```bash
   cd path/to/your/repo
   ```

4. **Create a New Branch**:
   Create a new branch for your changes:

   ```bash
   git checkout -b my-feature-branch
   ```

5. **Make Changes and Commit**:
   After making your changes, stage and commit them:

   ```bash
   git add .
   git commit -m "Description of your changes"
   ```

6. **Push Your Changes to GitHub**:
   Push the changes to the new branch:

   ```bash
   git push origin my-feature-branch
   ```

7. **Create a Pull Request**:
   Use the GitHub CLI to create a pull request:
   ```bash
   gh pr create --base main --head my-feature-branch --title "Pull Request Title" --body "Description of the changes"
   ```
   This will open a new pull request, and you can view or manage it from the GitHub website.

### Method 2: **Without GitHub CLI**

If you don't want to install GitHub CLI, you can still create a pull request using just Git and the GitHub web interface. You'll initiate the process from the command line and finish it on GitHub.

#### **Step-by-Step Guide Without GitHub CLI**

1. **Install Git**:
   If you haven't installed Git yet, you can download it from [git-scm.com](https://git-scm.com/). During the installation, ensure Git Bash is selected for command-line use.

2. **Navigate to Your Repository**:
   Open Git Bash or Command Prompt and navigate to your repository:

   ```bash
   cd path/to/your/repo
   ```

3. **Create a New Branch**:
   Create and switch to a new branch:

   ```bash
   git checkout -b my-feature-branch
   ```

4. **Make Changes and Commit**:
   Stage and commit your changes:

   ```bash
   git add .
   git commit -m "Description of your changes"
   ```

5. **Push the New Branch to GitHub**:
   Push your branch to the remote repository:

   ```bash
   git push origin my-feature-branch
   ```

6. **Create the Pull Request via GitHub Website**:
   - Go to your repository on GitHub (e.g., `https://github.com/yourusername/yourrepo`).
   - You should see a prompt saying “Compare & pull request” for your newly pushed branch.
   - Click on “Compare & pull request”.
   - Fill in the necessary details (title, description) and submit the pull request.

### Summary

- **GitHub CLI** simplifies the process, but it's not necessary.
- **Without GitHub CLI**, you can push the branch from the command line and create the pull request using the GitHub web interface.

Both methods work fine; the CLI just saves a few steps and allows the entire process from the terminal.
