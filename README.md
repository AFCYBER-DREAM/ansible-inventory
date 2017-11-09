# Ansible Inventory

Usage
-----

This repository stores all the inventories for the DREAM Teams' ansible plays.
The structure of the repository is similar to the following:

```
.
├── infra-badger-prod
│   └── inventory
├── infra-badger-stag
│   └── inventory
├── infra-clan-prod
│   └── inventory
└── README.md
```

An advantage of this structure is the use of `inventory` files inside of directories named in project-network-tier format. If Ansible is passed a directory on the command-line as it's target inventory file, it looks for a file named "inventory".

Lastly, you'll notice that the inventory files are separated by project-network-tier, and inside of each inventory file, the parent-child relationship of groups is spelled out clear using INI syntax:

```
[all:children]
infra

[infra:children]
infra-badger-prod

[infra-badger:children]
infra-badger-prod

[infra-badger-prod:children]
infra-badger-prod-artifactory
infra-badger-prod-xray
```

This allows for the plays to use all the host and group vars associated with both the parent and child groups, but also creates some seperation so that a single Ansible command is not mistakenly run across multiple projects, networks, or environment tiers.

