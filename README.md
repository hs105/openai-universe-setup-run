# car-race-algo

Use one racing game provided by openAI Universe. 

## Setup git account
* git config --global user.name "hs105"
* git config --global user.email "hengshuai@gmail.com"
* generate a ssh key for your account
```
ssh-keygen -t rsa -C "hengshuai@gmail.com"
```
you should select to overite your old one. 
* then add the public key to your github account. 
```
cat ~/.ssh/id_rsa.pub
```
copy and paste to GitHub Setting SSH Key. 

## Install Docker
* prerequisites: [follow here](https://docs.docker.com/engine/installation/linux/ubuntulinux/#/install-the-latest-version)   
* [install the latest version of docker](https://docs.docker.com/engine/installation/linux/ubuntulinux/#/install-the-latest-version)
* test if it's working
```
sudo docker ps
```
If you do without "sudo", it will say:
```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```
Another test: run bash in a docker
```
sudo docker run -it ubuntu bash
```
The last step is to add the currrent user to the docker group. This is important because by default docker is only run with sudo users. 
```
sudo usermod -aG docker $USER
```
If you don't do this, you will later see permission errors with Universe. 

## Install Universe 
OS: Ubuntu 16.04

### create a conda environment:
* conda create --name openai-universe python=3
* source activate openai-universe
* pip install gym
* pip install universe

### Install [Docker](https://docs.docker.com/engine/installation/linux/ubuntulinux/) 

## Start docker 
Run on command line
```
sudo service docker start
```
It will have no output. To check status, do
```
systemctl status docker.service
```
then it shows
```
Dec 13 14:54:26 hyao-linux systemd[1]: Started Docker Application Container Engi
```
docker started successfully. 

## Test
to quickly test whether Unviverse is installed correctly, do 
```
python -c "import gym; import universe"
```
No error. So it is correctly installed!

## DustDrive on Universe
```
import gym
import universe  # register the universe environments

env = gym.make('flashgames.DuskDrive-v0')
env.configure(remotes=1)  # automatically creates a local docker container
observation_n = env.reset()

while True:
  action_n = [[('KeyEvent', 'ArrowUp', True)] for ob in observation_n]  # your agent here
  observation_n, reward_n, done_n, info = env.step(action_n)
  env.render()
```







