# step by step fullnode 
 tutorial to boostsrap a fullnode on the avail kate testnet
Hey with this tutorial you can run an Avail full node step by step :
You need a Linux virtual machine 

1)setting up your environment :
Installation of the required dependencies:
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install make clang pkg-config libssl-dev build-essential git screen protobuf-compiler -y
```

2)Installs Rust :
```
curl https://sh.rustup.rs -sSf | sh
```
Press 1
Rust is installed, configure your current shell:
```
source $HOME/.cargo/env
```
Install nightly :
```
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```
Check the rust version:
```
rustc —version
```

3)Clone the full node repository:
```
git clone https://github.com/availproject/avail.git
```

4)Client installation:
(There are two methods to run your full node but I recommend the second for a better monitoring)

First method:
```
cd avail
screen -S avail
```
```
cargo build --release -p data-avail
```

![debut 11](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/3ea7b4ab-999f-4c52-aab7-cc8295e7a416)
![finis 2](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/ef51ac27-7356-4083-b2d7-4a443ee132c0)
final result

```
cargo build --release
```

![debut 1](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/0c5a9a8e-a293-4403-84c2-871bdd664799)
![finiiii](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/2549c312-e40a-4270-869c-723438c888ee)
final result

5)Run the node
```
./target/release/data-avail --base-path `pwd`/data --chain kate --name patatedoucetest
```

Change “patatedouce” whit your node name before running your node
the output 
![oui](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/74d9d6bc-eadd-4483-8c84-048160a8cfcd)

To check the node status go on the avail telemetry: http://telemetry.avail.tools/ your node will be appear on the site under the “node name”
![sync](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/63db3495-3bc1-40e8-a0fd-16424849ace0)
you should be see your node syncing in grey like in the example

Second method:

```
mkdir -p output
cargo run --locked --release -- --chain kate -d ./output
```

```
sudo touch /etc/systemd/system/availd.service
sudo nano /etc/systemd/system/availd.service
```

![syste](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/782ff328-88d0-42aa-a145-4857bdfc375b)

```
[Unit]
Description=Avail Validator
After=network.target
StartLimitIntervalSec=0
[Service]
User=root
ExecStart= /root/avail/target/release/data-avail --base-path `pwd`/data --chain kate --name "patatedoucetest"
Restart=always
RestartSec=120
[Install]
WantedBy=multi-user.target
```

Ctrl+x press y to save the file and enter to exit

To enable your file:
```
sudo systemctl enable availd.service
```

Start the node:
```
sudo systemctl start availd.service
```

You can check the status:
```
sudo systemctl status availd.service
```





To check the node status go on the avail telemetry: http://telemetry.avail.tools/ your node will be appear on the site under the “node name”
![sync](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/ac9463d1-6257-436b-b461-f7d03848caf3)

S/o to Dihncongtac221 for the systemclt setup on the second method, he did a guide and a video for running a full node :
https://github.com/DinhCongTac221/Install-Avail-Full-Node
https://youtu.be/HYBzK-jJIeQ



Notable commands :
To exit the open window: (Ctrl + a + d)
To stop the log/node: (Ctrl +c)
Return on the window : screen -x
If you open multiple windows: screen -r and the window name
