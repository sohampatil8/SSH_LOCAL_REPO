### Take access of github repository to your local machine (windows/git) to push your code at GitHub

#### Open Git Bash (or PowerShell) and run:
```
mkdir -p ~/.ssh
```
#### Loading the private key into the ssh-agent (id_rsa), adding the public key to GitHub (id_rsa.pub)
e.g : (id_rsa.pub OR id_rsa)
If the files doesn't exist then create this:
```
ssh-keygen  #Type Enter(default)
```
##### Copy your key files into ~/.ssh. If they are currently in Downloads
example: adjust path to where your files are
```
mv /c/Users/YourUser/Downloads/id_rsa.pub ~/.ssh/
mv /c/Users/YourUser/Downloads/id_rsa.pem ~/.ssh/
```
If the private key file is named id_rsa.pem, rename it to id_rsa
```
mv ~/.ssh/id_rsa.pem ~/.ssh/id_rsa
```

Set correct file permissions (important):
```
chmod 600 ~/.ssh/id_rsa         # private key: only owner read/write
chmod 644 ~/.ssh/id_rsa.pub     # public key: readable
```

#### Start and use the ssh-agent and add your private key
start the ssh-agent in the background
```
eval "$(ssh-agent -s)"
#add your key to the agent
ssh-add ~/.ssh/id_rsa
```
#### Using PowerShell (Windows 10/11 built-in OpenSSH)
```
# start and set service to automatic```
Set-Service -Name ssh-agent -StartupType Automatic
Start-Service ssh-agent
# add key (use full path)```
ssh-add $env:USERPROFILE\.ssh\id_rsa
```
#### Make sure your git remote uses SSH
```
# check remote
git remote -v
# If remote is HTTPS (like https://github.com/user/repo.git), change it to SSH:```
git remote set-url origin git@github.com:your-github-username/your-repo.git
```
#### Test the SSH connection to GitHub
```
ssh -T git@github.com
```
