# learncpp
My repo for saving the things while learning cpp

## Git initialization

```bash
git config --global user.name "Your name"
git config --global user.email "Your_email@gmail.com"

ssh-keygen -t rsa -b 4096 -C "Your_email@gmail.com"

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id-rsa

cat ~/.ssh/id-rsa.pub
```

Copy and paste the SSH key to github by going to the Github SSH Settings. You need to check the SSH connection by 

```bash
ssh -T git@github.com
```

## Getting started with Visual Studio Code

Install VS code, then

```bash
sudo apt-get update
sudo apt-get install build-essential gdb

```

