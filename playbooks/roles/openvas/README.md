Kalify OpenVAS Role
===================

This role installs OpenVAS on your Kali Linux server.
The OpenVAS server is started automatically. However, on reboot OpenVAS does
not currently restart automatically. Run `openvas-setup` to start it again.

A standalone Kali Linux server does not require any firewall rules.

You currently need to use a SSH tunnel to connect to the OpenVAS Greenbone Security
Assistant server. The Amazon EC2 Security Group allows SSH by default e.g.

    ssh -L 9392:localhost:9392 admin@<kali ip>

Then connect with your browser to:

    https://127.0.0.1:9392

Once connected you can login with the credentials printed near the end of the
ansible run.
