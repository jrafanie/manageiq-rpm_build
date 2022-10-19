FROM registry.access.redhat.com/ubi9/ubi

ENV TERM=xterm \
    RPM_SPEC=repmgr.spec

RUN ARCH=$(uname -m) && \
    # TODO figure out s390x
    dnf -y remove *subscription-manager* && \
    dnf -y update && \
    dnf -y install \
      http://mirror.stream.centos.org/9-stream/BaseOS/${ARCH}/os/Packages/centos-stream-repos-9.0-18.el9.noarch.rpm \
      http://mirror.stream.centos.org/9-stream/BaseOS/${ARCH}/os/Packages/centos-gpg-keys-9.0-18.el9.noarch.rpm \
      https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm && \
    dnf -y group install "development tools" && \
    dnf -y install --enablerepo=crb \
      ccache \
      clang-devel \
      flex \
      libxslt-devel \
      llvm-toolset \
      openssl-devel \
      pam-devel \
      postgresql \
      postgresql-server-devel \
      postgresql-static \
      readline-devel \
      wget && \
    dnf clean all && \
    rm -rf /var/cache/dnf

COPY . /root

ENTRYPOINT ["/root/container-assets/build.sh"]
