La Ruche qui dit oui - Plugin Discourse
=======================================

![interface](https://cloud.githubusercontent.com/assets/88243/24135485/b64cda76-0e55-11e7-812f-8def24d183c9.png)

## Local development using vagrant

```
vagrant up
vagrant ssh
mailcatcher --ip 0.0.0.0
cd /vagrant
bundle exec rails s -b 0.0.0.0
bundle exec sidekiq -l log/sidekiq.log -q critical -q default -q low
```

Point your browser to:
- http://127.0.0.1:4000 - Discourse instance
- http://127.0.0.1:4000/sidekiq2 - Sidekiq queues
- http://127.0.0.1:40803 - mailcatcher

## Installation using docker

```
cd /var/discourse
vi containers/app.yml
```

Add the following to your app.yml in the plugins section:

```
hooks:
  after_code:
    - exec:
        cd: $home/plugins
        cmd:
          - mkdir -p plugins
          - git clone https://github.com/ekkans/lrqdo-plugin-discourse.git
```

and rebuild docker via

```
./launcher cleanup
./launcher rebuild app
```
