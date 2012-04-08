#Open Source Pipeline

Python + Bash + Nuke + Shotgun + ?

##Mission: 
It's the twenty-first century, folks! If you're working in the VFX industry, there's a good chance you're not working at ILM, DD, Weta or any other shop that's been around for ages and has lots of developers working on their big, well developed pipeline. In fact, it's very likely that you're part of a small team leveraging the current peak of capability found in commodity hardware and the wealth of non-proprietary VFX software to create your own world. And why wouldn't you? 

The problem you're probably running into -- just like every other small shop -- is that these commodity tools don't automatically slot into each-other by themselves. And moving information around by hand is definitely sub-optimal. You may have also teamed up with other small shops and need to be able to swap files around between yourselves.

So you need a little bit of organization and you need a little bit of glue-ware. 

Enter the Open Source Pipeline.

##Current status: Broken
Dammit. I was playing a little too fast and loose by having Python scripts print commands for BASH to execute. It was a tricky solution and it worked... for a little while. But not any more. So I'm trying to figure out another approach.

I'm also wondering if a set of scripts called Open Source Pipeline should limit users to using BASH. Wouldn't it me nice to use the shell of your choice? Or maybe we should embrace the 21st century and get rid of shells entirely! What if OSP was written entirely in Python? How's that for bleeding-edge?

So, yeah... watch this space. I'm still thinking about OSP. You may have noticed updates are pretty rare. I blame trying to balance time with my loved ones, my job in the VFX industry, and my interest in opening the pipeline. There's only enough time for two of those at the moment. Hopefully that'll change in the future.

##Goals:
+ Minimal configuration on the workstation
+ Understand that artists want to deal with as little "technical stuff" as possible. 
+ Structure the environment so that it's flexible and expandable (multiple shows, variable naming-standards, changing storage).
+ Utilize Shotgun as a central "brain" that knows where everything lives on the filesystem. 
+ Facilitate "breaking off" a chunk of work to outside vendors and bringing their output back into the pipe. 
+ Allow customization by overloading OSP standard components with local studio-custom code. 

##Approach: 
+ Use the idea from Unix of simple, single-function tools, piped together to create something useful and complex.
+ Rely on [Shotgun](http://www.shotgunsoftware.com/) for the production database.

##Components in progress:
+ ospenv : A studio-wide command-line environment and framework for job-specific customizations. This is the base framework that OSP will run on. 
+ show.sh : Allows the user to further set up the environment for a show, sequence and shot.

##Future components:
+ Daily system
+ Site/Show/Shot magic for Nuke. Knobs in root which get evaluated + updated, all pathnames in script get expression-linked to the root knobs for single-point "correctability."
+ Checking  tool for logging sources in SG.
+ Log all sources in a Nuke script into Shotgun as an element and link them to the SG Version.
+ A "package up these files and send them to a vendor" tool.

#Installing

The Open Source Pipeline will need to have a home on a central location, called OSP_HOME. This will probably be a network share or something similar, something that's available to all the machines in the facility. 

Once the OSP files are placed in this central location, run the install script (osp/core/ospinstall) on each machine that will be "OSP-aware." This script will modify /etc/bashrc in order to source the OSP environment from our central location. This is the only bit of configuration that lives locally on a workstation (see goal #1, "minimal configuration on the workstation," above.) All other configuration will be done facility-wide from OSP_HOME.
