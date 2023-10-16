# step by step fullnode 
 tutorial to boostsrap a fullnode on the avail kate testnet
Hey with this tutorial you can run an Avail full node step by step :
You need a Linux virtual machine 

1)setting up your environment :
Installation of the required dependencies:
sudo apt update && sudo apt upgrade -y
sudo apt install make clang pkg-config libssl-dev build-essential git screen protobuf-compiler -y

2)Installs Rust :
curl https://sh.rustup.rs -sSf | sh
Touch 1
Rust is installed, configure your current shell:
source $HOME/.cargo/env
Install nightly :
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
Check the rust version:
rustc —version

3)Clone the full node repository:
git clone https://github.com/availproject/avail.git

4)Client installation:
(There are two methods to run your full node but I recommend the second for a better monitoring)
First method:
cd avail
screen -S avail
cargo build --release -p data-avail
cargo build --release

5)Run the node
./target/release/data-avail --base-path `pwd`/data --chain kate --name patatedouce

Change “patatedouce” whit your node name before running your node

To check the node status go on the avail telemetry: http://telemetry.avail.tools/ your node will be appear on the site under the “node name”

Second method:
mkdir -p output
cargo run --locked --release -- --chain kate -d ./output

touch /etc/systemd/system/availd.service
nano /etc/systemd/system/availd.service

[Unit]
Description=Avail Validator
After=network.target
StartLimitIntervalSec=0
[Service]
User=root
ExecStart= /root/avail/target/release/data-avail --base-path `pwd`/data --chain kate --name "Dinhcongtac221"
Restart=always
RestartSec=120
[Install]
WantedBy=multi-user.target

Save it : Ctrl + x
To enable this to autostart on bootup run
systemctl enable availd.service
Start it manually with:
systemctl start availd.service
You can check that it's working with:
systemctl status availd.service
You can tail the logs with journalctllike so:
journalctl -f -u availd

S/o to Dihncongtac221 for the systemclt on the second method, he made to a guide for running a full node :

To check the node status go on the avail telemetry: http://telemetry.avail.tools/ your node will be appear on the site under the “node name”

Notable commands :
To exit the open window: (Ctrl + a + d)
To stop the log/node: (Ctrl +c)
Return on the window : screen -x
If you open multiple windows: screen -r and the window name
