# HTB Pwnbox RDP over SSH

A high-performance and versatile alternative means to connect to HackTheBox's Pwnboxes.

## Get Started

> **⚠️ CAUTION:**  

> The xRDP server deployed by this script intentionally sacrifices several important security features to maximize performance. This is feasible because all data will travel through a secure SSH tunnel. This setup is strictly for educational purposes and should not be implemented in any other context. The author assumes no responsibility for misuse.

### Server-Side Setup

1. On the Pwnbox's home directory, open the `user_init` script (this script gets executed by HTB each time a new Pwnbox is deployed).
2. Insert the following commands:

    ```sh
    #!/bin/bash
    # This script is executed every time your instance is spawned.

    # Download the script from the raw URL
    sudo wget https://raw.githubusercontent.com/s4ndev/HTB-pwnbox-scripts/main/pwnbox_init.sh

    # Make the script executable
    sudo chmod +x pwnbox_init.sh

    # Execute the script
    ./pwnbox_init.sh
    ```
    
3. Done! Wait approximately 3 minutes after deployment and proceed to the Client-Side section.

### Client-Side Setup

> On the server side, we primarily deploy an xRDP server (among other things). Direct RDP to the Pwnbox's assigned hostname/IP may not work due to their reverse proxy or other restrictions.

1. Wait a few minutes for the script to finalize on the Pwnbox server.

2. Connect to the server using RDP over SSH. This involves establishing an SSH tunnel that will translate your local port 3389/tcp to the Pwnbox's interface on port 3389/tcp.

   - If you need guidance, refer to the `example_client.sh` script in the repository. It provides a basic example that works on macOS/Linux and can be translated to Windows, though some dependencies need to be installed first (details are in the first line of the script).

Note: You will need to create an "App Token" within HTB in order to perform this. (Link: https://app.hackthebox.com/profile/settings)

## Objectives and Improvements

### Current Objective

Configure the RDP (xRDP) server over xOrg to deliver the highest performance and lowest latency without sacrificing too much quality.

### Improvements Made So Far

- **Using xRDP over xOrg:** Improved performance compared to xRDP over VNC.
- **Optimization:** Reduced unnecessary processes that affect RDP session performance. Static content enhances performance, so unnecessary 3D effects and animations are minimized.
- **FreeRDP Client Arguments:** Currently identifying the best arguments to use with the FreeRDP client to connect to the Pwnbox's RDP server (50% complete).

---

For a practical demonstration, refer to the `example_client.sh` file in the main repository. This file shows how to connect to a Pwnbox instance with optimized settings.
