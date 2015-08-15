Docker Images
=============

General Notes
-------------
I like to use docker as a development tool. It keeps my base system clean and
since I run linux I don't see a performance hit. The images in this repo are
built with that in mind.  The python-datakit image should be fine to use on
lesser OS's that use technologies like boot2docker since it operates on
relatively small data sets.

This directory is organized by docker image. For each image there is a folder
and docker-compose file. The folder contains the  `Dockerfile` plus configs,
the compose file is a shortcut for running it. If you aren't familiar with
docker-compose go read stuff here https://docs.docker.com/compose/.  I'm lazy
so I run the compose files and they are tuned to how I have the HackTheFed
organized. The here is how that looks

::

hackthefed/
    data/
    govtrack2csv/S
    docker/

All that really means is that the data directory is at the same level as the
docker directory, so mounting it always looks like ../data:/data . You can do
whatever you like.



python-datakit
--------------
This image is intended for working with data that has been converted to CSV.
It contains the basic data-science toolkit needed to analyze csv's.
The image itself is not specific to the hackthefed project and can be used to
work with any filesystem based dataset. I may add database drivers etc later,
but I don't need them right now and haven't decided on which toolset I'll use
yet so they aren't there right now.

**Contents**

    * Python 3
    * Pandas
    * SciPy
    * NumPy
    * Pillow
    * ipython[all] - This includes notebook and matplotlib
    * pyYAML
    * rodeo - cause it looks interesting
    * zsh and oh-my-zsh

**Usage**

The image comes with ipython notebook installed and it's generally good idea to
mount a dataset into the container, but you don't need to use or do either. The
below commands do both.

Run by hand:

``docker run -it  -v ../data:/data -p 8888:8888 hackthefed/python-datakit /usr/local/bin/ipython notebook --ip=0.0.0.0``

Be lazy about it:

``docker-compose -f python-datakit up -d``

Now you can point your browser to http://<REPLACE WITH YOUR IP>:8888/ and
there will be ipython notebook. Or whatever unmemerable thing they call it
these days.
