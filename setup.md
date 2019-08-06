---
title: Pre-workshop Material
---

Before working through the tutorial, please be diligent and read through this page and ensure you
are familiar with all of these computing skills.  They are essential for any HEP physicist
and will benefit you throughout your career.  However, if you are pressed for time in the next days
then **be sure to install and familiarize yourself with Docker**.


## Install This Now! : [Docker](https://www.docker.com/)

  <p>
    <a href="https://www.docker.com/">Docker</a> is a powerful tool that allows you
    to perform a virtualization of your environment but completely in software.  It
    allows you to bundle up the installation of tools for use by others in a uniform way
    and we will be using it throughout this bootcamp.  Installing docker is absolutely
    necessary and there are directions to do this in each operating system.  For those
    of you that are using a Windows operating system, if you already have docker running
    and are comfortable using it, that is fine.  However, if you do not, then be aware
    that its usage on Windows can be challenging and none of the tutors know how to use
    such a setup.  Therefore, <strong>we highly reccomend that you reconsider
    your decision to use the Windows operating system as a high energy physicist.</strong>
  </p>

<div id="DockerOS"> {% comment %} Start of 'DockerOS' section. {% endcomment %}
  <div>
    <ul class="nav nav-tabs nav-justified" role="tablist">
      <li role="presentation" class="active"><a data-os="windows" href="#docker-windows" aria-controls="Windows" role="tab" data-toggle="tab">Windows</a></li>
      <li role="presentation"><a data-os="macos" href="#docker-macos" aria-controls="MacOS" role="tab" data-toggle="tab">MacOS</a></li>
      <li role="presentation"><a data-os="linux" href="#docker-linux" aria-controls="Linux" role="tab" data-toggle="tab">Linux</a></li>
    </ul>

    <div class="tab-content">
      <article role="tabpanel" class="tab-pane active" id="docker-windows">
        <p>
          <font color="red">It is highly recommended that you</font> <strong> DO NOT </strong> <font color="red">use Windows.  Few individuals
          use this OS within the HEP community as most tools are designed for Unix-based systems.
          If you do have a Windows machine, consider making your computer a dual-boot machine </font>-
          <a href="https://opensource.com/article/18/5/dual-boot-linux">Link to Directions</a>
          <br/>
          <br/>
          Download Docker for Windows <a href="https://docs.docker.com/docker-for-windows/install/">instructions</a>.<br>
          <br/>
          Docker Desktop for Windows is the Community Edition (CE) of Docker for Microsoft Windows. To download Docker Desktop for Windows, head to <a href="https://hub.docker.com/editions/community/docker-ce-desktop-windows">Docker Hub</a>. <br>
          <br/>
          Please read the relevant information on these pages, it should take no more than 5 minutes.
          <br/>
        </p>
      </article>
      <article role="tabpanel" class="tab-pane" id="docker-macos">
        <p>
          <br/>
          Download Docker for MacOS <a href="https://docs.docker.com/docker-for-mac/install/">instructions</a>.<br>
          <br/>
          Docker is a full development platform for creating containerized apps, and Docker Desktop for Mac is the best way to get started with Docker on a Mac. To download Docker Desktop for MacOS, head to <a href="https://hub.docker.com/editions/community/docker-ce-desktop-mac">Docker Hub</a>. <br>
          <br/>
          Please read the relevant information on these pages, it should take no more than 5 minutes.
          <br/>
          Another common way to install packages on Mac OSX is via the <a href="https://brew.sh/">homebrew</a> package manager.  In the case of docker, you can easily install
          docker by setting up homebrew and executing <code>brew cask install docker</code>.
          <br/>
        </p>
      </article>
      <article role="tabpanel" class="tab-pane" id="docker-linux">
        <p>
          <br/>
          Downloading and installing Docker for Linux may be slightly more difficult but please contact the organisers or tutors as soon as possible so they can help with any problems.<br>
          <br/>
          Here are the instructions for two popular Linux distributions:
          <li><a href="https://docs.docker.com/install/linux/docker-ce/CentOS/">CentOS</a></li>
          <li><a href="https://docs.docker.com/install/linux/docker-ce/ubuntu/">Ubuntu</a></li>
          <br/>
          Instructions for other Linux distributions can be found on the Docker docs pages.
          <br/>
          <br/>
          <font color="red">Be sure to read the Docker documentation on post-installation steps for Linux and managing Docker
          as a </font> <a href="https://docs.docker.com/install/linux/linux-postinstall/">non-root user</a>.
          <font color="red">This will allow you to edit files when you have started up the Docker container from your image. </font>
          <br/>
        </p>
      </article>
    </div>
  </div>
</div> {% comment %} End of 'docker' section. {% endcomment %}

