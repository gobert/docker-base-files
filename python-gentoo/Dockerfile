FROM gobert42/gentoo:latest

SHELL ["/bin/zsh", "-c"]

ENV USER jacques
ENV USER_HOME /home/$USER

USER root

# install pip
RUN emerge dev-python/pip

# add path to pip's binaries to PATH
USER $USER
COPY /python-gentoo/config_files $USER_HOME/config_files
RUN cat $USER_HOME/config_files/home/.zshenv >> $USER_HOME/.zshenv
