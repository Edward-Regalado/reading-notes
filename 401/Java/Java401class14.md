# Hashing Passwords: One-way Road to Security

- hashing is the foundation of secure password storage.
- the gist of auth is to proivde users with a set of credentials (username & password) and to verifty that they provide the correct credentials whenever they want access to the application.
- storing passwords on the servier side for auth is a difficult task.

## Storing passwords is risky and complex

- a simple solution would be just to store the usersname and password in a database table.
- the most basic and least secure password storagne is cleartext (this is equivalent of writing them down on a piece of digital paper)
- security strength depends on how the passowrd is stored.
- cleartext refers to the "readable data transmitted or stored in the clear", for example, unencrypted.
- hashing transforms password into data that cannot be converted back to the original password

## What's hashing about?

- a hash function is a mathematical algorithm that maps data of any size to a bit string of a fixed size. 
- it's easy and practical to compute the hash, but near impossible to re-generate the original input if only the hash value is known.
- it's difficult to create an initial input that would match a specific desired output.

- the implementation of a sha256 hash function in python
- the hash string represents 256 bits of information in total and all of its inputs have an output of equal size.

```
from hashlib import sha256
h = sha256()
h.update(b'python1990K00L')
hash = h.hexdigest()
print(hash)

output: d1e8a70b5ccab1dc2f56bbf7e99f064a660c08e361a35751b9c483c88943d082

```

### Crytographic Hash Functions are practically irreversible

- The pre-image is what we call a value that produces a certain specific hash when used as input to a hash function -- the plaintext value -- and it must be pre-image resistant.
- small changes in the password huge changes after the values are hashed- this is called the avalanche effect


### Using Crypgraphic Hashing for More Secure Password Storage

- irreversible mathematical propteries
- hash functions are deterministic - given the same input always produces the same output- needed in order to be able to validate the users credentails.

## Why you should use BCrypt to hash passwords

- hashed passwords solutions fall short
- many password solutions are not good enough

### Salting the password

- 'salt' add a very long string of bytes to the password and adds anoter layer of security
- a random 'salt' string could be added for each user, created on the generation of the user account and this will increase encryption significantly as hackers will have to try to find a password for a single user at a time.

## BCrypt Solution

- based on the Blowfish block cipher cryptomatic algorithm and takes the form of an adaptive hash function.
- uses a Key Factor and is able to adjust the cost of hashing.
- with key factor changes, the hash output can be influenced.
- bcrypt is extermely resistant to hacks, especially the type of password cracking called rainbow table.


### Sources  

[auth0](https://auth0.com/blog/hashing-passwords-one-way-road-to-security/)  

[Daniel Boterhoven](https://danboterhoven.medium.com/why-you-should-use-bcrypt-to-hash-passwords-af330100b861)  