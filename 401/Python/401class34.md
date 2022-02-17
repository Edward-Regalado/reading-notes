# Configuring Djano Settings: Best Practices

### Managing Djano Settings: Issues

#### Different environments

- usually you have several environment: local, dev, ci, qa, staging, production, etc.
- each env can have its own specific settings.

#### Sensitive data

- have SECRET_KEY in each django project.
- there can be DB passwords and tokens for 3rd party APIs like Amazon and Twitter.
- This data cannot be stored in VCS

#### Sharing settings between team members

- need to general approach to eliminate human error when working with the settings.
- a dev may add a third-party app or some API integration and fail to add specific settings.

## Setting Configuration: Different Approaches

- no built-in universal way to configure Django settings without hardcoding them.

### settings_local.py

- this is the oldest method.
- basic idea of this method is to extend all environment-specific settings in the `settings_local.py` file, which is ignored by VCS.
- Pros: secrets not in VCS
- Cons: `settings_local.py` is not in VCS, so you can lose some of your Django env settings, django settings file is a Python code, so `settings_local.py` can have some non-obvious logic and you need to have `settings_local.example` (in VCS) to share the default configuration for devs.

## What is SSH?

- Secure Shell, is a remote administration protocol that allows ussers to control and modify their remote servers over the internet.
- created as a replacement for the unencrypted Telnet and uses cryptographic techniques to ensure that all communication to and from the remote server happens in an ecrypted manner.
- provides a mechnanism for authenticating a remotre user, transferring input from the client to the host, and relaying the output back to the client.

## How Does SSH Work

- for Mac and Linux users, open terminal and then follow the procedure below:
- The SSH command consists of 3 parts:
- `ssh {user}@{host}`
- user represents the account you want to access.
- host refers to the computer you want to access.

## Different Encryption Techniques

- There are three different encryption technologies used by SSH:

#### Symmetric Encryption

- is a form of encryption where a secret key is used for both encryption and decryption of a messsage by both the client and the host.
- anyone possessing the key can decrypt the message being transferred.
- Symmetrical encryption is often called shared key or shared secret encryption.
- Keys are used to encrypt the entire communication during a SSH Session.
- The process of creating a key is carried out by a key exchange algorithm.

#### Asymmetric Encryption

- uses two separate keys for encryption and decryption: Public key and Private key.
- public key is openly distributed and shared with all parties.
- a message that is encrypted by a machine's public key can only be decrypted by the smae machine's private key.

#### Hashing

- One-way hashing is another form of cryptography used in Secure Shell Connections.
- generate a unique value of a fixed length for each input that show no clear trend which can be exploited.
- makes them practically impossible to reverse
- SSH used hashes to verifty the authenticity of messages by using HMACs, or Hash-based Message Authentication Codes.
