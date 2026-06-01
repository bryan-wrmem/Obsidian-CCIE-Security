Create a script to add some vlans and apply them to switch ports

```
from netmiko import ConnectHandler

device = {
    'device_type': 'cisco_ios',
    'host': '10.253.253.218',
    'username': 'admin',
    'password': 'EVE-Secret123',
    'secret': 'EVE-Secret123',
}

# Configuration commands to push
config_commands = [
    # --- Create vlans ---
    "vlan 10,20,30,40",

    # --- Add vlans to switch ports ---
    "interface GigabitEthernet1/0/1",
    "switchport mode access",
    "switchport access vlan 10",
    "description access vlan 10",
    "interface GigabitEthernet1/0/2",
    "switchport mode access",
    "switchport access vlan 20",
    "description access vlan 20",
    "interface GigabitEthernet1/0/3",
    "switchport mode access",
    "switchport access vlan 30",
    "description access vlan 30",
    "interface GigabitEthernet1/0/4",
    "switchport mode access",
    "switchport access vlan 40",
    "description access vlan 40",
]

try:
    # Connect to the device
    print(f"Connecting to {device['host']}...")
    connection = ConnectHandler(**device)

    # Enter enable mode (if not already privileged)
    connection.enable()

    # Send configuration commands
    print("Pushing configuration...")
    output = connection.send_config_set(config_commands)
    print(output)

    # Save the configuration
    save_output = connection.save_config()
    print(save_output)

    # Verify — show the new interface status
    print("\n--- Verification: Interface Gi1/0/1 ---")
    print(connection.send_command("sh int status | i Gi1/0/1"))

    # Verify — show the new interface status
    print("\n--- Verification: Interface Gi1/0/2 ---")
    print(connection.send_command("sh int status | i Gi1/0/2"))

    # Verify — show the new interface status
    print("\n--- Verification: Interface Gi1/0/3 ---")
    print(connection.send_command("sh int status | i Gi1/0/3"))

    # Verify — show the new interface status
    print("\n--- Verification: Interface Gi1/0/4 ---")
    print(connection.send_command("sh int status | i Gi1/0/4"))

    # Disconnect
    connection.disconnect()
    print("\nDone! Configuration applied and saved successfully.")

except Exception as e:
    print(f"An error occurred: {e}")
```

[Open: Pasted image 20260530125725.png](c3ecfd224b2a2abba5897f590f1b55d2_MD5.png)
![](c3ecfd224b2a2abba5897f590f1b55d2_MD5.png)

