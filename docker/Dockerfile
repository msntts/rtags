FROM centos:8

RUN dnf install -y make cmake clang clang-devel llvm-devel git which zlib-devel openssl-devel vim && \
    mkdir bear && cd bear && \
    curl -s -L https://download-ib01.fedoraproject.org/pub/fedora/linux/releases/32/Everything/x86_64/os/Packages/b/bear-2.4.3-2.fc32.x86_64.rpm --output bear.rpm && \
    dnf install -y bear.rpm && \
    dnf clean all

RUN git clone --recursive https://github.com/Andersbakken/rtags.git && \
    cd rtags && \
    mkdir build && cd build && \
    cmake -DLIBCLANG_LLVM_CONFIG_EXECUTABLE=$(which llvm-config) .. && \
    make -j$(grep processor /proc/cpuinfo | wc -l) && \
    make install && \
    cd ../../ && rm -rf rtags

ADD setup-vim-rtags.sh /root/setup-vim-rtags.sh
RUN chmod +x /root/setup-vim-rtags.sh && \
    /root/setup-vim-rtags.sh
