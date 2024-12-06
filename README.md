# SHIELD: Assessing Security-by-Design in Federated Data Spaces using Attack Graphs

## Abstract

Federated data spaces relate to collaborative environments, where smart communities exchange messages for providing services, efficiency, and decision-making processes. The huge number of nowadays discovered vulnerabilities makes federated data spaces highly exposed to cyber attacks. Existing solutions to secure them focus on messaging protocol protection (e.g., using cryptographic means), but this is not enough. Attackers may exploit application and platform vulnerabilities to perpetrate detrimental circumstances (e.g., availability disruption of community services). To this aim, we propose SHIELD, a security-by-design solution for federated data spaces, which leverages attack graphs and trust computation to mitigate the risks posed by attacks exploiting vulnerabilities of devices in smart communities. Mitigation is accomplished by proactively assessing system weaknesses, and enabling security messaging measures before reaching detrimental attacks.
A prototype implementation of SHIELD using publish/subscribe as a messaging mechanism is experimentally evaluated over a real architecture in a V2X (Vehicle-to-Everything) scenario.

## Requirements

The following packages and libraries are required to run the simulation:

- networkx==3.3
- pandas==2.2.2
- matplotlib==3.8.4
- paho-mqtt==1.6.1
- nvdlib==0.7.6

You can install all the above packages with
`sudo pip3 install requirements.txt`

**Docker** is required which you can find [here](https://docs.docker.com/engine/install/ubuntu/).

**Mosquitto**: to install Mosquitto, run `sudo apt update -y && sudo apt install mosquitto mosquitto-clients -y`

We highly suggest using **Ubuntu** to facilitate reproducibility.

## Repository structure

In this repository you will find the following folders:

- **src**: contains all the source files to run the code.
- **data**: contains the inputs to reproduce the experiment. You can add your custom networks according to the JSON format present in this folder.
- **experiments**: contains the assessment output, including data and plots.

## Installation Instruction

### 1. Docker Network instantiation

1. Create a new folder in this location: `'/etc/mosquitto/<your_folder>/'` (you could create it everywhere but then you must change the Docker's volume location).

2. Paste there the Mosquitto configuration file that you can find in this repository (`src/srcEx/config/broker.conf`).

3. Make sure port 1883 is free by running `lsof -i :1883`, otherwise killing processes is required.

4. Run these commands to instantiate the Mosquitto broker:

- `sudo docker network create -d bridge mqttNetwork`

- `sudo docker pull eclipse-mosquitto`

- `sudo docker run -it -d --name broker -p 1883:1883 --network mqttNetwork -v /etc/mosquitto/<your_folder>/broker.conf:/mosquitto/config/mosquitto.conf eclipse-mosquitto`

5. (Optional) Check if everything worked smoothly by running `docker logs broker`, then you should find something like this:

```
mosquitto version 2.0.18 starting
Config loaded from /mosquitto/config/mosquitto.conf.
Opening ipv4 listen socket on port 1883.
mosquitto version 2.0.18 running
```

### 2. Run experiments

1. Open 2 terminals (one for subscribers, one for publishers)

2. Launch the following commands in the first terminal (for subscribers):

- `cd src/srcEx`
- `sudo python3 buildNet.py`

3. The terminal stays idle waiting for the other terminal to send messages (Subscriber service)

4. In the second terminal launch `sudo python3 src/main.py` and wait for the experiment to finish (you can customize the duration with the `td` variable, expressed in seconds).

5. The message `GRAPHS PRINTED, SUCCESS` indicates the successful completion of the experiment.

6. You can find the assessment results in `experiments/plot` folder.

## Cite this work

```
TBD
```
