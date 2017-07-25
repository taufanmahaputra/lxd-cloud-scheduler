# LXD Cloud Scheduler
>LXD project by GO-SQUADS Tech Intern 2017

This is the setup we are using for LXD team's project: LXD web interface and cloud scheduler.

## Installing / Getting started

After cloning the repo, run this in root:

```bash
sudo apt-get install virtualbox vagrant
vagrant up
```

And you're up and running. To ssh into master:

```bash
vagrant ssh master
```

## Developing

```shell
git clone https://github.com/satraul/lxd-cloud-scheduler.git
cd lxd-cloud-scheduler/
```

To-do list for automation:
1. Create box/automate provisioning for bridge-utils and zfs
2. Upating LXD to feature release (optional)
3. Creating a preseed file for lxd init --preseed

## Licensing

The code in this project is licensed under MIT license.
