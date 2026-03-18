context: https://docs.saltproject.io/en/getstarted/index.html#:~:text=SaltStack%20is%20a%20revolutionary%20approach,with%20each%20system%20in%20seconds.

*SaltStack is a revolutionary approach to infrastructure management that replaces complexity with speed. SaltStack is simple enough to get running in minutes, scalable enough to manage tens of thousands of servers, and fast enough to communicate with each system in seconds.*

*Built on Python, Salt is an event-driven automation tool and framework to deploy, configure, and manage complex IT systems. Use Salt to automate common infrastructure administration tasks and ensure that all the components of your infrastructure are operating in a consistent desired state.

Salt has many possible uses, including configuration management, which involves:

- Managing operating system deployment and configuration.
    
- Installing and configuring software applications and services.
    
- Managing servers, virtual machines, containers, databases, web servers, network devices, and more.
    
- Ensuring consistent configuration and preventing configuration drift.
    

Salt is ideal for configuration management because it is pluggable, customizable, and plays well with many existing technologies. Salt enables you to deploy and manage applications that use any tech stack running on nearly any [operating system](https://docs.saltproject.io/salt/install-guide/en/latest/topics/salt-supported-operating-systems.html), including different types of network devices such as switches and routers from a variety of vendors.

In addition to configuration management Salt can also:

- Automate and orchestrate routine IT processes, such as common required tasks for scheduled server downtimes or upgrading operating systems or applications.
    
- Create self-aware, self-healing systems that can automatically respond to outages, common administration problems, or other important events.*

## Pillars
Storing sensitive data

Pillar data is compiled on the master. Additionally, pillar data for a given minion is only accessible by the minion for which it is targeted in the pillar configuration. This makes pillar useful for storing sensitive data specific to a particular minion.

The pillar is by default declared in `/srv/pillar/top.sls`


### Concepts:
- Salt master
	- These are 2 EC2 Instances. prod and dev
	- The minions have a configuration that sets the master instances
	- This will push state to the minions
	- The state of the salt masters are just git branches. To change the state of the master, checkout a different git branch.
- Minions -> gateways/tx2s
	- Give pub/private keys to minions with master
- Grains:
	- The define the operating environments that the states will apply to
		- "Only apply to these grains"
	- Kinda like tags for our gitlab runners
- Reactor:
	- An event for when a minion checks in:
		- Can run any salt applies


### Software Deployment Repo
- CI/CD: On deploy, debian packages  will be copied onto the salt master, but not tracked by git.


### On salt.stoutagtech.dev
- entrypoint for state: **top.sls**


### Pushing State for Development
- Use CI/CD Pipelines to build and deploy to the SALT MASTER.
	- Either use salt-client to pull state or salt master to push
	- 
- 