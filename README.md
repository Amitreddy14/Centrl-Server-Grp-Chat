# Secure Cental Server Group Chat

## Overview
This project features a secure, Signal-inspired group chat system that allows multiple users to communicate via a central server. It leverages the CryptoPP and Boost libraries for implementing cryptographic protocols and network communications.

### Server
A centralized server architecture is adopted to ensure efficiency and scalability for multi-user interactions. The server is multithreaded, enabling it to manage several user connections simultaneously. It also functions as a certificate authority—verifying user credentials and issuing digitally signed certificates.

### User
Users are required to register or log in using a valid password, followed by a two-factor authentication process to obtain a certificate. Once authenticated, users can securely message each other using certificate-based encryption, eliminating the risk of impersonation.

Beyond one-on-one messaging, users can form group chats and perform administrative actions like adding or removing members.

### Security Premises
#### Diffie-Hellman Key Exchange
Secure communication is established using DH key exchange between users and the server, as well as between users themselves. Messages are double encrypted: first with the sender-recipient shared key, and again with a key shared between the sender and server, ensuring the server cannot read the messages.

#### Semi-honest Server
The server is trusted to route messages correctly without inspecting their content. Group messages are treated as individual direct messages to each member, preventing the server from inferring group structures. 

## Running the code
To build the project, `cd` into the `build` folder and run `cmake ..`. This will generate a set of Makefiles building the whole project. From here, you can run `make` to generate a binary (`chat_user` and `chat_server`) you can run, and you can run make check to run any tests you write in the test folder.

### Server
To run the server binary, run `./chat_server <port> <config file>`. We have provided server config files for you to use; you shouldn't need to change them. Afterwards, the server will start listening for connections and handle them in separate threads.

- list registered users: `$ users`
- reset registered users: `$ reset`

### User
To run the user binary, run `./chat_user <config file>`. You may find example users from the `config` folder. 

#### Full Command List
- login and connect: `$ login <address> <port>`
- register and connect: `$ register <address> <port>`
- direct message: `$ dm <userID> <message>`
- create group: `$ create <groupID> <userID> [userID] [userID] ...`
- group message: `$ gm <groupID> <message>`
- add member to group: `$ add <groupID> <userID>`
- remove self from group: `$ rm <groupID>`
- list groups and members: `$ groups`
- disconnect from server: `$ exit`

## Future Development
1. Integrate Double Ratchet Protocol for more robust user-to-user key exchanges.
2. Fully obfuscate group structures from the server using distributed or probabilistic methods.
3. Improve the command-line user interface for better usability.

## _Reference_
