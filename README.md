# Knowledge-graph-storage-on-filecoin

<p align="center">
    <img src="https://www.datalatte.com/imgs/datalatte.svg">
</p>
<p align="center">
    <a href="https://github.com/datalatte-ai/Knowledge-graph-storage-on-filecoin/graphs/contributors" alt="Contributors">
        <img src="https://img.shields.io/github/contributors/datalatte-ai/Knowledge-graph-storage-on-filecoin" /></a>
    <a href="https://github.com/datalatte-ai/Knowledge-graph-storage-on-filecoin/pulse" alt="Activity">
        <img src="https://img.shields.io/github/commit-activity/m/datalatte-ai/Knowledge-graph-storage-on-filecoin" /></a>
    <a href="https://discord.com/invite/saUmuZ3Rrw">
        <img src="https://img.shields.io/discord/308323056592486420?logo=discord"
            alt="chat on Discord"></a>
    <a href="https://twitter.com/intent/follow?screen_name=DATALATTE_">
        <img src="https://img.shields.io/twitter/follow/DATALATTE_?style=social&logo=twitter"
            alt="follow on Twitter"></a>
</p>
### Filecoin Storage
Filecoin is a decentralized storage network that allows users to buy and sell storage space in a secure and trustless manner. It uses a novel blockchain-based mechanism to incentivize users to provide storage to the network, and allows them to earn rewards in the form of the network's native cryptocurrency, also called Filecoin. The goal of Filecoin is to provide a more secure, scalable, and transparent alternative to existing centralized storage solutions.

