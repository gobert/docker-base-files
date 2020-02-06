FROM gentoo/stage3-amd64-hardened:latest

ENV USER jacques

#
# UPDATE GENTOO CONFIG
###############################################################################
COPY /gentoo/config_files /root/config_files
RUN mkdir /etc/portage/profile

# portage
RUN cat /root/config_files/etc/portage/make.conf >> /etc/portage/make.conf
RUN cp -r /root/config_files/etc/portage/package.use /etc/portage/
RUN cp -r /root/config_files/etc/portage/profile/use.stable.mask /etc/portage/profile/use.stable.mask
# use python3
RUN cp -r /root/config_files/etc/portage/package.accept_keywords /etc/portage/package.accept_keywords

# locale
RUN cat /root/config_files/etc/env.d/02locale >> /etc/env.d/02locale
RUN cat /root/config_files/etc/locale.gen >> /etc/locale.gen

#
# SETUP OS
###############################################################################

# UTF-8
RUN localedef -i fr_FR -f UTF-8 fr_FR.UTF-8
RUN locale-gen

# update dependencies & systen
RUN emerge --sync
RUN emerge -vuDN --with-bdeps y --keep-going world

# install system tools
RUN emerge \
  app-shells/zsh app-shells/zsh-completions app-shells/gentoo-zsh-completions \
  dev-vcs/git \
  sys-apps/shadow

SHELL ["/bin/zsh", "-c"]

# now that git is installed, update with git
RUN cp -r /root/config_files/etc/portage/repos.conf /etc/portage/
RUN rm -rf /var/db/repos/gentoo
RUN mkdir /var/db/repos/gentoo
RUN emerge --sync

#
# SETUP USER ACCOUNT
###############################################################################

RUN useradd -m -G users -s /bin/zsh $USER

USER $USER

# install oh-my-zsh for user
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

USER root

RUN cat /root/config_files/home/.zshrc >> /home/$USER/.zshrc
RUN chown $USER:$USER /home/$USER/.zshrc

#
# SETUP ROOT ACCOUNT
###############################################################################

# use zsh also for root
RUN chsh root -s /bin/zsh

#
# CLEANUP
###############################################################################

# delete things we don't need anymore
RUN emerge -c sys-apps/shadow
RUN emerge -v --depclean
