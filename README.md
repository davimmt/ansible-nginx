## How to work with this repo
This repo is supossed to work in three branches side-by-side, that is: `dev`, `hom` and `prd`.<br>
Configuration files will be `shared` to all branches while `individual` files will be exclusive for each one 
(they can be the same at some point):

||
|---|
| roles/deploy/defaults |
| roles/deploy/templates |
| roles/deploy/vars |
| roles/undeploy/defaults |
||

**That means that all commits must not include `shared` files and `individual` files at the same time.**

This is because *cherry-picking* will be used to merge shared files commits to another branches, while leaving individual files commits alone.

### Checking inventory
    ansible-inventory -i inventories/ --graph
### Main (deploy and undeploy)
    ansible-playbook --key-file ansible.pem -i inventories/hosts main.yml
### Deploy
    ansible-playbook --key-file ansible.pem -i inventories/hosts deploy.yml
### Undeploy
    ansible-playbook --key-file ansible.pem -i inventories/hosts undeploy.yml