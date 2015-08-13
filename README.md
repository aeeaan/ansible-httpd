correcthorse.httpd
=========

Role for installing apache httpd and configuring vhosts.

Role Variables
--------------
| Variable						| Default				| Notes			|
| :---							| :---					| :---			|
| httpd_mod_ssl						| true					| 			|
| httpd_mpm						| prefork				|			|
| httpd_user						| apache				|			|
| httpd_group						| apache				|			|
| httpd_http_port					| 80					|			|
| httpd_https_port					| 443					|			|
| httpd_open_http_port					| false					|			|
| httpd_open_https_port					| false					|			|
| httpd_default_override				| None					| 			|
| httpd_can_network_connect				| 'no'					|			|
| httpd_can_network_connect_db				| 'yes'					|			|
| httpd_ssl_certificate					| /etc/pki/tls/certs/localhost.crt	|			|
| httpd_ssl_key						| /etc/pki/tls/private/localhost.key	|			|
| httpd_ssl_chain					| '' 					|			|
| httpd_ssl_ca						| ''					|			|
| httpd_ssl_ciphers					| "EECDH+ECDSA+AESGCM:EECDH+aRSA+AESGCM:EECDH+ECDSA+SHA384:EECDH+ECDSA+SHA256:EECDH+aRSA+SHA384:EECDH+aRSA+SHA256:EECDH+AESGCM:EECDH:EDH+AESGCM:EDH+aRSA:HIGH:!MEDIUM:!LOW:!aNULL:!eNULL:!LOW:!RC4:!MD5:!EXP:!PSK:!SRP:!DSS" | |
| httpd_honor_cipher_order				| true					|			|
| httpd_timeout						| 60					|			|
| httpd_remoteip_header					| X-Forwarded-For			|			|
| httpd_remoteip_internal_proxies			| []					|			|
| httpd_remoteip_trusted_proxies			| []					|			|
| httpd_extra_modules					| []					| for extra mod_foo packages that don't warrant their own role |

    httpd_vhosts:
      - servername: localhost2.localdomain	(required)
        documentroot: /vagrant/static		(required)
        redirect_http_to_https: false		(optional, default false)
        ssl_offloaded: false			(optional, default false)
        remoteip: false				(optional, active mod_remoteip for vhost, default false)
        raw: |	       				(optional, for passing in extra apache config)
          ExtraApacheConfigDirective1
          ExtraApacheConfigDirective2

Dependencies
------------

* correcthorse.common

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: correcthorse.httpd }

License
-------

MIT

Author Information
------------------

* [Joshua Rusch](https://correct.horse/)
