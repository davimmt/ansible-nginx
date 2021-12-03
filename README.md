## How to work with this repo
This repo is supossed to work in three branches side-by-side, that is: `dev`, `hom` and `prd`.<br>
Configuration files will be `shared` to all branches while `individual` files will be exclusive for each one 
(they can be the same at some point):

|Individual files|
|---|
| hosts |
| roles/deploy/templates |
| roles/deploy/vars |
| roles/undeploy/defaults |

**This means that no commit can include `shared` files and `individual` files at the same time.**

One should use `cherry-picking` to merge shared files commits from another branches, while leaving individual files commits alone. <br>
And `checkout <branch> <path>` (path should be listed in the above table) can be used to stage individual files commits from another branches, while leaving shared files commits alone.

## Commands
### Checking inventory
    ansible-inventory --graph
### Pinging hosts
    ansible -m ping all
### Running playbooks
    ansible-playbook [-e "cli_hosts=<hosts>"] <name>.yml

## Playbook descriptions
- `install.yml` – if NGINX is not installed, will install its latest version; if installed, will update to the latest version.
- `uninstall.yml` – uninstall NGINX.
- `start.yml` – start NGINX.
- `stop.yml` – stop NGINX.
- `restart.yml` – restart NGINX.
- `deploy.yml` – will install or ensure NGINX is installed; start or ensure NGINX is started; create or ensure some necessary folders are present; deploy all server blocks that have a file at *roles/deploy/templates/\*.j2*; reload NGINX if any changes.
- `undeploy.yml` – undeploy all server blocks that are present at *roles/undeploy/defaults/main.yml*; reload NGINX if any changes.
- `main.yml` – deploy.yml + undeploy.yml.