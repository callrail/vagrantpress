# CallRail Marketing Site VagrantPress

*VagrantPress* is a packaged development environment for developing WordPress themes and modules.  
This repo is intended to serve as a means to quickly set up a development environment for the [CallRail Marketing Site](https://github.com/callrail/marketing-site).


## Prerequisites
+ [Homebrew Cask](https://github.com/caskroom/homebrew-cask) - `brew install caskroom/cask/brew-cask`
+ [Vagrant](http://www.vagrantup.com/downloads.html) - `brew cask install virtualbox`
+ [Virtualbox](https://www.virtualbox.org/wiki/Downloads) - `brew cask install vagrant`
+ [Vagrant Hostsupdater](https://github.com/cogitatio/vagrant-hostsupdater) - `vagrant plugin install vagrant-hostsupdater`

## Getting Started

In order to get the development environment up and running, there are a few steps that need to be completed (listed below).  As of right now, this is still a fairly manual process, but ideally it will be further automated in the future.

1. Clone this project.
2. Clone the [Marketing Site](https://github.com/callrail/marketing-site) into a directory adjacent to this project.
3. Obtain a copy of the Production database from WP Engine.  Rename and place here: `puppet/modules/wordpress/files/wordpress-db.sql`.
4. Obtain a copy of `wp-config.php` from the Production FTP server.  Rename and place here: `puppet/modules/wordpress/files/wp-config.php`.
5. Modify `wp-config.php` to set the values below. You should see each of these lines in the config file, but with different values on the right-hand side.  Make sure to replace them with values listed below.  If you don't see one of these lines, copy and paste it into `wp-config.php`.
  
  ```
  define( 'DB_NAME', 'wordpress' );
  define( 'DB_USER', 'wordpress' );
  define( 'DB_PASSWORD', 'wordpress' );
  define( 'WP_HOME', 'http://callrail.local' );  
  define( 'WP_SITEURL', '' );
  ```
6. Run the command `vagrant up` from the `vagrantpress` directory (this will take a while, it installs everything you need)
7. Open your browser to http://callrail.local

NOTE: For the time being, you still have to run `compass watch` from the `marketing-site` on your computer if you're making CSS changes.

## Other Stuff

### Vagrant commands (run these from withint the `vagrantpress` directory):
+ `vagrant up` - starts the VM for the Marketing site, makes it avaiable at `http://callrail.dev`
+ `vagrant halt` - stops the VM, `http://callrail.dev` will no longer be available
+ `vagrant destroy` - wipes out the VM, next time you run `vagrant up` it will re-install everything
+ `vagrant ssh` - provides you with command line access to the VM

When you're done working on the site, run `vagrant halt` from the `vagrantpress` directory to shut the VM down.  When you need to work on the site again, you can run `vagrant up` from within the `vagrantpress` directory any time.

### TODO
+ Add ruby/compass to the VM and configure the VM to run it on boot (also maybe provide a log for this?)
+ Put the SQL dump and `wp-config.php` files on S3 and have the VM retrieve them on provisioning to eliminate the manual step
+ troubleshoot some images not loading correctly
+ Use Chef instead of Puppet for provisioning script :neckbeard: 
