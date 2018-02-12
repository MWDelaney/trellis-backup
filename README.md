# trellis-backup
Role to set up [Stouts.backup](https://github.com/Stouts/Stouts.backup) jobs for [Roots/Trellis](https://roots.io/trellis/) sites

## Usage
From your project directory

1) Clone this repository
````{r, engine='bash', count_lines}
git clone --depth=1 git@github.com:MWDelaney/trellis-backup.git trellis/roles/backup && rm -rf trellis/roles/backup/.git
````

2) Clone Stouts.backup
````{r, engine='bash', count_lines}
git clone --depth=1 git@github.com:Stouts/Stouts.backup.git trellis/roles/Stouts.backup && rm -rf trellis/roles/Stouts.backup/.git
````

3) Add `trellis-backup` and `Stouts.backup` to server.yml:
 ````yaml
- name: Set up backups
  hosts: web:&{{ env }}
  become: yes
  roles:
    - { role: backup, tags: [backup] }
    - { role: Stouts.backup, tags: [backup] }
````

4) Reprovision your server to add backup tasks:
````{r, engine='bash', count_lines}
ansible-playbook server.yml -e env=production
````
