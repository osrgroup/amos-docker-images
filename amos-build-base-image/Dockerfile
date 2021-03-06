#REPO: osrgroup/amos-build-base-image:1.0
#PUSH!
#
# Copyright 2016 The Open Source Research Group,
#                University of Erlangen-Nürnberg
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

FROM ubuntu:14.04

# -------------------------------------- Configure basics

RUN locale-gen en_US.UTF-8 \
  && locale-gen de_DE.UTF-8

ENV LANG        en_US.UTF-8
ENV LANGUAGE    en_US.UTF-8
ENV LC_ALL      en_US.UTF-8

ENV HOME        /root

# -------------------------------------- Update base system

ADD assets/scrub_image /usr/local/bin/scrub_image
RUN chmod +x /usr/local/bin/scrub_image

# Upgrade system
RUN apt-get -y update \
  && apt-get -y upgrade \
  && scrub_image

# Remove rsyslog, phusion uses syslog-ng
RUN apt-get -y purge rsyslog \
  && scrub_image

# Install a set of often needed programs
RUN apt-get -y update \
  && apt-get -y --no-install-recommends install \
    bash-completion man less nano wget curl zip unzip patch git sudo software-properties-common \
  && scrub_image

# -------------------------------------- Done
