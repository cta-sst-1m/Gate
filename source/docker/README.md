# GateDocker
Gate Docker scripts, Generate the image by running the `Generate.sh` script

# First Image Geant4
## Docker for gate prerequisites

[optional if not done before]
`systemctl start docker`
login: `docker login`

[build and use]
* build: 
    * `docker build -t opengatecollaboration/geant4:11.0.0 -f DockerFileGeant --build-arg ROOT_Version=v6-24-06 --build-arg Geant4_Version=v11.0.0 .`
* push: 
    * `docker push opengatecollaboration/geant4:$version`
* interactive: 
    * `docker run -it --rm -v $PWD:/APP opengatecollaboration/geant4:$version /bin/bash`

Where: 

* `$version` is `11.0.0` for gate `9.2`

# Second image Gate
## Docker for gate

[optional if not done before]
`systemctl start docker`
login: `docker login`

[build and use]
* build: 
    * `docker build -t opengatecollaboration/gate:9.2 -f DockerFileGate --build-arg Geant4_Version=opengatecollaboration/geant4:11.0.0 --build-arg Gate_Version=v9.2 .`
* push:  
    * `docker push opengatecollaboration/gate:$version`
* run command:  
    * `docker run -i --rm -v $PWD:/APP opengatecollaboration/gate:$version mac/main.mac`
* interactive:  
    * `docker run -it --rm -v $PWD:/APP --entrypoint /bin/bash opengatecollaboration/gate:$version`

You can just install docker and then create an alias in your configuration
* ```echo "alias Gate='docker run -i --rm -v $PWD:/APP opengatecollaboration/gate:$version'" >> ~/.bashrc```

Where: 
* `$version=9.2`