> ## Know the Basics
>
> There is a wealth of documentation on the basics of docker all over the internet.  However,
> a local tutorial, written by Matthew Fiecker who is a HEP colleague, can be found here - [Link To Tutorial](https://github.com/matthewfeickert/Intro-to-Docker).
> Please take 2 hours to work through the basics here.  Then confirm that you appreciate what the following commands do
>
> ~~~bash
> docker pull smeehan12/dmatlhc2019-tutorial:v0
> docker run --rm -it -v $PWD:/contur/local smeehan12/dmatlhc2019-tutorial:v0 bash
> ~~~
>
> It would be a good idea to spend some time thinking about this since you will need to be using both of
> these commands for the tutorial itself.
>
{: .challenge}

## Know This Stuff Before the Tutorial

Throughout this workshop we will assuming previous knowledge in Unix, Python, C++, as well
as a new tool called Docker, which you have hopefully installed above. Luckily these topics
are heavily documented already and there is a lot of material available so if you feel you
are not very confident with any of these prerequisites please read the links below and work
through the examples before you arrive. It is not necessary for you to be an expert but it
would be beneficial to have some experience and to feel comfortable working with them. For many
of you, this may just be going through and confirming your familiarity with these topics,
but for others, please take this as an opportunity/excuse to learn these fundamental skills.

> ## Prerequisite Checklist
> - Unix and the Terminal : Review and understand the contents of the [Software Carpentry Tutorial](http://swcarpentry.github.io/shell-novice/).
> - Essential C++ : Ensure you understand the concepts in the "Bare Minimum" checklist.
> - Python : Review and understand the contents of the [Software Carpentry Tutorial](http://swcarpentry.github.io/python-novice-inflammation/).
> - Git : The [GitHub](https://github.com/) service is very common and you should know it (and sign up for an account if you haven't already).  The service used by CERN is [GitLab](https://gitlab.cern.ch/) and if you have a CERN computing account, you can log on here as well.
>
{: .checklist}


### Unix and Shells

In Unix operating systems like Linux or OSX, the shell ("**the terminal**") is a program that interprets commands and acts as an intermediary
between the user and the inner workings of the operating system. It can help you navigate
your files and directories.  You can create (`touch` and `mkdir`), copy (`cp`) and delete (`rm`) files and repositories. Even more
powerful things are possible such as working remotely with `ssh`, the transfer of files with `scp` and
shell scripting tasks you do regularly.

> ## What are those commands?
>
> If you are wondering what any of the commands are in the above paragraph, then you can always use the shell to
> learn more by using the `man` command.  Read more about the `ssh` command by trying the following
> ```bash
> man ssh
> ```
> More importantly, if you are wondering how any of these commands work, then it is _imperative_ that you spend a day reviewing
> how the shell works **prior to the bootcamp**.
{: .callout}

Software Carpentry provides two very nice in-depth tutorials on the shell
- [Unix and the Shell](http://swcarpentry.github.io/shell-novice/) : <span style="color:red">**All participants should review this tutorial and ensure they are comfortable with its contents prior to the bootcamp.**</span>
- [Advanced Techniques](http://swcarpentry.github.io/shell-extras/) : This is useful to review, but not necessary for this bootcamp.

A few other very good go-to resources that are good to work through

* [History of Unix and the Shell](https://www.distributednetworks.com/basic-unix-shell-scripts/module2/available-unix-shells.php) : The backstory of all this
* [tutorialspoint.com](https://www.tutorialspoint.com/unix/unix-what-is-shell) : A good introduction to the shell and the basic utilities it has
* [Shell Scripting](https://www.shellscript.sh/) : How to write code in the "bash" programming language


Please take some time before the workshop to read through these.

> ## The bare minimum
>
> Though the essential aspects and "bare minimum" is very subjective, a few of the most basic concepts that you should
> be comfortable with are the following.
> - Navigating files and directories (`pwd`,`ls` and `cd`)
> - Create, copy and delete files and directories (`mkdir`, `touch`, `mv`, `cp` and `rm`)
> - Executing shell scripts (`source script.sh`)
> - Environmental Variables (`echo $ENVVAR`)
>
> You can use this as the "bare minimum" checklist for this bootcamp and you will be expected to be familiar with these concepts throughout the bootcamp.
>
{: .callout}



### Essential C++

Throughout your studies and career in particle physics, you will find a large amount
of your code and software will be written in C++. Within ATLAS for example, the software
is very C++ based and many analysis frameworks are constructed using C++. The problem with
teaching C++ in the context of research is that it is such a broad programming language
that it becomes very difficult to adequately explain "the essential" things that you need to know.
It would be very worth your while to enroll in a formal university level introduction to C++
course and this _will_ pay dividends in your research. Fortunately, there is a large amount of C++
material available and hopefully you can gain some basic understanding of C++ essentials if
you are not familiar already. And for the purposes of this bootcamp, a certain amount of requisite
knowledge is necessary, as highlighted below.  A few good references are :

* [cplusplus.com](http://www.cplusplus.com/doc/tutorial/) : _The_ go-to reference for c++ with a solid tutorial.  <span style="color:red"> **All participants should review this tutorial and ensure they are comfortable with its contents.**</span> If you have questions about whether a particular concept is important or frequently used in HEP, please ask!
* [learncpp](https://www.learncpp.com/) : A more long and drawn out tutorial.  It presents the same thins as [cplusplus.com](http://www.cplusplus.com/doc/tutorial/), but from a different perspective.
* [tutorialspoint.com tutorial](https://www.tutorialspoint.com/cplusplus/) : Another very good reference with tutorials
* [W3School tutorial](https://www.w3schools.com/cpp/) : W3 Schools covers more than just c++ including HTML, Java, etc. as well


> ## The bare minimum
>
> Though the essential aspects and "bare minimum" is very subjective, a few of the most basic concepts that you should
> be comfortable with are the following.
> - Loops : [https://www.tutorialspoint.com/cplusplus/cpp_loop_types](https://www.tutorialspoint.com/cplusplus/cpp_loop_types)
> - Vectors : [https://www.tutorialspoint.com/cpp_standard_library/vector](https://www.tutorialspoint.com/cpp_standard_library/vector)
> - Pointers : [https://www.tutorialspoint.com/cplusplus/cpp_pointers](https://www.tutorialspoint.com/cplusplus/cpp_pointers)
> - Function : [https://www.tutorialspoint.com/cplusplus/cpp_functions](https://www.tutorialspoint.com/cplusplus/cpp_functions)
> - Classes : [https://www.tutorialspoint.com/cplusplus/cpp_classes_objects](https://www.tutorialspoint.com/cplusplus/cpp_classes_objects)
> - Namespaces : [https://www.tutorialspoint.com/cplusplus/cpp_namespaces](https://www.tutorialspoint.com/cplusplus/cpp_namespaces)
> - Inheritance/Polymorphism : [https://www.tutorialspoint.com/cplusplus/cpp_inheritance](https://www.tutorialspoint.com/cplusplus/cpp_inheritance)
>
> You can use this as the "bare minimum" checklist for this bootcamp and you will be expected to be familiar with these concepts throughout the bootcamp.
>
{: .callout}



### Python

[Python](https://www.python.org/) is a popular programming language that runs on an interpreter system.
This means that unlike C++, you do not need to explicitly compile the code prior to running it.  Instead
the code can be executed as soon as it is written. This makes it very appropriate for writing scripts and testing
things quickly.  Python was designed for readability, and has some similarities to the English language with
influence from mathematics (e.g. [sets](https://docs.python.org/2/library/sets.html)). Furthermore, it is possible
to link C++ compiled libraries with python code, allowing you to form an "interface" between the two, thereby
taking advantage of the best of both worlds.

It is rare to not come across Python in some form when working in particle physics and data analysis, particularly
when using advanced techniques in machine learning. In the ATLAS
experiment, python is used in many places, most notably as a mechanism by which we "steer" our C++ code.  This is
done in the form of [jobOptions](https://atlassoftwaredocs.web.cern.ch/ABtutorial/alg_basic_job_options/) or a [steering macro](https://atlassoftwaredocs.web.cern.ch/ABtutorial/alg_basic_macro/).  However, in this tutorial, we will not explicitly be using jobOptions to execute our code.
This is something that is rather left for the [ATLAS software tutorial](https://atlassoftwaredocs.web.cern.ch/ABtutorial/).

Software Carpentry provides a very nice introductory tutorial to python - [Link to Tutorial](http://swcarpentry.github.io/python-novice-inflammation/).
<span style="color:red"> **All participants should review this tutorial and ensure they are comfortable with its contents prior to the bootcamp.**</span>

Beyond this, a few additional resources that are very useful
- [Python3](https://docs.python.org/3/) : Main point of entry for all things python3
- [Python3 Tutorial](https://docs.python.org/3/tutorial/index.html) : Included linked from the page above.  This is the official tutorial.
- [W3School Python Tutorial](https://www.w3schools.com/python/default.asp) : Like C++, W3Schools has their own tutorial. A different perspective.
- [TutorialsPoint Python Tutorial](https://www.tutorialspoint.com/python/) : ... and another perspective.

**MadGraph is written in python, and so being familiar with the syntax will be very useful here!**

### GitHub and GitLab

You may be familiar with Git (if not, you will learn about it from Software Carpentries) and
even have a [Git**Hub**](https://github.com/) account.  Many other equivalent services such
as this, that serve as places where one can house remote repositories exist (e.g. [bitbucket](https://bitbucket.org)
and [atlassian](https://www.atlassian.com/)) and the one that is used at CERN is [GitLab](https://gitlab.cern.ch/).

> ## Log in to GitLab
>
> Confirm that your credentials work properly by logging into [GitLab](https://gitlab.cern.ch/) on
> your web browser.  For this, just use the same username and password that you use for everything else
> CERN-related.
>
> Once you do this, explore around the site a bit.  Fill in your profile information and upload a picture
> to serve as your avatar.
>
{: .challenge}


{% include links.md %}



{% include links.md %}
