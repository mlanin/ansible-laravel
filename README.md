### Deploy Laravel5 using Ansible in Capistrano way

#### Prepare

Create hosts file for (all or any):

- production
- staging
- develop

```bash
cp hosts.example production
```

Create `group_vars/laravel.yml` from example:

```bash
cp group_vars/laravel.example.yml group_vars/laravel.yml
```

Edit it to match your environment.

> Note! Playbook uses [Ansistrano](http://ansistrano.com/), so you are free to update default `group_vars` and use Ansistrano's.

#### Use

Playbooks:

- `master.yml` - Run all tasks
- `deploy.yml` - Only files deployment
- `migrate.yml` - Only migrations & seeds if you want
- `seed.yml` - Only seeding

```bash
ansible-playbook deploy.yml -i production -u root
```
