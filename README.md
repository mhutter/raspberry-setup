# Raspberry Pi Setup :rocket:

Includes:
* [Admin user setup][mhutter-base]
* [Traefik][traefik]
* [Pi-Hole][pihole] - DNS based ad/tracker blocker
* [MinIO][minio] - S3 compatible storage
* [Watchtower][watchtower] - auto update of running docker images
* iptables setup
* OpenVPN Server configuration

## Limitations

- Docker is not installed automatically. See `curl -fsSL https://get.docker.com -o get-docker.sh`
- OpenVPN is not installed automatically. See https://docs.pi-hole.net/guides/vpn/overview/ for instructions

## Usage

0. Create `hosts.yml` according to template:
    ```yaml
    ---
    raspberry:
      hosts:
        rpi:
          ansible_host: 12.34.56.78
    ```
0. Create `group_vars/raspberry.yml` according to example:
    ```yaml
    ---
    base_admin_username: mhutter
    base_pubkey_url: https://github.com/mhutter.keys
    pihole_webpassword: 'TODO: set a password here'
    pihole_dns1: 1.1.1.1
    pihole_dns2: 1.0.0.1
    pihole_virtual_host: 'TODO: set (pihole.example.com)'
    watchtower_slack_url: 'TODO: get from https://<your slack>.slack.com/apps'
    minio_access_key: 'TODO: set an access key here'
    minio_secret_key: 'TODO: set a secret here'
    ```
0. Install ansible requirements:

        ansible-galaxy install -r roles/requirements.yml

0. Run it!

        ansible-playbook main.yml


---

> [Manuel Hutter](https://hutter.io) - GitHub [@mhutter](https://github.com)

[mhutter-base]: https://github.com/mhutter/ansible-base
[traefik]: https://traefik.io/
[pihole]: https://pi-hole.net/
[minio]: https://www.min.io/
[watchtower]: https://github.com/containrrr/watchtower
