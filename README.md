# vagrant-npm-www

[Vagrant][] setup for [`npm-www`][]

This was created to isolate dependency management (e.g. [elasticsearch][], [Java][]) from the host OS. When working with a new technology, we prefer to isolate ourselves from potentially shooting ourselves in the foot.

[Vagrant]: http://www.vagrantup.com/
[`npm-www`]: https://github.com/npm/npm-www

![Screenshot of `vagrant-npm-www`](docs/screenshot.png)

## Getting Started
Install [Vagrant][] as instructed by http://www.vagrantup.com/

Clone this repository via `git`:

```bash
git clone https://github.com/twolfson/vagrant-npm-www
```

Launch the [Vagrant][] instance:

```bash
vagrant up
# Bringing machine 'default' up with 'virtualbox' provider...
```

When the machine is done provisioning, you will be prompted with next steps:

```bash
`npm-www` is ready to go
To start the app, inside of `vagrant ssh`, run the following:
cd /vagrant/npm-www
sudo npm run dev

On your host machine, you can access `npm-www` at:
https://127.0.0.1:15443/
```

The website will be immediately available but there will be no packages as replication occurs. Replication is over when you no longer see messages like:

```
[info] [<0.856.0>] 127.0.0.1 - - PUT /registry/gulp-bower-source?new_edits=false&rev=4-be904485b7d5b1f4e9b1b9d41d46a101 201
```

The website will be available on the host computer at:

https://127.0.0.1:15443/

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style.

## Donating
Support this project and [others by twolfson][gittip] via [gittip][].

[![Support via Gittip][gittip-badge]][gittip]

[gittip-badge]: https://rawgithub.com/twolfson/gittip-badge/master/dist/gittip.png
[gittip]: https://www.gittip.com/twolfson/

## Unlicense
As of Mar 29 2014, Todd Wolfson has released this repository and its contents to the public domain.

It has been released under the [UNLICENSE][].

[UNLICENSE]: UNLICENSE
