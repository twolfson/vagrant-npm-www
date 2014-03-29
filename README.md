# vagrant-npm-www [![Build status](https://travis-ci.org/twolfson/vagrant-npm-www.png?branch=master)](https://travis-ci.org/twolfson/vagrant-npm-www)

[Vagrant][] setup for [`npm-www`][]

This was created to isolate dependency management (e.g. [elasticsearch][], [Java][]) from the host OS. When working with a new technology, we prefer to isolate ourselves from potentially shooting ourselves in the foot.

[Vagrant]: http://www.vagrantup.com/
[`npm-www`]: https://github.com/npm/npm-www

// TODO: Screenshot please

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
npm run dev

On your host machine, you can access `npm-www` at:
https://127.0.0.1:15443/
```

When `npm run dev` stops outputting CouchDB information (e.g. `[PUT]`), you should be able to access the website:

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
