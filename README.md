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
| httpd_maxconnectionsperchild				| 0					|			|
| httpd_minspareservers					| 5					| prefork		|
| httpd_maxspareservers					| 10					| prefork		|
| httpd_serverlimit					| 256 prefork, 16 worker/event		| prefork, worker/event |
| httpd_maxrequestworkers				| 256 prefork, 400 worker/event		| prefork, worker/event |
| httpd_startservers					| 5 prefork, 3 worker/event		| prefork, worker/event |
| httpd_threadlimit					| 64	       				| worker/event		|
| httpd_threadsperchild					| 25					| worker/event		|
| httpd_minsparethreads					| 75					| worker/event		|
| httpd_maxsparethreads					| 250					| worker/event		|
| httpd_default_override				| None					| 			|
| httpd_can_network_connect				| 'no'					|			|
| httpd_can_network_connect_db				| 'yes'					|			|
| httpd_servertokens					| Prod					| Major,Minor,Min,Prod,OS,Full |
| httpd_traceenable					| 'off'					| 'off','on','extended' - turn on for RFC 2616 compliancy |
| httpd_logrotate_period				| weekly				| daily, weekly, monthly |
| httpd_logrotate_keep					| 5					| number of rotations to keep |
| httpd_logrotate_compress				| false					| compress logs if true	 |
| httpd_ssl_disable_default_vhost			| false					| disable default ssl vhost |
| httpd_ssl_certificate					| /etc/pki/tls/certs/localhost.crt	|			|
| httpd_ssl_key						| /etc/pki/tls/private/localhost.key	|			|
| httpd_ssl_chain					| '' 					|			|
| httpd_ssl_ca						| ''					|			|
| httpd_honor_cipher_order				| true					|			|
| httpd_timeout						| 60					|			|
| httpd_remoteip_header					| X-Forwarded-For			|			|
| httpd_remoteip_internal_proxies			| []					|			|
| httpd_remoteip_trusted_proxies			| []					|			|
| httpd_extra_modules					| []					| for extra mod_foo packages that don't warrant their own role |

    httpd_ssl_ciphers: "EECDH+ECDSA+AESGCM:EECDH+aRSA+AESGCM:EECDH+ECDSA+SHA384:EECDH+ECDSA+SHA256:EECDH+aRSA+SHA384:EECDH+aRSA+SHA256:EECDH+AESGCM:EECDH:EDH+AESGCM:EDH+aRSA:HIGH:!MEDIUM:!LOW:!aNULL:!eNULL:!LOW:!RC4:!MD5:!EXP:!PSK:!SRP:!DSS"


    httpd_vhosts:
      - servername: localhost2.localdomain	(required)
        serveraliases:				(optional)
          - localhost3.localdomain
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
