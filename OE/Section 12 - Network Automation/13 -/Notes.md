```
from netmiko import ConnectHandler

  

# Define the switch connection parameters

device = {

    "device_type": "cisco_ios",

    "host": "192.168.1.1",            # Replace with your switch's management IP

    "username": "admin",              # Replace with your username

    "password": "yourpassword",       # Replace with your password

    "secret": "enablepassword",       # Replace with your enable secret (if needed)

}

  

# --- VLAN-to-Port Mapping ---

# Easy to modify — just update this dictionary to scale

vlan_map = {

    10: {"name": "DATA",       "ports": range(1, 11)},   # Ports 1–10

    20: {"name": "VOICE",      "ports": range(11, 21)},  # Ports 11–20

    30: {"name": "MANAGEMENT", "ports": range(21, 31)},  # Ports 21–30

}

  

def build_config(vlan_map):

    """Build the full configuration command list from the VLAN map."""

    commands = []

  

    # --- Step 1: Create all VLANs ---

    for vlan_id, info in vlan_map.items():

        commands.append(f"vlan {vlan_id}")

        commands.append(f"name {info['name']}")

  

    # --- Step 2: Assign ports to VLANs ---

    for vlan_id, info in vlan_map.items():

        for port in info["ports"]:

            commands.append(f"interface GigabitEthernet0/{port}")

            commands.append("switchport mode access")

            commands.append(f"switchport access vlan {vlan_id}")

            commands.append("spanning-tree portfast")

            commands.append("no shutdown")

  

    return commands

  
  

try:

    # Connect to the switch

    print(f"Connecting to switch at {device['host']}...")

    connection = ConnectHandler(**device)

  

    # Enter enable mode

    connection.enable()

  

    # Build and push the configuration

    config_commands = build_config(vlan_map)

    print(f"Pushing {len(config_commands)} configuration commands...")

    output = connection.send_config_set(config_commands)

    print(output)

  

    # Save the configuration

    print("\nSaving configuration...")

    save_output = connection.save_config()

    print(save_output)

  

    # --- Verification ---

    print("\n" + "=" * 50)

    print("          VERIFICATION OUTPUT")

    print("=" * 50)

  

    # Verify VLANs exist

    print("\n--- VLAN Summary ---")

    print(connection.send_command("show vlan brief"))

  

    # Verify port assignments per VLAN

    for vlan_id in vlan_map:

        print(f"\n--- Ports Assigned to VLAN {vlan_id} ---")

        print(connection.send_command(f"show vlan id {vlan_id}"))

  

    # Verify switchport status for a sample port from each VLAN

    sample_ports = [1, 11, 21]

    for port in sample_ports:

        print(f"\n--- Switchport Status: Gi0/{port} ---")

        print(connection.send_command(f"show interfaces GigabitEthernet0/{port} switchport"))

  

    # Disconnect

    connection.disconnect()

    print("\nDone! VLANs created and ports assigned successfully.")

  

except Exception as e:

    print(f"An error occurred: {e}")
```