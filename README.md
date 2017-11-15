# Library Senior Fellows at UCLA

The program is a collaborative effort of the UCLA Library, UCLA Graduate School of Education and Information Studies, and Ithaka S+R, a nonprofit that provides guidance to the academic community. This project is built using [drupal-composer](https://github.com/drupal-composer/drupal-project) with the [UC D8 distro](https://github.com/ucdavis/sitefarm_seed).

## Development Setup

### Requirements

- Keys to access private dependencies
- PHP 7 - currently `7.0.10`
- [Composer](https://getcomposer.org/doc/00-intro.md)
- Drupal 8 env _(see recommended Docksal setup)_

### Getting Started

`git clone`, `cd [new-project-dir]`, `composer install`, and go!

### Deployment Steps

1. Put site into maint. mode – `cd <project-repo-dir>/web && drush sset system.maintenance_mode 1`
2. Make a backup – `drush ard`
3. Get updates – `cd .. && git pull`
4. Update any deps. – `composer install`
5. Rebuild Drupal's cache – `cd web && drush cr`
6. Apply any database updates – `drush updatedb -y`
7. Import config changes – `drush cim -y` 7.1 Might need to do some features based stuff here, not sure yet though
8. Rebuild Drupal's cache one more time – `drush cr`
9. Take site out of maint. mode – `drush sset system.maintenance_mode 0`

### Development Theme package update to deploy procedure

This project uses the [UCLALibrary/ucla_gateway](https://github.com/uclalibrary/ucla_gateway), this is the process for updating that theme:

1. Do theme work in UCLALibrary/ucla_gateway via fork and make PR upstream
2. Merge PR on UCLALibrary/ucla_gateway
3. Make theme update deployment PR in project repo

  1. Fetch all project updates – `git fetch --all`
  2. Checkout topic branch – `git checkout -b deploy-<your-theme-update-topic> upstream/master`
  3. Update your composer lock – `composer update <theme-repo-package>` eg:

    - `composer update uclalibrary/ucla_gateway`
    - This will see the latest updates in you theme can put them into you composer.lock file

  4. Commit changes in composer lock – `git add composer.lock && git commit -m "updates to latest theme changes with that thing`

  5. Push to your fork and make PR

4. Approve and Merge PR and run deployment steps

## Updating Drupal Core (TBD)
