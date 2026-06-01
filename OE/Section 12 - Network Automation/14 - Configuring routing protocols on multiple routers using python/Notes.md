```
from netmiko import ConnectHandler

import time

  

# ============================================================

#  DEVICE DEFINITIONS

# ============================================================

  

router1 = {

    "device_type": "cisco_ios",

    "host": "192.168.1.1",            # Replace with Router 1's management IP

    "username": "admin",

    "password": "yourpassword",

    "secret": "enablepassword",

}

  

router2 = {

    "device_type": "cisco_ios",

    "host": "192.168.1.2",            # Replace with Router 2's management IP

    "username": "admin",

    "password": "yourpassword",

    "secret": "enablepassword",

}

  

# ============================================================

#  CONFIGURATION MAP

#  Easy to modify — all router-specific details in one place

# ============================================================

  

config_map = {

    "Router1": {

        "device": router1,

        "loopback_id": 0,

        "loopback_ip": "1.1.1.1",

        "loopback_mask": "255.255.255.255",

        "ospf_router_id": "1.1.1.1",

        "connected_interface": "GigabitEthernet0/0",       # Interface facing Router2

        "connected_network": "10.0.0.0",                   # Shared link subnet

        "connected_wildcard": "0.0.0.3",                   # /30 wildcard

    },

    "Router2": {

        "device": router2,

        "loopback_id": 0,

        "loopback_ip": "2.2.2.2",

        "loopback_mask": "255.255.255.255",

        "ospf_router_id": "2.2.2.2",

        "connected_interface": "GigabitEthernet0/0",       # Interface facing Router1

        "connected_network": "10.0.0.0",                   # Shared link subnet

        "connected_wildcard": "0.0.0.3",                   # /30 wildcard

    },

}

  
  

def build_config(cfg):

    """Build the configuration commands for a single router."""

    commands = [

        # --- Create Loopback ---

        f"interface Loopback{cfg['loopback_id']}",

        f"ip address {cfg['loopback_ip']} {cfg['loopback_mask']}",

        f"description OSPF Router-ID Loopback",

        "no shutdown",

  

        # --- Ensure the connected interface is up ---

        f"interface {cfg['connected_interface']}",

        "no shutdown",

  

        # --- Enable OSPF ---

        "router ospf 1",

        f"router-id {cfg['ospf_router_id']}",

        "log-adjacency-changes",

  

        # --- Advertise the Loopback into OSPF Area 0 ---

        f"network {cfg['loopback_ip']} 0.0.0.0 area 0",

  

        # --- Advertise the connected link into OSPF Area 0 ---

        f"network {cfg['connected_network']} {cfg['connected_wildcard']} area 0",

    ]

    return commands

  
  

def configure_router(name, cfg):

    """Connect to a router, push config, and run verification."""

    device = cfg["device"]

  

    print(f"\n{'=' * 60}")

    print(f"  CONFIGURING {name} ({device['host']})")

    print(f"{'=' * 60}")

  

    try:

        # Connect

        print(f"  Connecting to {device['host']}...")

        connection = ConnectHandler(**device)

        connection.enable()

  

        # Push configuration

        commands = build_config(cfg)

        print(f"  Pushing {len(commands)} commands...")

        output = connection.send_config_set(commands)

        print(output)

  

        # Save

        print("  Saving configuration...")

        save_output = connection.save_config()

        print(save_output)

  

        # Verification

        print(f"\n  --- {name}: Loopback{cfg['loopback_id']} Status ---")

        print(connection.send_command(

            f"show ip interface brief | include Loopback{cfg['loopback_id']}"

        ))

  

        print(f"\n  --- {name}: OSPF Interfaces ---")

        print(connection.send_command("show ip ospf interface brief"))

  

        # Disconnect

        connection.disconnect()

        print(f"\n  {name} configured successfully! ✓")

        return True

  

    except Exception as e:

        print(f"\n  ERROR on {name}: {e}")

        return False

  
  

def verify_ospf_adjacency(cfg):

    """Reconnect to Router1 and check if the OSPF neighbor is up."""

    device = cfg["device"]

  

    print(f"\n{'=' * 60}")

    print(f"  VERIFYING OSPF ADJACENCY FROM {device['host']}")

    print(f"{'=' * 60}")

  

    try:

        connection = ConnectHandler(**device)

        connection.enable()

  

        print("\n  --- OSPF Neighbors ---")

        print(connection.send_command("show ip ospf neighbor"))

  

        print("\n  --- OSPF Routes in Routing Table ---")

        print(connection.send_command("show ip route ospf"))

  

        print("\n  --- Full OSPF Database ---")

        print(connection.send_command("show ip ospf database"))

  

        connection.disconnect()

  

    except Exception as e:

        print(f"\n  ERROR during verification: {e}")

  
  

# ============================================================

#  MAIN EXECUTION

# ============================================================

  

if __name__ == "__main__":

  

    print("\n" + "#" * 60)

    print("#    OSPF DUAL-ROUTER CONFIGURATION SCRIPT")

    print("#" * 60)

  

    # Step 1: Configure both routers

    results = {}

    for name, cfg in config_map.items():

        results[name] = configure_router(name, cfg)

  

    # Step 2: Wait for OSPF adjacency to establish

    if all(results.values()):

        print("\n⏳ Both routers configured. Waiting 15 seconds for OSPF adjacency...")

        time.sleep(15)

  

        # Step 3: Verify OSPF from Router1's perspective

        verify_ospf_adjacency(config_map["Router1"])

  

        print("\n" + "#" * 60)

        print("#    ALL DONE — OSPF adjacency should be FULL")

        print("#" * 60)

    else:

        failed = [n for n, ok in results.items() if not ok]

        print(f"\n⚠️  Configuration failed on: {', '.join(failed)}")

        print("Please fix the errors above and re-run.")
```