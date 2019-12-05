## Prerequisites

Please visit the [prerequisite installation instructions] (https://hyperledger-fabric.readthedocs.io/en/release-1.4/prereqs.html) to ensure you have the correct prerequisites installed. 
Since the fabric release version used is **1.4**, please use the version of that documentation to ensure alignment.

## Download Binaries and Docker Images

Clone the **fuzz-fabric-chaincode** repository and checkout the **develop** branch.
The repository has already been bootstrapped to include all the necessary binaries and docker images.

You can also download the script and execute locally, using the **bootstrap.sh** script in the **scripts** folder.

## Continuous Integration

Please have a look at [Continuous Integration Process](docs/fabric-samples-ci.md)

## License <a name="license"></a>

Hyperledger Project source code files are made available under the Apache
License, Version 2.0 (Apache-2.0), located in the [LICENSE](LICENSE) file.
Hyperledger Project documentation files are made available under the Creative
Commons Attribution 4.0 International License (CC-BY-4.0), available at http://creativecommons.org/licenses/by/4.0/.

## Build and start the network

The chaincodes are written in Golang and Node.js. You can find them with the respective languages in *chaincode/chaincode_example02* folder.
The fuzz code is present in the `invoke()` method of the two chaincodes.
Also, the network components are common to both the languages and are present in the **first-network** folder.

### Golang

Open a terminal and execute the following commands:

1. `cd first-network`

2. `./byfn.sh down`: to shut down the network (if up).

3. `./byfn.sh up`: to start the network.

The network components start spawning up after the above commands. 
The Golang chaincode contains an import statement for the go-fuzz library. Hence, keep track of when the CLI is container starts.
Once the CLI starts, open up another terminal, and execute:
4. `docker exec -it cli bash`: opens up the cli container.
5. `go get github.com/google/go-fuzz`

The bug can now be seen in the terminal where the network was bootstrapping.

### Node.js

Open a terminal and execute the following commands:

1. `cd first-network`

2. `./byfn.sh down`: to shut down the network (if up).

3. `./byfn.sh up -l node`: to start the network.

The network components start spawning up after the above commands.
No fuzz-library has been used here; rather, Math.random() fuzzes a variable, as can be seen in the this file, *chaincode/chaincode_example02/node/chaincode_example02.js*.

