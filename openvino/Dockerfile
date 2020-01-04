FROM ubuntu:16.04
ENV http_proxy $HTTP_PROXY
ENV https_proxy $HTTP_PROXY
ARG DOWNLOAD_LINK=https://7meerkat-openvino.s3.ap-northeast-2.amazonaws.com/openvino_v3.1.tgz
ARG INSTALL_DIR=/opt/intel/openvino
ARG TEMP_DIR=/tmp/openvino_installer
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    cpio \
    lsb-release \
    python3-pip \
    libnuma1 \
    ocl-icd-libopencl1 && \
    rm -rf /var/lib/apt/lists/*
RUN mkdir -p $TEMP_DIR && cd $TEMP_DIR && \
    wget -c $DOWNLOAD_LINK --no-check-certificate && \
    tar xf openvino_*.tgz && \
    cd l_openvino_* && \
    sed -i 's/decline/accept/g' silent.cfg && \
    ./install.sh -s silent.cfg && \
    rm -rf $TEMP_DIR
RUN $INSTALL_DIR/install_dependencies/install_openvino_dependencies.sh
RUN cd $INSTALL_DIR/install_dependencies && ./install_NEO_OCL_driver.sh
RUN useradd -G video -ms /bin/bash user
RUN apt update && apt install -y libpython3.5

ENV INSTALLDIR=/opt/intel/openvino
ENV HDDL_INSTALL_DIR=$INSTALLDIR/deployment_tools/inference_engine/external/hddl
ENV IE_PLUGINS_PATH=$INSTALLDIR/deployment_tools/inference_engine/lib/intel64
ENV LD_LIBRARY_PATH=/opt/intel/opencl:$HDDL_INSTALL_DIR/lib:$INSTALLDIR/deployment_tools/inference_engine/external/gna/lib:$INSTALLDIR/deployment_tools/inference_engine/external/mkltiny_lnx/lib:$INSTALLDIR/deployment_tools/inference_engine/external/tbb/lib:$IE_PLUGINS_PATH:$LD_LIBRARY_PATH
