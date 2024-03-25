# ueransim

The ueransim repository enables the building of a multi-container and multi-node cluster of ueransim using Docker. This allows you to run ueransim simulations on multiple VMs, with the flexibility to run multiple containers on each VM.

To download the ueransim repository, use the following command:
```
git clone https://github.com/aligungr/UERANSIM
```

## Step-by-Step Installation
To install ueransim, follow these steps:

1. Install Docker by running `make ueransim-docker-install`.
2. Configure the network for ueransim:
   - Set the "data_iface" parameter to the network interface name of the machine.
   - Set "macvlan_iface" to the name of the macvlan interface to be created.
   - Set "macvlan_network_name" to the name of the Docker network to be created.
   - Set "subnet_prefix" to the first two bytes of the subnet, which should correspond to the "custome_ran_subnet" of 5g-core or the machine's subnet.
3. Start the ueransim Docker containers using `make ueransim-docker-start`:
   - Set the container "image" for ueransim.
   - Set "prefix" to the desired name for the ueransim containers.
   - Set "count" to the number of containers to be instantiated on each VM.
4. Start the simulation:
   - Set "amf.ip" to the IP address of the core machine.
   - Set "ueid_base" to the starting IMSI number.
     - Each container will have a different starting IMSI number.
   - Set "ue_per_pod" to the number of UEs on each ueransim container.
   - Set the "ueransims" array with a list of key-value pairs:
     - Each key represents the container number (numeric).
     - The corresponding value `config_file` is the config template file for ueransim.
   - Run `make ueransim-simulator-start`.
5. Check the results:
   - Enter one of the Docker containers using `docker exec -it *prefix*-1 bash`.
   - Use `cat summary.log` to view the last result.
   - To check the logs generated by ueransim, use `cat *ueransim*.log`.

### One-Step Installation
To install ueransim in one go, run `make ueransim-simulator-setup-install`.

### Uninstall
To uninstall ueransim, run `make ueransim-simulator-setup-uninstall`.
