NOTE: This is work in progress at a very, very early stage ... still in the spiking/designing phase. You cannot install and use this on your own servers yet.

# serene

The serene agent sets up and manages access to your Linux infrastructure. This
includes user accounts, access groups, and ssh keys for your users and your
hosts. Access to your servers is locked down to ssh via two factor
authentication or console via username/password.

## Design Goals
- secure in theory and practice
- simple to install
- simple to add or disable users
- users manage their credentials themselves (distributed/no centralized bottleneck)
- hosts are automatically updated


## User Accounts

Each user's account is managed by them interacting with the serene-server either through the web interface or the cli.
- username ... must be unique across the serene-server
- ssh keys
- sms number for out of band 2nd factor
- sudo/console password

Bureaucrats create and lock accounts, manage access groups, and

## Linux Access Groups

- sudo access is managed through linux groups

## Host Keys

When an agent registers a new host with the server, all agents automatically
add the key to known hosts. When a new host registers a new key for an existing
domain/ip with the server, all agents automatically update the key for that
domain/ip in known hosts.

## sudo

## ssh login

Options for 2fa:
- ForceCommand /usr/local/bin/authy-ssh login
- pam module like duo_unix

sequence diagram based off http://www.linuxjournal.com/article/9566 SSH Under the Hood article.

```jsseq
participant CLIENT
participant SERVER
Note over CLIENT: ssh-transport
CLIENT->SERVER: (kex) SSH_MSG_KEXINIT
SERVER->CLIENT: SSH_MSG_NEWKEYS
CLIENT->SERVER: SSH_MSG_SERVICE_REQUEST
SERVER->CLIENT: SSH_MSG_SERVICE_ACCEPT
Note over CLIENT: ssh-userauth
CLIENT->SERVER: SSH_MSG_USERAUTH_REQUEST
SERVER->CLIENT: SSH_MSG_USERAUTH_SUCCESS
CLIENT->SERVER: SSH_MSG_CHANNEL_OPEN
Note over CLIENT: ssh-connection
```

## ssh-userauth sequence diagram
- https://tools.ietf.org/html/rfc4251 ... SSH Protocol Architecture
- https://tools.ietf.org/html/rfc4252 ... SSH Authentication Protocol

```jsseq
participant CLIENT
participant SERVER
```
