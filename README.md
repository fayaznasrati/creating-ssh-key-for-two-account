# creating-ssh-key-for-two-account
# Step 1 - Create a New SSH Key

We need to generate a unique SSH key for our second GitHub account.
## ssh-keygen -t rsa -C "your-email-address"

Be careful that you don't over-write your existing key for your personal account. Instead, when prompted, save the file as id_rsa_YOUR-GITHUB-ACOUNT-NAME. In my case, I've saved the file to ~/.ssh/id_rsa_nettuts.

# Step 2 - Attach the New Key

Next, login to your second GitHub account, browse to "Account Overview," and attach the new key, within the "SSH Public Keys" section. To retrieve the value of the key that you just created, return to the Terminal, and type: 
vim ~/.ssh/id_rsa_YOUR-GITHUB-ACOUNT-NAME.pub. Copy the entire string that is displayed, and paste this into the GitHub textarea. Feel free to give it any title you wish.

Note: You might need to start ssh-agent before you run the ssh-add command: type eval `ssh-agent -s`

Next, because we saved our key with a unique name, we need to tell SSH about it. Within the Terminal,
 type: ssh-add ~/.ssh/id_rsa_YOUR-GITHUB-ACOUNT-NAME. If successful, you'll see a response of "Identity Added."

 # Step 3 - Create a Config File
 We've done the bulk of the workload; but now we need a way to specify when we wish to push to our personal account, and when we should instead push to YOUR-NEW-CREATED-GITHUB-ACOUNT-NAME . To do so, let's create a config file.

To create config file, Type:
 touch ~/.ssh/config
 vim config

 Note: If you're not comfortable with Vim, feel free to open it within any editor of your choice. Paste in the following snippet.
 
 #Default GitHub
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa


  This is the default setup for pushing to our personal GitHub account. Notice that we're able to attach an identity file to the host. Let's add another one for the company account. Directly below the code above, add:

  Host github-YOUR-GITHUB-ACOUNT-NAME
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_YOUR-GITHUB-ACOUNT-NAME

  This time, rather than setting the host to github.com, we've named it as github-YOUR-GITHUB-ACOUNT-NAME.
   The difference is that we're now attaching the new identity file that we created previously: YOUR-GITHUB-ACOUNT-NAME. Save the page and exit!
   # Step 4 - Try it Out

   It's time to see if our efforts were successful. Create a test directory, initialize git, and create your first commit.
on your git type:

git init
git commit -am "first commit'

Login to your YOUR-GITHUB-ACOUNT-NAME account, create a new repository, give it a name of "Test," and then return to the Terminal and push your git repo to GitHub


git remote add origin git@github-YOUR-GITHUB-ACOUNT-NAME:YOUR-GITHUB-ACOUNT-NAME/testing.git
git push origin master

## for Example main is:
git remote add origin git@github.com:fayaznasrati/test.git


Note that, this time, rather than pushing to git@github.com, we're using the custom host that we create in the
config file: git@github-YOUR-GITHUB-ACOUNT-NAME.

Return to GitHub, and you should now see your repository. Remember:

When pushing to your personal account, proceed as you always have.
For your YOUR-GITHUB-ACOUNT-NAME account, make sure that you use git!github-YOUR-GITHUB-ACOUNT-NAME as the host.
Be sure to refer to the screencast if you need a more visual overview of the steps above!

# Example
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github-fayaz_github:fayaznasrati/test.git
git push -u origin main




