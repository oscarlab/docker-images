# Rolling forward to 18.04
FROM ubuntu:18.04

SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND noninteractive

# Add Node.js v10 APT repo

RUN apt-get clean
RUN apt-get update
RUN apt-get install -y curl gnupg

RUN curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -

RUN sh -c "echo deb https://deb.nodesource.com/node_10.x bionic main > /etc/apt/sources.list.d/nodesource.list"

# Packages needed to build filesystem and run xfstests
RUN apt-get clean
RUN apt-get update
RUN apt-get install -y                      \
		       automake             \
		       autoconf             \
		       build-essential      \
		       cmake                \
		       debhelper            \
		       gcc                  \
    	    	       git                  \
		       libaio-dev           \
		       libcurl4-openssl-dev \
		       libprotobuf-dev      \
		       libssl-dev           \
		       libtool              \
		       libxxhash-dev        \
		       make                 \
		       nodejs               \
		       ocaml                \
		       ocamlbuild           \
		       perl                 \
		       protobuf-compiler    \
		       python               \
		       reprepro             \
		       sysstat              \
		       unzip                \
		       wget

# Install SGX SDK
RUN git clone https://github.com/intel/linux-sgx.git
RUN cd linux-sgx && git checkout sgx_2.12
RUN cd linux-sgx && make preparation && cp external/toolset/ubuntu18.04/* /usr/local/bin
RUN cd linux-sgx && make sdk_install_pkg
RUN ./linux-sgx/linux/installer/bin/sgx_linux_x64_sdk_2.12.100.3.bin --prefix /opt/intel

# (a) Install PSW
# RUN cd linux-sgx && make deb_psw_pkg
# RUN dpkg -i linux-sgx/linux/installer/deb/libsgx-headers/*.deb
# RUN dpkg -i linux-sgx/linux/installer/deb/libsgx-enclave-common/*.deb
# RUN dpkg -i linux-sgx/linux/installer/deb/libsgx-urts/*.deb
# RUN dpkg -i linux-sgx/linux/installer/deb/libsgx-epid/*.deb
# RUN dpkg -i linux-sgx/linux/installer/deb/libsgx-launch/*.deb
# RUN dpkg -i linux-sgx/linux/installer/deb/libsgx-quote-ex/*.deb
# RUN dpkg -i linux-sgx/linux/installer/deb/libsgx-uae-service/*.deb

# Install SGX SSL Library
RUN git clone https://github.com/intel/intel-sgx-ssl.git
RUN cd intel-sgx-ssl/openssl_source && wget https://github.com/openssl/openssl/releases/download/openssl-3.0.13/openssl-3.0.13.tar.gz
RUN cd intel-sgx-ssl/Linux && source /opt/intel/sgxsdk/environment && make all && make install

CMD ["bash"]
