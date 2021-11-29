## How to work with this repo
This repo is supossed to work in three branches side-by-side, that is: `dev`, `hom` and `prd`.<br>
Configuration files will be `shared` to all branches while `individual` files will be exclusive for each one 
(they can be the same at some point):

|Individual files|
|---|
| roles/deploy/defaults |
| roles/deploy/templates |
| roles/deploy/vars |
| roles/undeploy/defaults |
||

**This means that no commit can include `shared` files and `individual` files at the same time.**

One should use `cherry-picking` to merge shared files commits from another branches, while leaving individual files commits alone. <br>
And `checkout <path>` (path should be listed in the above table) can be used to stage individual files commits from another branches, while leaving shared files commits alone.

### Checking inventory
    ansible-inventory -i inventories/ --graph
### Main (deploy and undeploy)
    ansible-playbook --key-file ansible.pem -i inventories/hosts main.yml
### Deploy
    ansible-playbook --key-file ansible.pem -i inventories/hosts deploy.yml
### Undeploy
    ansible-playbook --key-file ansible.pem -i inventories/hosts undeploy.yml