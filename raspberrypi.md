# RaspberryPi

1. Install docker

        curl -sSL https://get.docker.com | sh

# Notes:

Fix locale issue:

        sudo locale-gen en_GB en_US en_GB.UTF-8 en_US.UTF-8

wpa_supplicant.conf

        country=VN
        ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
        update_config=1

        network={

        ssid="Inspectorio"
        psk="Inspectorio@2017"
        key_mgmt=WPA-PSK
        }
	
ssh

open the config.txt file and add those lines bellow to config HDMI 7inch

        max_usb_current=1
        hdmi_group=2
        hdmi_mode=1
        hdmi_mode=87
        hdmi_cvt 1024 600 60 6 0 0 0

        sudo apt-get purge openssh-server
        sudo apt-get install openssh-server

Ensure SSH starts by default in the future
       
        sudo systemctl enable ssh

set timezone

        sudo cp -vf /usr/share/zoneinfo/Asia/Ho_Chi_Minh /etc/localtime

list all connection in LAN in Window

        arp -a

edit hostname

        sudo nano /etc/hostname
        sudo nano /etc/hosts

mosquitto

        sudo apt-get install mosquitto mosquitto-clients
        mosquitto_sub -h 192.168.200.25 -t sensor
        mosquitto_pub -h 192.168.200.25 -t sensor -m "test"

go

        apt-get install golang

check volumes

        df -h

mdns setup

        sudo apt-get install avahi-daemon

paho-mqtt

        sudo pip install paho-mqtt

elasticsearch

        sudo pip install elasticsearch

tmux

        tmux
        crtl+b then d to leave/detach tmux
        crtl+b then $ to name session
        tmux attach -t session_name
        tmux list-session	to list all session
        tmux kill-session -t session_name

systemd - make service on rasp

        http://www.diegoacuna.me/how-to-run-a-script-as-a-service-in-raspberry-pi-raspbian-jessie/
        https://www.freedesktop.org/software/systemd/man/systemd.service.html
	
    counter.py
        
        #!/usr/bin/python
        from time import sleep
        count = 0
        try:
                while True:
                        count += 1
                        print("\tWait for 5s...(%d)" % count)
                        sleep(5)
        except KeyboardInterrupt, e:
                print("Stopping...")
	
    /lib/systemd/system/counter.service
        
		[Unit]
		Description=My Counter
		After=multi-user.target

		[Service]
		WorkingDirectory=/home/pi/
		User=root
		Type=simple
		ExecStart=/usr/bin/python -u /home/pi/testfol/counter.py
		StandardOutput=journal+console
		Restart=always

		[Install]
		WantedBy=multi-user.target

        sudo chmod 644 /lib/systemd/system/counter.service
        chmod +x /home/pi/testfol/counter.py
        sudo systemctl daemon-reload
        sudo systemctl enable counter.service
        sudo systemctl start counter.service
        sudo systemctl status counter.service
        sudo systemctl stop counter.service
        systemctl list-units --type=service
        sudo journalctl -f -u counter.service

dhcp renew ip

        Type ifconfig to show the current IP address that you received from DHCP.
        Type dhcpcd -k to send the appropriate signals to dhcpcd.

change Keyboard

        sudo raspi-config
                Choose Internationalization menu
                - Choose keyboard setup menu.
                - If your exact keyboard is not on the list then choose one of the generic 101, 102 or 104 keyboards.
                The following steps are Important! If need US then you must choose US. Don't leave it set to UK.......
                - The default Keyboard Layout is [ English (UK) ]
                - You may need to scroll down and select [Other] to get back to the country of origin menu
                - From country of origin menu select [English (US) ]
                - Then from Keyboard layout: menu, scroll to top of list and select - [ English (US) ]. Do not choose anything else unless you know exactly what you are doing!
                - Complete the other menus then reboot.

Connect to wifi

        sudo iwlist wlan0 scan
        sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
                network={
                        ssid="testing"
                        psk="testingPassword"
                }
        wpa_cli -i wlan0 reconfigure
        ifconfig wlan0
