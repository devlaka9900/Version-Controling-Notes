Resolving Merge Conflicts in GitHub Using Branches

1. Create and switch to a new Branch in GitHub repository:
    - Create a new repository called test-repo in GitHub.
    - Next navigate to Applications->Terminal Emulator and launch a new terminal.
    - Initialize the git repository by using the command below:
        # git init 
    - Next, navigate back to your GitHub repository and copy the URL of the repository which you want to clone to your local system.
    - Navigate to the terminal window which you had opened earlier, and clone your repository  by using the command
        #  git clone https://github,com/<your Github username>/<your GitHyb reponame>.git
    - Next, execute the command below to navigate to the local folder.
        # cd <your GitHub reponame>

2. Create a New Branch Locally 
    - Checkout to the repository's main branch  
        # git checkout main
    -  Create and switch to the new branch
        # git checkout -b feature/update-text

3. Edit the Text File Locally  
    - Create a new file sample.txt and add the line "Adding a new line" to  it.
        # echo "Adding  a  new line " > sample.txt
    - Add the changes and commit them
        # git add <your-text-file-name>
        # git commit -m "Updated text file with feature update"
    - You will be prompted to enter your Github user email and username to enable global Git configurations. Replace the placeholders in the command below with your GitHub email and username.
        # git config --global user.name "Your Name"
        # git config --global user.email "youremail@example.com"

4. Push the Changes to the New Branch  
    - Before pushing the changes  you need to create a Personal access token on your GitHub repository.
    - Steps create a Personal access token:
        > Navigate to your GitHub repository .
        > Select Settings  option under your profile to open the Settings webpage.
        > Click on Developer Settings
        > Next create a new Personal access classic token by enabling repo scope.Scroll down and click on the Generate Token button to create a new token.
        > Make sure to copy the personal access token as it will not accessible later.
    - Next navigate back to the terminal and execute the command below to push the changes to your GitHub branch.
    - You will be prompted to enter your username and password on execution. Enter your GitHub username and the provide the personal access token which you copied as the password.
        # git push origin feature/update-text
    - Your file will now be pushed to the branch feature/update-text.

5. Edit the File on the Main Branch via GitHub GUI  
    - Navigate to the GitHub repository in your browser.
    - Go to the main branch and create a new text file by the same name sample.txt  which is also present in the feature/update-text branch.
    - Click the pencil icon to edit the file. Make some manual changes directly in the file. 
        # Add a new line to main

    -  Commit the changes .Later click on Compare and pull Request button.
    -  Select feature/update-text as the source branch and main as the target branch. 
    -  Click Create Pull Request.  

6. Resolve the Merge Conflict  
    -  GitHub will detect the merge conflict in the text file.  
    -  Click on Resolve Conflicts.
        > You will see the conflicting changes highlighted:
        > Resolve the conflict by accepting the incoming changes from the branch:  
        > Click Mark as Resolved and then Commit Merge.

7. Complete the Pull Request
    - Return to the pull request page
    - Click Merge Pull Request to merge the changes into the main branch.  
    - You can then return back to the main branch to view the merged changes.






















    








 



