FROM debian:latest

MAINTAINER vance@hackthefed.org

ENV PYTHONUNBUFFERED 1
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get upgrade -y

# Set locale to US EN UTF8
RUN apt-get install locales -y && \
    sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen && \
    locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
RUN dpkg-reconfigure locales


RUN apt-get install -y mercurial git vim tmux
RUN apt-get install -y ncurses-dev wget curl

# Get our python toolset
RUN apt-get install -y python3 python3-pip python3-matplotlib python3-pillow
RUN apt-get install -y liblapack-dev libblas-dev hdf5-tools python3-tables
RUN apt-get install -y gfortran

COPY ./requirements.txt requirements.txt

RUN pip3 install  -r requirements.txt

VOLUME /data

EXPOSE 8888

CMD sh -c "/usr/local/bin/jupyter notebook --ip=0.0.0.0 --no-browser --notebook-dir=/data"