### Lotus node
This sounds like a simple question; what is Lotus? And the surface-level answer is:
![alt text](https://lotus.filecoin.io/lotus/get-started/what-is-lotus/High-Level-Lotus-Suite_hu46f9931703ca6917a3d49082bcb430a7_87466_800x0_resize_box_3.png)

Lotus is a command-line application that lets you interact with Filecoin. You can do this by uploading and downloading files, renting out your storage to other users, and checking that computers are storing data correctly.

Now, let's run a lotus node to have access to file storage and retrieval.
There are two methods for installing Lotus on Linux: AppImage and Snap. We chose the second method, Snap, and I should note that we were using Ubuntu.

we have to take afew steps before runing lotus node :
1. Update and upgrade your system:
```
sudo apt update -y && sudo apt upgrade -y
```
2. Install Lotus using Snap, run:
```
sudo snap install lotus
```
### System-specific
Building Lotus requires some system dependencies, usually provided by your distribution.

Ubuntu/Debian:
```
sudo apt install mesa-opencl-icd ocl-icd-opencl-dev gcc /
git bzr jq pkg-config curl clang build-essential hwloc /
libhwloc-dev wget -y && sudo apt upgrade -y
```
### Rustup
Lotus need rustup, The easiest way to install it is:
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
### Go
To build Lotus, you need working installation of Go 1.19.4 or higher:
```
wget -c https://golang.org/dl/go1.19.4.linux-amd64.tar.gz -O - | sudo tar -xz -C /usr/local
```


You’ll need to add /usr/local/go/bin to your path. For most Linux distributions you can run something like:
```
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc && source ~/.bashrc
```
See the official Golang installation instructions if you get stuck.


### Run a Lotus lite-node
Once all the dependencies are installed, you can build and install Lotus.

1. Clone the repository:
```
git clone https://github.com/filecoin-project/lotus.git
cd lotus/
```
2. Swtich to the lated stable release branch:
```
git checkout releases
```
3. Build and install Lotus on Calibration testnet:
```
make clean calibnet # Calibration with min 32GiB sectors
sudo make install
```
Now you can check lotus version:
```
lotus --version
```
you should be able to see your lotus version after runing that.

4. Install daemon:
```
make install-daemon-service
make install-miner-service
```
5. Now you are good to run lotus:
```
lotus daemon 
```
Make sure that you open another terminal in order to interact with the lotus.
6. You should wait for the node to sync with the chain:
```
lotus sync wait
```
When you enter the sync command, you will see the message "Done!" When it's finished, your node will be synced and you may begin stroing data.
### Get a FIL address
1. Open a new terminal window and enter an address using the lotus:
```
lotus wallet list
```
```
t14cdn74fvwcniq5b3y7fbwmh4adrq5akjowwh73a
```
2. You can use the following command to view the wallet address and balance:
```
list wallet list
```
```                                                                
Address                                    Balance   Nonce  Default  
t14cdn74fvwcniq5b3y7fbwmh4adrq5akjowwh73a  0 FIL     0      X  
```

3. Use `lotus wallet export` to export your private key, replacing `f1...` with your public key:

```
lotus wallet export f1... > my_address.key
```

### Adding FIL to your wallet using calibration faucet
After copying your public address, go to https://faucet.calibration.fildev.network to receive FIL.
Now you should wait for your request to be confirmed, and after it is, if your node is synced, enter 'lotus wallet list' you will notice that your balance has increased to 200 FIL.
```
Address                                    Balance     Nonce  Default  
t14cdn74fvwcniq5b3y7fbwmh4adrq5akjowwh73a  200 FIL     0      X 
```
## knowledge graph
Before we go into storing data on Filecoin, let's speak about knowledge graphs, which is what we'll be storing on Filecoin storage.

A knowledge graph is a structured representation of real-world entities and their relationships. It is a way to organize and connect data in a way that allows for easy access and understanding of complex information.

One advantage of storing a knowledge graph on a decentralized storage system is that it allows for greater accessibility and scalability. Decentralized systems do not rely on a central server or authority, which means that the knowledge graph can be accessed from anywhere with an internet connection. This is particularly useful when the knowledge graph is large and complex, as it allows for more efficient querying and retrieval of information.

Another advantage of storing a knowledge graph on a decentralized system is that it can increase the security and integrity of the data.

Overall, storing a knowledge graph on a decentralized storage system can provide greater accessibility, scalability, and security for the data. It is an effective way to store and manage complex information and can be a valuable tool for organizations and individuals seeking to make sense of large amounts of data.

To move forward with Filecoin storage, we want to create a knowledge graph based on the [happiness survey](https://happiness-survey.com/).

Let's have a look at the structure of the knowledge graph.

![alt text](https://github.com/Alihszh/Knowledge-graph-storage-on-filecoin/blob/main/Knowledge_graph_data_model-2_page-0001.jpg)

![alt text](https://github.com/Alihszh/Knowledge-graph-storage-on-filecoin/blob/main/Knowledge_graph_data_model-2_page-0002.jpg)

![alt text](https://github.com/Alihszh/Knowledge-graph-storage-on-filecoin/blob/main/Knowledge_graph_data_model-2_page-0003.jpg)

![alt text](https://github.com/Alihszh/Knowledge-graph-storage-on-filecoin/blob/main/Knowledge_graph_data_model-2_page-0004.jpg)


### Storing data on filecoin
1. First, choose a miner:
```
lotus client list-asks
```
You should see a list of miners like this: 
```
.. getting miner list
* Found 64 miners with power
.. querying asks
* Queried 14 asks, got 12 responses
t02133: min:256 B max:32 GiB price:0 FIL/GiB/Epoch verifiedPrice:0 FIL/GiB/Epoch ping:479.870292ms protos:
t01584: min:2 MiB max:32 GiB price:0 FIL/GiB/Epoch verifiedPrice:0 FIL/GiB/Epoch ping:660.963027ms protos:
t01588: min:256 B max:32 GiB price:0.0000000005 FIL/GiB/Epoch verifiedPrice:0.00000000005 FIL/GiB/Epoch ping:556.94495ms protos:
t01235: min:256 B max:32 GiB price:0.0000000005 FIL/GiB/Epoch verifiedPrice:0.00000000005 FIL/GiB/Epoch ping:632.022959ms protos:
t03351: min:256 B max:32 GiB price:0.0000000005 FIL/GiB/Epoch verifiedPrice:0.00000000005 FIL/GiB/Epoch ping:664.910486ms protos:
t01750: min:256 B max:64 GiB price:0.0000000005 FIL/GiB/Epoch verifiedPrice:0.00000000005 FIL/GiB/Epoch ping:810.881221ms protos:
t01990: min:256 B max:32 GiB price:0.0000000005 FIL/GiB/Epoch verifiedPrice:0.00000000005 FIL/GiB/Epoch ping:884.028678ms protos:
t01718: min:256 B max:32 GiB price:0.0000000005 FIL/GiB/Epoch verifiedPrice:0.00000000005 FIL/GiB/Epoch ping:345.768699ms protos:
t01231: min:256 B max:32 GiB price:0.0000000005 FIL/GiB/Epoch verifiedPrice:0.00000000005 FIL/GiB/Epoch ping:571.478234ms protos:
t01035: min:256 B max:32 GiB price:0.0000000005 FIL/GiB/Epoch verifiedPrice:0.00000000005 FIL/GiB/Epoch ping:673.214057ms protos:
t02255: min:256 B max:32 GiB price:0.0000000005 FIL/GiB/Epoch verifiedPrice:0.00000000005 FIL/GiB/Epoch ping:671.735297ms protos:
t01591: min:256 B max:32 GiB price:0.0000000005 FIL/GiB/Epoch verifiedPrice:0.00000000005 FIL/GiB/Epoch ping:714.858919ms protos:
```
2. Choose a miner and write down the miner ID, for example. I'd like to work with the first miner, whose ID is 't02133'.
3. Import your file:
```
lotus client import 
```

