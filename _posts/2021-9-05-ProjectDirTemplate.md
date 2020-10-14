---
layout: post
title: A template for structuring your scientific code
excerpt:
         <p>Over the last ten years or so i've slowly settled on a standard template and directory structure for my coding projects. I don't see many people sharing ideas on project layout or directory structure so I thought i'd post a short blog on what I do.</p>
---
Over the last ten years or so i've slowly settled on a standard template and directory structure for my coding projects. I don't see many people sharing ideas on project layout or directory structure so I thought i'd post a short blog on what I do.

### Small to Medium Projects
In my mind small project are projects where all of the data and source code can fit on my laptop without causing too many problems. Therefore i put the whole project in one project directory structured as so:
```
.
    |-- bin
    |-- config.ini
		|-- docs
    |-- data
    |-- logs
		|-- runtime
		|   `-- logs
		|-- scripts
    |   `-- dotask.py
    |   `-- python
    |   `-- runall.py
    |   `-- shell
		|-- tests
```

Small - all in one dir on the one machine.
Mid - most in one dir but data maybe on an external drive.





### Big Projects


Huge - some code with data on one machine some other code and data on another machine. Try to have src all together and to have the whole project managed by version control and make sure that the you know what is checked out where. Maybe have a build script that you check out in a tmp dir and run build to move it to wherever you need it to be. Have no hard code paths - only use config files that allow you to modify stuff on the fly as the time will come when you want to run an experiment and put data elsewhere.
