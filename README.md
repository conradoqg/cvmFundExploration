# meajudafi-workers

Background workers of the [meajudafi](https://github.com/conradoqg/meajudafi-stack) stack.

## Available workers

- cvmDataWorker: Download, extract and insert CVM funds list, indicators data into database;
- cvmStatisticWorker: Calculate a wide range of statistics of the CVM funds including investment return, sharpe, consistency, risk, and so on;
- dataImprovementWorker: Improves and unify data gathered from the sources, does a great job on funds name's and non oficial data like initial investment, quota limits and so on;
- xpiFundWorker: Download, cleanup and extract data from XPI broker;
- btgPactualFundWorker: Download, cleanup and extract data from BTG Pactual broker;
- migrateWorker: Migrates the database;
- all: Run all the above workers except `migrateWorker`;

## Usage

```sh
$ git clone https://github.com/conradoqg/meajudafi-workers.git
$ cd meajudafi-workers
$ npm install
$ node ./bin/cvmfe.js run <worker> <options>
```

## Related repositories

- [meajudafi-stack](https://github.com/conradoqg/meajudafi-stack)
- [meajudafi-front-end](https://github.com/conradoqg/meajudafi-front-end)
- [meajudafi-docker-container-crontab](https://github.com/conradoqg/meajudafi-docker-container-crontab)

## Troubleshooting
Fixing 15 minutes connection broken when using Docker Swarm:

```
$ docker run --net=host --ipc=host --uts=host --pid=host -it --security-opt=seccomp=unconfined --privileged --rm -v /:/host alpine /bin/sh

$ chroot /host

$ echo "net.ipv4.tcp_keepalive_time = 600" >> /etc/sysctl.d/00-alpine.conf
$ echo "net.ipv4.tcp_keepalive_intvl = 30" >> /etc/sysctl.d/00-alpine.conf
$ echo "net.ipv4.tcp_keepalive_probes = 10" >> /etc/sysctl.d/00-alpine.conf

$ sysctl -p /etc/sysctl.d/00-alpine.conf

or

$ docker run --net=host --ipc=host --uts=host --pid=host -it --security-opt=seccomp=unconfined --privileged --rm -v /:/host alpine /bin/sh -c "chroot /host && echo \"net.ipv4.tcp_keepalive_time = 600\" >> /etc/sysctl.d/00-alpine.conf && echo \"net.ipv4.tcp_keepalive_intvl = 30\" >> /etc/sysctl.d/00-alpine.conf && echo "net.ipv4.tcp_keepalive_probes = 10" >> /etc/sysctl.d/00-alpine.conf && sysctl -p /etc/sysctl.d/00-alpine.conf"

or change this settings on sysctl.conf

net.ipv4.tcp_keepalive_time=300
net.ipv4.tcp_keepalive_intvl=30
net.ipv4.tcp_keepalive_probes=10
```

License
----
This project is licensed under the [MIT](LICENSE.md) License.
