FROM ubuntu:20.04

LABEL author="Michael Jochum, Baylor College of Medicine, Houston, TX, USA" \
    maintainer="michael.jochum@bcm.edu"
RUN apt-get update && apt-get install -y tzdata
RUN DEBIAN_FRONTEND="noninteractive"
RUN apt-get -y install \
    build-essential \
    wget \
    tar \
    unzip \
    bzip2 \
	cmake \
	zlib1g-dev  \
	bzip2 \
	libghc-bzlib-dev \
	liblzma-dev  \
	libncurses5-dev \
    libhts-dev \
    libtbb-dev \
    autoconf

# Tool versions:
ENV BOWTIE2_VERSION 2.4.1
ENV SAMTOOLS_VERSION 1.10

#Install Bowtie2:
RUN cd /usr/local/ \
    && wget -O bowtie2.zip \
    https://github.com/BenLangmead/bowtie2/releases/download/v${BOWTIE2_VERSION}/bowtie2-${BOWTIE2_VERSION}-linux-x86_64.zip \
	&& unzip bowtie2.zip \
	&& rm bowtie2.zip \
	&& mv bowtie2* bowtie2
ENV PATH="/usr/local/bowtie2/:${PATH}"

# Install samtools:
RUN cd /usr/local/ \
    && wget -O samtools.tar.bz2 \
    https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VERSION}/samtools-${SAMTOOLS_VERSION}.tar.bz2 \
	&& tar -jxf samtools.tar.bz2 \
	&& rm samtools.tar.bz2 \
	&& mv samtools* samtools \
	&& cd samtools \
    && autoheader \
    && autoconf -Wno-syntax \
    && ./configure \
	&& make \
	&& make install
ENV PATH="/usr/local/samtools/:${PATH}"

