The code and the following notes are from a presentation on using Ansible to 
setup a couple of basic web servers to: 
  
  * Setup NGINX as a proxy to a local 
  [BlueOakJS](https://github.com/BlueOakJS/blueoak-server) template project 
  running on a different port.  
  * Transfer files I need to have my development environment the way I like it
  * Setup users and groups
  * Install server dependencies
  * Install app dependencies
  * Deploy
  * Build
  * Start and persist with PM2

ONE - DevOps for Developers
=================================================================================
  
  How is this useful from the perspective of a developer?

  - Most of us in this office are full stack developers.  Being a full stack 
  developer means that your skillset is divided across two (or more) domains that 
  warrant their own specialization.  So, at least in my case, I'm willing to 
  make that sacrifice in order to be as self-sufficient as possible.  I like 
  being equipped to create a full end-to-end project.

  - As full-stack developers, (again in my personal experience) is that we
  neglect the far ends of either side of the full-stack, so our experience looks 
  more like this:

TWO -> FOUR: Distribution of Skill
=================================================================================

  You can probably argue that the column to the far left might not belong in 
  that location, but for the sake of illustrating a point I've set it up this 
  way.

FIVE -> EIGHT:  Approaches
=================================================================================

I Have to admit I ripped off the premise of this slide from another presentation 
I saw a while back that I unfortunately can't find anymore.

So the idea is that there are these tiers to the way we handle server
administration going from worst to most ideal.

1. The job is handed off to an individual who has some mysterious process that 
sort of works.

2. The processes are documented but aren't automated.  Each server must be 
manually configured, updated, etc.  Deployments are manual, etc.

3. So this is a definite step in the right direction, but lacks standardization.
Processes might involve a collection of scripts loosely scattered about

4. Automation with configuration management and infrastructure orchestration 
tools

NINE: Overview
=================================================================================

  1. Provide a standardized approach to problems around server administration, 
  deployments, etc.
  2. What infrastructure as code means, is that your code describes what your 
  server infrastructure should look like, how it should behave, etc.  It means 
  you can keep this in version control.  Large open source communities.

TEN - Comparison
=================================================================================
  
  Puppet and Chef are Ruby projects.  They've both been around for a while now 
  and are very large and enterprise-y, and sort of industry standards at this 
  point. They're likely very powerful, but I wasn't interested because of the 
  large time investment to get going.  I don't care about getting certified, 
  being marketable as an enterprise-y DevOps guy, etc.

  Salt and Ansible are "2nd generation" config management, Infrastructure 
  orchestration tools. Salt is known to be faster, but a bit more difficult 
  to use.  Ansible is still plenty fast and very easy to use.  It's possible 
  to pick up and to do useful things with it even on your first day or two
  with it.

ELEVEN - THIRTEEN: When it's useful
=================================================================================

  Single Server?

  - It's debatable.  Administering one server isn't a huge time sink and it 
  might take a while to get a return on your educational investment

  Multi Server?

  - If you have a handful of servers to administer, still not a huge deal, but 
  the more servers you add the more impractical individual server management 
  becomes and the more beneficial tools like Ansible become

  Many Servers / complex deployments? 

  - Anything more than a handful, tools in this category become more or less 
  essential.

FOURTEEN - How it works
=================================================================================

  - Use your own computer to administer remote servers over SSH
  - Create a host file that has your servers' IP Address / Hostname
  - Write a series of "roles" that describe the state you'd like to see
  - Execute the roles in a sequence called a playbook
  - Use the CLI to apply playbooks to particular severs or server groups


FIFTEEN - SIXTEEN: Diving In
=================================================================================

  So now I'm going to walk through setting up publically accessible staging and 
  production servers running a blueoak-server-template project. I've created two
  fresh micro instances from Digital Ocean running Ubuntu 14.04.

  Take a second to think about how long this would take you to set up manually

  ...

  - Explain project structure
    - Flexible enough to accomodate any structure
    - Canonical structure

  - Explain host files
    - Explain groups

  - Explain group_vars

  - Explain host_vars

  - Explain roles

  - Explain modules
    - Linux philosophy (super tiny programs that do one thing and do that thing well)
    - Show modules list 

  - Explain playbooks
    - Explain how they're comprised of roles

  - Explain how states are described (ideal)
    - Idempotent

  - Explain templating
    - nginx template
    - blueoak default.json template

  Show and explain the following commands:

  - ping: ansible -i hosts all -m ping -u root
  - show affected: ansible-playbook -i hosts playbook.yml --list-hosts
  - dry run: ansible-playbook -i hosts playbook.yml --check
  - actual: ansible-playbook -i hosts playbook.yml
  - actual (verbose): ansible-playbook -i hosts playbook.yml -v

Wrapping up
=================================================================================
  
  This was kind of an arbitrary example, some other great usecases for Ansible 
  are: rolling restarts, zero-downtime deployments, managing high availability
  environments.

  Stuff to think about:

  - Possible use cases around the office
  - Open for questions

