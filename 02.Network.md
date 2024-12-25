- Explain why the network is so important
- How to build the network
- IP address 
    - Private & Public

## Questions  
- How to setup static IP to a connection and then set the connection to a device
- How to configure the Hostname


- In an OS to view the IP and its configuration
    - ip address show (ip a s)
- To see the routes of the network
    - ip route show
- To See the services and their ports
    - netstat -tulnp ( tcp udp local network port)
    - lsof -i :8080 
- To see the DNS 
    - cat /etc/resolv.conf

- How the IPs are attached to a machine
    - Previously we used to set the IP on the NIC 
    - Now, we do things differently
    - We create something called "connection"
    - We configure all the IP and other related items into that connection file
    - Then we attach the connection to the NIC(Hardware device)
    - At a time the connection can be attached to only one device card


- To know about the connection, we use a service deamon on Linux `Network Manager`
    - `NetworkManager` is a system network service that manages your network devices and connections and attempts to keep network connectivity active when available. It manages Ethernet, WiFi, mobile broadband (WWAN) and PPPoE devices while also providing VPN integration with a variety of different VPN services.
    - To see the list of connections on our system
        - the utility `nncli` is used to manupulate the connection
        - nmcli connection show
        - nmcli connection show "connection_name"
    - To create a new connection
        - nmcli connection add con-name "some_name_of_connection" ifname eth0 type ethernet
    - This created a connection
    - Now, we have to provide the IP info to that connection
    - nmcli connection modify "some_name_of_connection" ipv4.method manual ipv4.address 192.168.2.100/24 
    - Now once the IP is setup, now we can enable this connection to be attached with eth0
    - nmcli connection up "some_name_of_connection"
    - This will make the new connection up with eth0
    - This will change the DNS, the route, IP, Gateway etc 

- Where all these configurations are stored
    - Linx is all about files & folders
    - So, everything goes and stores in a file
    - The network related info also goes and stores in a file
    - cd /etc/sysconfig/network-scripts/
    - There all the connections would be listed with their connection names
    - We can directly edit the conf from these files as well, rather using the command line `nmcli modify`
    - more info 
    - https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/ch-network_interfaces#sect-setting-the-host-name

- How to change the name of the hostname(servername)
    - see the name of the hostname
        - hostname
    - Doing any action like modify, change, we need some utility
        - `hostnamectl` --help 
        - change to a new name 
            - hostname set-hostname "new_name"
    - All these hostname related items are stored on `/etc/hostname` file

- For laptops within a LAN, generally uses local hostname to connect
    - /etc/hosts
    - update the name of the laptop and their IP (static)
    - ex 💯
        - 192.168.1.200 ftp.my-laptop
        - 192.168.1.201 video-my-laptop\