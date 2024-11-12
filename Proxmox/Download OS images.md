# Download OS images
#Proxmox #Virtualization 

First we update and list available os images for Proxmox
```bash
pveam update
pveam available
```

Output:
```
mail            proxmox-mail-gateway-8.1-standard_8.1-1_amd64.tar.zst
mail            proxmox-mailgateway-7.3-standard_7.3-1_amd64.tar.zst
system          almalinux-9-default_20240911_amd64.tar.xz
system          alpine-3.18-default_20230607_amd64.tar.xz
system          alpine-3.19-default_20240207_amd64.tar.xz
system          alpine-3.20-default_20240908_amd64.tar.xz
system          archlinux-base_20240911-1_amd64.tar.zst
system          centos-9-stream-default_20240828_amd64.tar.xz
system          debian-11-standard_11.7-1_amd64.tar.zst
system          debian-12-standard_12.7-1_amd64.tar.zst
system          devuan-5.0-standard_5.0_amd64.tar.gz
system          fedora-39-default_20231118_amd64.tar.xz
system          fedora-40-default_20240909_amd64.tar.xz
system          gentoo-current-openrc_20231009_amd64.tar.xz
system          opensuse-15.5-default_20231118_amd64.tar.xz
system          opensuse-15.6-default_20240910_amd64.tar.xz
system          rockylinux-9-default_20240912_amd64.tar.xz
system          ubuntu-20.04-standard_20.04-1_amd64.tar.gz
system          ubuntu-22.04-standard_22.04-1_amd64.tar.zst
system          ubuntu-24.04-standard_24.04-2_amd64.tar.zst
turnkeylinux    debian-10-turnkey-collabtive_16.1-1_amd64.tar.gz
turnkeylinux    debian-10-turnkey-concrete5_16.1-1_amd64.tar.gz
turnkeylinux    debian-10-turnkey-drupal8_16.2-1_amd64.tar.gz
turnkeylinux    debian-10-turnkey-ezplatform_16.0-1_amd64.tar.gz
turnkeylinux    debian-10-turnkey-foodsoft_16.1-1_amd64.tar.gz
turnkeylinux    debian-10-turnkey-magento_16.1-1_amd64.tar.gz
turnkeylinux    debian-10-turnkey-moinmoin_16.1-1_amd64.tar.gz
turnkeylinux    debian-10-turnkey-mongodb_16.1-1_amd64.tar.gz
turnkeylinux    debian-10-turnkey-processmaker_16.1-1_amd64.tar.gz
turnkeylinux    debian-10-turnkey-revision-control_16.1-1_amd64.tar.gz
turnkeylinux    debian-10-turnkey-trac_16.1-1_amd64.tar.gz
turnkeylinux    debian-11-turnkey-b2evolution_17.1-1_amd64.tar.gz
turnkeylinux    debian-11-turnkey-drupal9_17.1-1_amd64.tar.gz
turnkeylinux    debian-11-turnkey-ghost_17.1-1_amd64.tar.gz
turnkeylinux    debian-11-turnkey-gnusocial_17.1-1_amd64.tar.gz
turnkeylinux    debian-11-turnkey-joomla3_17.1-1_amd64.tar.gz
turnkeylinux    debian-11-turnkey-mahara_17.1-1_amd64.tar.gz
turnkeylinux    debian-11-turnkey-mayan-edms_17.1-1_amd64.tar.gz
turnkeylinux    debian-11-turnkey-plone_17.1-1_amd64.tar.gz
turnkeylinux    debian-11-turnkey-sahana-eden_17.1-1_amd64.tar.gz
turnkeylinux    debian-11-turnkey-vanilla_17.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-ansible_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-asp-net-core_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-avideo_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-bagisto_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-bookstack_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-bugzilla_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-cakephp_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-canvas_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-codeigniter_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-concrete-cms_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-core_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-couchdb_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-django_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-dokuwiki_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-domain-controller_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-drupal10_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-drupal7_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-e107_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-elgg_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-espocrm_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-etherpad_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-faveo-helpdesk_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-fileserver_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-foswiki_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-gallery_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-gameserver_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-gitea_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-gitlab_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-ibexa_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-icescrum_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-invoice-ninja_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-jenkins_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-joomla4_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-lamp_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-lapp_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-laravel_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-leantime_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-lighttpd-php-fastcgi_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-limesurvey_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-mantis_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-matomo_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-mattermost_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-mediaserver_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-mediawiki_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-mibew_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-moodle_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-mumble_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-mysql_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-nextcloud_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-nginx-php-fastcgi_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-nodejs_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-observium_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-odoo_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-omeka_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-opencart_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-openldap_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-openvpn_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-orangehrm_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-oscommerce_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-otrs_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-owncloud_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-phpbb_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-phplist_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-postgresql_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-prestashop_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-processwire_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-rails_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-redis_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-redmine_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-roundup_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-silverstripe_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-simplemachines_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-snipe-it_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-suitecrm_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-symfony_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-syncthing_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-tkldev_18.1-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-tomcat-apache_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-tomcat_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-torrentserver_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-tracks_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-typo3_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-ushahidi_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-web2py_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-wireguard_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-wordpress_18.2-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-xoops_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-yiiframework_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-zencart_18.0-1_amd64.tar.gz
turnkeylinux    debian-12-turnkey-zoneminder_18.0-1_amd64.tar.gz
```

Find the os image you intend to download, copy the file name, then run:
```bash
pveam download [storage pool] [os file name]
```

Example:
```
pveam download local fedora-39-default_20231118_amd64.tar.xz
```

After downloading the image, this should be available in the specified storage pool.