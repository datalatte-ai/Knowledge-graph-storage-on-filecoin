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
