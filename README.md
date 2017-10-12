# Senior Fellows at UCLA

The program is a collaborative effort of the UCLA Library, UCLA Graduate School of Education and Information Studies, and Ithaka S+R, a nonprofit that provides guidance to the academic community.

## Development Setup

### Requirements

- Keys to access private dependencies
- PHP 7 - currently `7.0.10`
- [Composer](https://getcomposer.org/doc/00-intro.md)
- Drupal 8 env _(see recommended Docksal setup)_

### Recommended Docksal Setup (pending)

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

    - `composer update uclalibrary/ucla_gateway` _(don't forget `fin exec ...` if you are using docksal)_
    - This will see the latest updates in you theme can put them into you composer.lock file

  4. Commit changes in composer lock – `git add composer.lock && git commit -m "updates to latest theme changes with that thing`
  5. Push to your fork and make PR

4. Approve and Merge PR and run deployment steps

--------------------------------------------------------------------------------

**_TDB if we need the rest of this stuff_**

## Updating Drupal Core

This project will attempt to keep all of your Drupal Core files up-to-date; the project [drupal-composer/drupal-scaffold](https://github.com/drupal-composer/drupal-scaffold) is used to ensure that your scaffold files are updated every time drupal/core is updated. If you customize any of the "scaffolding" files (commonly .htaccess), you may need to merge conflicts if any of your modified files are updated in a new release of Drupal core.

Follow the steps below to update your core files.

1. Run `composer update drupal/core --with-dependencies` to update Drupal Core and its dependencies.
2. Run `git diff` to determine if any of the scaffolding files have changed. Review the files for any changes and restore any customizations to `.htaccess` or `robots.txt`.
3. Commit everything all together in a single commit, so `web` will remain in sync with the `core` when checking out branches or running `git bisect`.
4. In the event that there are non-trivial conflicts in step 2, you may wish to perform these steps on a branch, and use `git merge` to combine the updated core files with your customized files. This facilitates the use of a [three-way merge tool such as kdiff3](http://www.gitshah.com/2010/12/how-to-setup-kdiff-as-diff-tool-for-git.html). This setup is not necessary if your changes are simple; keeping all of your modifications at the beginning or end of the file is a good strategy to keep merges easy.

## FAQ

### How can I apply patches to downloaded modules?

If you need to apply patches (depending on the project being modified, a pull request is often a better solution), you can do so with the [composer-patches](https://github.com/cweagans/composer-patches) plugin.

To add a patch to drupal module foobar insert the patches section in the extra section of composer.json:

```json
"extra": {
    "patches": {
        "drupal/foobar": {
            "Patch description": "URL to patch"
        }
    }
}
```

### How do I switch from packagist.drupal-composer.org to packages.drupal.org?

Follow the instructions in the [documentation on drupal.org](https://www.drupal.org/docs/develop/using-composer/using-packagesdrupalorg).
