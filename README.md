# car-race-algo

Use one racing game provided by openAI Universe. 

## Setup git account
* git config user.name "hs105"
* git config user.email "hengshuai@gmail.com"
* generate a ssh key for your account
```
ssh-keygen -t rsa -C "hengshuai@gmail.com"
```
you should select to overite your old one. 
* then add this to your github account. 

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
run bash in a docker
```
sudo docker run -it ubuntu bash
```

## Install Universe 
* Ubuntu 16.04
* create a conda environment:
* * conda create --name openai-universe python=3
* * source activate openai-universe
* * pip install gym
* * pip install universe

* [Docker](https://docs.docker.com/engine/installation/linux/ubuntulinux/) 
when importing Universe, it still has an error. Looks like docker is not started. Starting docker using
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
to quickly test whether the importing is Okay, do 
```
python -c "import gym; import universe"
```
No error. So the two modules are correctly installed. 






