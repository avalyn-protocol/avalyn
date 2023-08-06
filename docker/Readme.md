# Docker container
## How to build
Inside the avalyn root directory, execute
```
docker build -t avalyn -f docker/Dockerfile .
```

## How to use
To run the daemon, use
```
docker run -it avalyn
```

In order to use the avalyn wallet cli, you can use
```
docker run -it avalyn avalyn-wallet-cli
```

## Docker compose example
This example runs 2 daemons for HA and a avalyn wallet rpc with the specified keys
```
version: '3.7'

networks:
  net:
    driver: overlay
    driver_opts:
      encrypted: ''
    attachable: true
    
volumes:
  blockchain:
    name: 'blockchain-{{.Task.Slot}}'
    
services:
  avalyn_daemon:
    image: avalyn
    command: ["avalynd", "--p2p-bind-ip=0.0.0.0", "--p2p-bind-port=43730", "--rpc-bind-ip=0.0.0.0", "--rpc-bind-port=43731", "--non-interactive", "--confirm-external-bind", "--restricted-rpc"]
    volumes:
      - blockchain:/root/.avalyn
    networks:
      - net
    ports:
     - target: 43730
       published: 43730
       protocol: tcp
       mode: ingress
     - target: 43731
       published: 43731
       protocol: tcp
       mode: ingress
    deploy:
      replicas: 2
      update_config:
        parallelism: 1
        delay: 10s
  wallet:
    image: avalyn
    command: ["avalyn-wallet-rpc", "--wallet-file", "funding", "--password", "", "--daemon-host", "avalyn_daemon_avalyn_daemon", "--rpc-bind-port", "11182", "--disable-rpc-login", "--rpc-bind-ip=0.0.0.0", "--confirm-external-bind"]
    volumes:
      - ./wallet.keys:/funding.keys
      - ./wallet.cache:/funding.cache
    networks:
      - net
```
