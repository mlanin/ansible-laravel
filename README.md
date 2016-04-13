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

- `deploy.yml` - Run files deployment
- `migrate.yml` - Run migrations & seeds if you want
- `seed.yml` - Run seeding

```bash
ansible-playbook deploy.yml -i production -u root
```
