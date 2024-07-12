# Cross-distro communication experiments

Build the containers by `cd`ing into the jazzy/iron/humble directory and running `./build.sh`

To start the action & service servers, run
```bash
docker compose --profile ${SERVER_DISTRO} up
```
where `SERVER_DISTRO` is one of `jazzy`, `iron`, or `humble`.

To start the client, run

```bash
docker compose --profile client up
```

To connect to the client to send action goals/call the server run
```bash
docker compose ls
```
and look for the UUID of the client container:
```
CONTAINER ID   IMAGE                     COMMAND       CREATED          STATUS         PORTS     NAMES
01b02f0bc464   jazzy-experiment:latest   "/bin/bash"   11 minutes ago   Up 3 seconds             docker_experiment-client-1
```
then run
```bash
docker exec -it 01b02f0bc464 bash
```
replacing the container ID as necessary.

To send action goals:
```bash
source /ros_entrypoint.sh
ros2 action send_goal /fibonacci action_tutorials_interfaces/action/Fibonacci  'order: 5' --feedback
```

To call services:
```bash
source /ros_entrypoint.sh
ros2 service call /add_two_ints example_interfaces/srv/AddTwoInts '{"a": 314, "b": 2718}'
```
