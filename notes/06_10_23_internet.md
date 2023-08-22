# 06_10_23

## Network tools

`netstat`

- shows you all the activity on your local machine
- can pass into grep to filter for all sorts of things

`traceroute`

- shows all the hops in given network request
- takes a domain arg: `traceroute google.com`

`ping`

- hits a domain and receives a pong
- useful for checking whether the domain is healthy

`nslookup`

- shows you the underlying ip address and other useful things

`dig`

- shows you the actual dns records

## Setting up server

1. Create a super user (never run as root): `adduser <your-username>`
2. Add user to sudo group: `usermod -aG sudo <your-username>`
3. Switch to the super user: `su <your-username>`
4. Check sudo access: `sudo cat /var/log/auth.log`
