# geant-4-docker
Simplified [Geant4](https://geant4.web.cern.ch/) usage with a Docker container derived from a [Ubuntu 18.04 ROOT](https://cloud.docker.com/repository/docker/smflment/root-docker) container. The [image is hosted on DockerHub](https://cloud.docker.com/repository/docker/smflment/geant4)

Docker can be installed following the instructions on the [Docker homepage](https://docs.docker.com/install/linux/docker-ce/ubuntu/). The Docker image can also be used very well to build a [Singularity container](https://www.sylabs.io/singularity/) from it. Tested on [CentOS7](https://www.centos.org/) with [Singularity 3.2](https://github.com/sylabs/singularity) successfully with graphics support wihtout the need for passing further flags.

## Usage

To run the container, simply call
```
docker run -it --rm --name geant4_container smflment/geant4:10.5.1 bash
```
Options:
- ``` -it ```: Keep bash open after invoking
- ``` --rm ```: Delete container when stopping. Remove this option if you want to keep your container for more than one session
- ``` --name geant4_container```: Name for your container.

### GUI

To use the GUI, you need to pass X11 information. From Linux you can run the container using
```
docker run -it --rm --ipc=host --net=host \
           -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix \
           -v "$HOME/.Xauthority:/root/.Xauthority:rw" \
           --name geant4_container \
           smflment/geant4:10.5.1 bash
```
### Run example

A simple test can be performed using a simple example within the container:
```
cp -r $G4EXAMPLES/basic/B1 ./ && cd B1/ && mkdir build && cd build && cmake ../ && make && ./exampleB1
```

## Bare image (currently not available)

The bare image comes without examples and datasets. You will need to download them yourself in that case and provide them using a volume adding the option
```
-v path/to/unpacked/datasets:/usr/local/geant4/share/Geant4-10.5.1/data
```

- [G4NDL.4.5](https://cern.ch/geant4-data/datasets/G4NDL.4.5.tar.gz)
- [G4EMLOW.7.7](https://cern.ch/geant4-data/datasets/G4EMLOW.7.7.tar.gz)
- [G4PhotonEvaporation.5.3](https://cern.ch/geant4-data/datasets/G4PhotonEvaporation.5.3.tar.gz)
- [G4RadioactiveDecay.5.3](https://cern.ch/geant4-data/datasets/G4RadioactiveDecay.5.3.tar.gz)
- [G4PARTICLEXS.1.1](https://cern.ch/geant4-data/datasets/G4PARTICLEXS.1.1.tar.gz)
- [G4PII.1.3](https://cern.ch/geant4-data/datasets/G4PII.1.3.tar.gz)
- [G4RealSurface.2.1.1](https://cern.ch/geant4-data/datasets/G4RealSurface.2.1.1.tar.gz)
- [G4SAIDDATA.2.0](https://cern.ch/geant4-data/datasets/G4SAIDDATA.2.0.tar.gz)
- [G4ABLA.3.1](https://cern.ch/geant4-data/datasets/G4ABLA.3.1.tar.gz)
- [G4INCL.1.0](https://cern.ch/geant4-data/datasets/G4INCL.1.0.tar.gz)
- [G4ENSDFSTATE.2.2](https://cern.ch/geant4-data/datasets/G4ENSDFSTATE.2.2.tar.gz)

Download shortcut:
```
wget https://cern.ch/geant4-data/datasets/G4NDL.4.5.tar.gz \
     https://cern.ch/geant4-data/datasets/G4EMLOW.7.7.tar.gz \
     https://cern.ch/geant4-data/datasets/G4PhotonEvaporation.5.3.tar.gz \
     https://cern.ch/geant4-data/datasets/G4RadioactiveDecay.5.3.tar.gz \
     https://cern.ch/geant4-data/datasets/G4PARTICLEXS.1.1.tar.gz \
     https://cern.ch/geant4-data/datasets/G4PII.1.3.tar.gz \
     https://cern.ch/geant4-data/datasets/G4RealSurface.2.1.1.tar.gz \
     https://cern.ch/geant4-data/datasets/G4SAIDDATA.2.0.tar.gz \
     https://cern.ch/geant4-data/datasets/G4ABLA.3.1.tar.gz \
     https://cern.ch/geant4-data/datasets/G4INCL.1.0.tar.gz \
     https://cern.ch/geant4-data/datasets/G4ENSDFSTATE.2.2.tar.gz
```

           
