# laptop-postconf

An Ansible collection for post-configuration tasks on laptops, including DHCP server configuration and edge device gather OS information.

## Playbooks:
- `dhcp-configure.yaml`: Configures the DHCP server for edge devices.
- `gather_version_info.yaml`: Gathers version info from laptops.
- `upload_images_local.yaml`: Push Local Images to container Registry
- `upload_images.yaml`: Copy Images from Container Registry A to Container Registry B

## Templates:
- `dhcpd.conf.j2`: Template for DHCP server configuration file.

## Requirements:
- Ansible 2.15.13 or later
- Supported Linux distributions (RHEL like)

## Ansible Playbook Commands

Below are the commands to execute the playbooks for configuring and managing the system:

1. Configure DHCP Server:
    ```bash
    ansible-playbook os_mgmt.laptop_postconf.dhcpd_configure.yaml -i ansible-content/inventories/ -e @ansible-content/vars/dhcp_server_vars.yaml
    ```

2. Upload Images Locally:
    ```bash
    ansible-playbook os_mgmt.laptop_postconf.upload_images_local.yaml
    ```

3. Tag and Push Images Locally and run podman-autoupdate:
    ```bash
    ansible-playbook os_mgmt.laptop_postconf.tag_images.yaml -e@ansible-content/vars/tag_images_vars.yaml
    ```

4. Gather Version Information from Edge:
    ```bash
    ansible-playbook os_mgmt.laptop_postconf.edge_gather_version_info.yaml -i ansible-content/inventories/ -u admin -k
    ```

5. Generate Bootloader Files:
    ```bash
    ansible-playbook os_mgmt.laptop_postconf.generate_bootloaders_files.yml -e '{efi_grub_files_destination: ~/iso-build/laptop-rhel84/DevicesGRUBs/, bios_ipxe_files_destination: ~/iso-build/laptop-rhel84/ipxe/}'
    ```
6. Generate Custom ISO:
    ```bash
    ansible-playbook os_mgmt.laptop_postconf.generate_custom_iso.yaml -e@ansible-content/vars/generate_custom_iso_vars.yaml
    ```

Make sure to replace any placeholders like `admin` with appropriate values and adjust paths if necessary.
