### Deploy Laravel5 using Ansible in Capistrano way

#### Prepare

Create hosts file for all your environments from example:

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

- `playbook-deploy.yml` - Run files deployment
- `playbook-rollback.yml` - Rollback deploy
- `playbook-migrate.yml` - Run migrations
- `playbook-seed.yml` - Run seeding

```bash
ansible-playbook playbook-deploy.yml -i production -u root
```

#### Deployment order

1. Init releases directory structure
1. Update repositody
1. Export a copy of the repo to a new release directory
1. Copy `.env.example` to `shared/.env` if it was absent
1. Copy `storage` to `shared/storage` if it was absent
1. Remove local `.env` & `storage` from release directory
1. Create soft links to shared `.env` & `storage`
1. Install composer localy
1. Run `composer self-update`
1. Run `composer install`
1. Clear Laravel cache
1. Optimize code
1. Run `npm install`
1. Run `gulp --production`
1. Change soflink to new release
1. Update chown
1. Install cachetool to clear opcache
1. Run `cachetool opcache:reset`
1. Restart Laravel queue
1. Delete old relases

> Attention! Don't forget to update your `shared/.env` file after first deloy!
