Kalify Nessus Role
==================

This role downloads and installs Nessus 6.3.4 to your Kali Linux server.
The Nessus server is started automatically.

If you are running an Amazon EC2 Kali Linux Instance you must first allow TCP
port 8834 in the Amazon EC2 Security Group assigned to the EC2 instance.

A standalone Kali Linux server does not require any firewall rules.

You may then connect to Nessus:

    https://<kali ip>:8834

You may also use a SSH tunnel to connect to the Nessus server. The Amazon EC2
Security Group allows SSH by default e.g.

    ssh -L 8834:localhost:8834 admin@<kali ip>

Then connect with your browser to:

    https://127.0.0.1:8834

Once connected you can walk through the initial set up and activation.
