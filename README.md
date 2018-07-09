 # Documentation

## Requirements
Different branches of fabric-grabielle refer to different machines ( root ca ,  intermediate ca ect )  Ensure the content from each branch of the fabric-gabriele repository is in $GOPATH/src/github.com/hyperledger/ of the corresponding machine.




Both fabric & fabric-ca must also be cloned to $GOPATH/src/github.com/hyperledger/

## setup-fabric-network.sh

### Preface
For the intial simple case we concern ourselves with , we include only 1 organisation (BT) alongside the orderer. This leaves 5 components involved : 
* root ca 
* intermediate ca
* orderer
* peer
* run

![git](https://user-images.githubusercontent.com/40793810/42423385-3fb8cd68-82f1-11e8-84b5-5c111fea58e7.png)

Each of the above have a machine dedicated to them. We also have a separate machine which we will refer to as master ( since it corresponds to master branch) . setup-fabric-network.sh is to be run on this master machine. It is responsible for automizing the process of setting up each individual machine separately.

### Cleaning up
The first step is merely to access each machine in turn and remove the data folder from the local go/src/github.com/Fabric_Gabriele path . 

### setup procedure
Following the clean up procedure , the sequence of setups on each machine can occur. This begins with running the local start.sh script on the root ca machine. Then the data directory produced is copied to the next link in the sequence , namely the intermediate ca machine. This copying occurs via the master machine , in that the data folder is copied first to the master machine then from the master machine to the intermediate ca machine. This process is then repeated for each successive link in the sequence, ending with the start.sh being executed in the run machine. This is summarised in the diagram below.

![screen shot 2018-07-08 at 22 51 18](https://user-images.githubusercontent.com/40793810/42424268-8c796c74-8301-11e8-9bd9-2f4fee5345d6.png)


#### start.sh 
The start.sh script handles creating and running of relevant containers for each machine. This first involves deleting any previous docker containers and any existing chaincode images. The log folder is then created within the copied data directory.

![screen shot 2018-07-08 at 22 28 16](https://user-images.githubusercontent.com/40793810/42424366-01fdc188-8303-11e8-8e01-5f6336998dff.png)

The above is common to all machines. The next process is to create the appropriate docker compose files corresponding to each machine to allow the right containers to be run in each machine. This is handled by the make-docker.sh script . This script varies for each machine allowing accordingly different containers to be run on different machines.


