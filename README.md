# ansible-role-munin-fcgi
Enable munin "dynazoom" graphs using _spawn-fcgi_ and a systemd service.

# Requirements
Only tested on Ubuntu 16.04 xenial, a few paths in
[munin-fcg.service](files/munin-fcgi.service) are specific to Debian-based
distributions but any OS running a _munin_ server and _systemd_ should be fine.

## Role Variables
None.

## Dependencies
None.

## Example Playbook
Play:
```yaml
- hosts: munin-master
  become: true
  roles:
    - {role: "geerlingguy.munin"}
    - {role: "geerlingguy.nginx"}
    - {role: "digitalbackstage.munin-fcgi"}
```

Nginx configuration:
```nginx
location ^~ /munin-cgi/munin-cgi-graph/ {
    fastcgi_split_path_info ^(/munin-cgi/munin-cgi-graph)(.*)$;
    fastcgi_param PATH_INFO $fastcgi_path_info;
    fastcgi_pass unix:/var/run/munin/fcgi-graph.sock;
    include fastcgi_params;
}
```

## License
MIT

## Author Information
Written by [Léo Peltier](https://leo-peltier.fr/) for [UniversCiné/Le Meilleur du Cinéma](http://www.universcine.com/).
