# Kweli Network Creation

Kweli ledger is based on Hyperledger Indy. The following is a guide to configure an [Indy](https://www.hyperledger.org/projects/hyperledger-indy) node to join the Kweli Network.

## Aim

The aim of this codebase is to allow entities and/or organizations to setup a shared network of trustees, stewards and nodes (according to prior agreements).

The final result is a pool of validator nodes run in Docker containers, that produce content (e.g., logs and ledger data) available to the host machine through volumes mounting.

## Structure

On a general level, the main entities interacting with the repository to setup the pool are two: the **pool creator**, responsible to collect the initial required information from the other entities involved in the _genesis transactions_, and the **members**, i.e., the entities involved in the initial setup of the pool but that do not have the duty of generating the actual genesis transactions or collect information from the other partners. A better description of the process is explained in the next sections.

The repository is so divided:

- `common`: this folder contains scripts that are usually used by all the parties involved, such as those for generating the needed keys to interact with the pool and the ledger.
- `containers`: the content of this folder is not actively used. It contains files that allow to spin up the Docker containers running the validator node software (one per steward, i.e., one per partner entity involved).
- `creator`: all the scripts that the entity responsible to create the pool needs to execute in order to produce the needed configuration files to run the network.
- `member`: the entities that participate in the network setup, albeit not as creators, will interact with the scripts in this folder in order to join the initial network.
- `utils`: utility functions both for internal use as well as available to users to, e.g., download all the needed dependencies to execute the scripts and launch the containers.
