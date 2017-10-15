# TRACE
Transient Cloud Engine - Ephemeral Environments Builder/Manager

*Work in Progress*

## Info

Current in the Design and Initial Development Phase

### Builder/Engine Flow
Initial Idea of Function

![Builder Flow](https://raw.githubusercontent.com/fynxlabs/tempus/master/diagrams/builder_flow.png)

### Idea

This will be a system to create and manage lower environments, qa/dev/test aka non-prod. We'll call them traces when referring to their configuration within the engine.

It will enable having ephemeral or transient environments that build or are turned on (based on config) when accessed. Then after a configured time (e.g.; 15 mins) of inactivity from the instances or load balancers (also configurable) the engine will then trigger a shutdown or destruction of that environment.

#### Building environments

The only way to make something of this feasible is to have a AMI or Image pipeline built out (probably going to have examples). That way you have a image that already has packages updated, your app installed, and most items configured to a default state.

The engine would then build spot instances or a spot fleet with this image, run any configuration managed (e.g.; puppet, salt, ansible) so things are current and the right versions and configs are in place.

##### ON OFF Switching

This will probably be the easiest to accomplish for most, now that AWS allows RDS to be turned on/off at will you can basically have your entire environment shutdown when not in use.

Currently this is Mostly manual, Cloudwatch in AWS (with some other items) can automatically shutdown items after a period of inactivity. But there is no good way to turn them back on without doing it manually or setting a lambda function to run at 9am M-F or something

This if inefficient however, Still going to shutdown after so much time and it will probably be a tad maddening. Hence why I'm working on this. Something that turns on and off based on usage/need.

## TODO
- [ ] Define Scope for MVP
- [ ] Define how system should be configured first, then decide how to make it possible
  - Make the config easy and approachable
- [ ] Build Terraform Scaffolding to build Prototype Engine
- [ ] Create additional diagrams and documentation for

## Decision Points
- [ ] AWS Specific?
  - Making Modularized w/ AWS as Defaults would leave open to adopting system to other Clouds or On-Prem setups
  - Making AWS only limits the amount of code to maintain/up-keep
- [ ] Add-Ons - Decide on in Direct API interaction w/ AWS (or others pending above) or utilize systems such as terraform/cloudformation
  - Pure API will make things straight forward and limit the number of items to interact with
  - Enabling existing systems will make adoption easier, especially for those wanting 'like' environments with production using the same config tools
- [ ] Central Manager?
  - Some kind of pre-canned bootstrap GUI that enables tracking all the traces and status. Maybe add a button to kick them from a console if needed?
  - Requires frontend work and can be a pain, especially for someone like me that does mostly backend work
