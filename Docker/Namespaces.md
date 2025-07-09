get the process id of a specific container
```bash
docker inspect -f '{{.State.Pid}}' container-name
```

Running commands of different namesapces in the context of a specific container
```bash
sudo nsenter --target conatiner-PID -n <command here>
```

E.g.
```bash
sudo nsenter --target $(docker inspect -f '{{.State.Pid}}' container-name) -n netstat -tunalp
```