# Containers


## Portainer
```shell
docker volume create portainer_data
docker run -d -p 32125:8000 -p 32126:9443 --name portainer --restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
-v portainer_data:/data portainer/portainer-ce:latest
```

## Ubuntu container
```shell
#as your normal user
cd 
cd puppet-7
cd puppet-agent/ubuntu  # go to the relevant directory
docker build -t puppet-agent-ubuntu .  # build the image
docker run -d --name target1 --add-host puppet:<internal_ip> puppet-agent-ubuntu # enter puppetmaster internal ip address 
docker ps # Check
# Check /etc/hosts using portainer
puppet agent -t  # check 
```

## Almalinux container
```shell
cd puppet-agent/almalinux  # go to the relevant directory
docker build -t puppet-agent-almalinux .  # build the image
docker run -d --name target2 --add-host puppet:<internal_ip> puppet-agent-almalinux # enter puppetmaster internal ip address 
# Check /etc/hosts using Portainer
puppet agent -t  # check 
```

## Signed all certificates
As root outside containers, on your VM
```shell
/opt/puppetlabs/bin/puppetserver ca sign -a # list all current certificats
```

**Go to FIRST_MANIFESTS.md**