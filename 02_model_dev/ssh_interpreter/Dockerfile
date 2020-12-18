FROM ubuntu

RUN apt-get update

# we're going to run a Python application
RUN apt-get install -y python3.5

# configure an SSH server in case we want to debug something
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:changeme' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
EXPOSE 22

# add our stuff
ADD . /var/stuff

WORKDIR /var/stuff

CMD [ "bash", "wrapper.sh" ]
