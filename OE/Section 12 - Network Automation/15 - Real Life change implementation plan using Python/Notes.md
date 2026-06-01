Example CSV

```
vlan,ip

100,192.168.100.1

200,192.168.200.1

```

Script

```
from netmiko import ConnectHandler

import csv

import re

  

# ===== DEVICE INFO =====

device = {

    "device_type": "cisco_ios",  # change to "arista_eos" if needed

    "host": "192.168.1.10",

    "username": "admin",

    "password": "password",

}

  

# ===== CSV FILE =====

csv_file = "vlans.csv"

  

# ===== CONNECT =====

connection = ConnectHandler(**device)

print("[INFO] Connected to device")

  

# ===== GET CURRENT CONFIG =====

running_config = connection.send_command("show running-config")

vlan_output = connection.send_command("show vlan brief")

  

# ===== HELPER FUNCTIONS =====

def vlan_exists(vlan_id):

    return str(vlan_id) in vlan_output

  

def ip_exists(ip_address):

    return ip_address in running_config

  

# ===== PROCESS CSV =====

with open(csv_file, mode="r") as file:

    reader = csv.DictReader(file)

  

    for row in reader:

        vlan = row["vlan"].strip()

        ip = row["ip"].strip()

  

        print(f"\n[INFO] Processing VLAN {vlan} with IP {ip}")

  

        # ===== VALIDATION =====

        if vlan_exists(vlan):

            print(f"[ERROR] VLAN {vlan} already exists. Skipping.")

            continue

  

        if ip_exists(ip):

            print(f"[ERROR] IP {ip} already exists in config. Skipping.")

            continue

  

        # ===== CONFIGURATION =====

        config_commands = [

            f"vlan {vlan}",

            f"name VLAN_{vlan}",

            f"interface vlan {vlan}",

            f"ip address {ip} 255.255.255.0",

            "no shutdown"

        ]

  

        print(f"[INFO] Applying config for VLAN {vlan}")

  

        output = connection.send_config_set(config_commands)

        print(output)

  

# ===== SAVE CONFIG =====

connection.save_config()

print("\n[INFO] Configuration saved")

  

# ===== DISCONNECT =====

connection.disconnect()

print("[INFO] Disconnected")


```

Output/error handling

```
[INFO] Processing VLAN 100 with IP 192.168.100.1

[ERROR] VLAN 100 already exists. Skipping.

  

[INFO] Processing VLAN 200 with IP 192.168.200.1

[INFO] Applying config for VLAN 200

(config output...)

```