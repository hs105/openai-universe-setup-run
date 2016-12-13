# car-race-algo

Use one racing game provided by openAI Universe. 

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
has an error "Job for docker.service failed because the control process exited with error code. See "systemctl status docker.service" and "journalctl -xe" for details."
Do 
```
systemctl status docker.service
```
we see 
```
 docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: failed (Result: exit-code) since Mon 2016-12-12 16:36:06 PST; 1min 0s ago
     Docs: https://docs.docker.com
  Process: 5374 ExecStart=/usr/bin/dockerd -H fd:// (code=exited, status=1/FAILURE)
 Main PID: 5374 (code=exited, status=1/FAILURE)

Dec 12 16:36:06 hyao-linux systemd[1]: Starting Docker Application Container Engine...
Dec 12 16:36:06 hyao-linux dockerd[5374]: time="2016-12-12T16:36:06.530659363-08:00" level=fatal msg="Error starting daemon: pid file found, ensure docker is not running or delete /var/ru
Dec 12 16:36:06 hyao-linux systemd[1]: docker.service: Main process exited, code=exited, status=1/FAILURE
Dec 12 16:36:06 hyao-linux systemd[1]: Failed to start Docker Application Container Engine.
Dec 12 16:36:06 hyao-linux systemd[1]: docker.service: Unit entered failed state.
Dec 12 16:36:06 hyao-linux systemd[1]: docker.service: Failed with result 'exit-code'.
```

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




