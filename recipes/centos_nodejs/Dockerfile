# Copyright (c) 2012-2018 Red Hat, Inc.
# This program and the accompanying materials are made
# available under the terms of the Eclipse Public License 2.0
# which is available at https://www.eclipse.org/legal/epl-2.0/
#
# SPDX-License-Identifier: EPL-2.0
#
# Contributors:
#   Red Hat, Inc. - initial API and implementation
#   Dharmit Shah <dshah@redhat.com>
#   Maxime Clerix <mclerix@redhat.com>

FROM registry.centos.org/che-stacks/centos-stack-base

ARG OC_VERSION=3.11.16

EXPOSE 1337 3000 4200 5000 9000 8003 4243 4403 8080 8000 22
LABEL che:server:8003:ref=angular che:server:8003:protocol=http che:server:3000:ref=node-3000 che:server:3000:protocol=http che:server:9000:ref=node-9000 che:server:9000:protocol=http

RUN sudo yum update -y && \
    sudo yum -y install rh-nodejs6 tar curl wget && \
    sudo yum -y clean all && \
    sudo ln -s /opt/rh/rh-nodejs6/root/usr/bin/node /usr/local/bin/nodejs && \
    sudo scl enable rh-nodejs6 'npm install --unsafe-perm -g gulp bower grunt grunt-cli yeoman-generator yo generator-angular generator-karma generator-webapp' && \
    cat /opt/rh/rh-nodejs6/enable >> /home/user/.bashrc && \
    sudo wget -qO- "https://mirror.openshift.com/pub/openshift-v3/clients/${OC_VERSION}/linux/oc.tar.gz" | sudo tar xvz -C /usr/local/bin

# Install jq
RUN sudo yum install -y epel-release && \
    sudo yum install -y jq

# Install Ansible
RUN sudo yum install -y ansible

# Install Openshift DO (ODO)
RUN sudo curl -L https://github.com/redhat-developer/odo/releases/download/v0.0.13/odo-linux-amd64 -o /usr/local/bin/odo && \
    sudo chmod +x /usr/local/bin/odo

ENV PATH=/opt/rh/rh-nodejs6/root/usr/bin${PATH:+:${PATH}}
ENV LD_LIBRARY_PATH=/opt/rh/rh-nodejs6/root/usr/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
ENV PYTHONPATH=/opt/rh/rh-nodejs6/root/usr/lib/python2.7/site-packages${PYTHONPATH:+:${PYTHONPATH}}
ENV MANPATH=/opt/rh/rh-nodejs6/root/usr/share/man:$MANPATH
