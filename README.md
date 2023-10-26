# step by step  Avail fullnode 
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
Press 1,
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
git checkout v1.7.2
```
```
cargo build --release -p data-avail
```

![debut 11](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/8d8f5096-adaf-4115-b5e4-829c8c077a21)
![finis 2](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/77dcf3a6-c78b-4590-8249-6b06075af4ae)

final result

```
cargo build --release
```

![debut 1](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/61fc6b92-8091-4258-81fb-9dd1b7c9646b)
![finiiii](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/3c86c379-bc15-48fe-b2b9-87264bcda9b7)
final result

5)Run the node
```
./target/release/data-avail --base-path `pwd`/data --chain kate --name patatedoucetest
```

Change “patatedouce” with your node name before running your node
![oui](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/e183e399-6c1e-46f0-9b04-ad616c5d0a35)

To check the node status go on the avail telemetry: http://telemetry.avail.tools/ your node will be appearing on the site under the “node name”
![sync](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/d69df11f-54cd-4fe8-854d-a8a654e29311)
you should see your node syncing in grey like in the example

Second method:

```
mkdir -p output
mkdir -p data
git checkout v1.7.2
cargo run --locked --release -- --chain kate -d ./output
```
![hh](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/f3a366e3-8e5d-45fd-9a16-98e73f800bf2)

```
sudo touch /etc/systemd/system/availd.service
sudo nano /etc/systemd/system/availd.service
```
Copy this and paste it in the file, don’t forget to change the name “patatedouce” whit your name:

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
![syste](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/807fc945-be3b-43e5-a99c-0ff07d08e2b6)
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

![Capture d’écran 2023-10-16 232922](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/b4505035-f6fa-4b54-9bc5-d22819f86018)

check your node log:
```
journalctl -f -u availd
```

![log](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/48b64c7b-46c5-4fba-b7bd-ac1903f0c151)

If you wan to stop the node:
```
sudo systemctl stop availd.service
```

To check the node status go on the avail telemetry: http://telemetry.avail.tools/ your node will be appearing on the site under the “node name”
![sync](https://github.com/0xpatatedouce/step-by-step-availfullnode/assets/123324096/ee7f05aa-2ce9-44df-ad00-8c6878286c8b)
you should see your node syncing in grey like in the example

Some others guides:
https://github.com/0xrishitripathi/avail-anywhere/tree/main
https://github.com/DinhCongTac221/Install-Avail-Full-Node
https://youtu.be/HYBzK-jJIeQ



Notable commands :
To exit the open window: (Ctrl + a + d)
To stop the log/node: (Ctrl +c)
Return on the window : screen -x
If you open multiple windows: screen -r and the window name
