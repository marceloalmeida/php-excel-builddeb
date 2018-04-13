FROM marceloalmeida/php-docker:7.0

LABEL maintainer="Marcelo Almeida <marcelo.almeida@jumia.com>"

WORKDIR "/root"

ENV \
  DEBIAN_FRONTEND="noninteractive" \
  VERSION="1.0.2" \
  LIBXL_VERSION="3.8.2"

# INSTALL BUILDER DEPENDENCIES
RUN apt-get update && apt-get install -y --no-install-recommends \
  apt-utils \
  build-essential \
  ca-certificates \
  checkinstall \
  lsb-release \
  make \
  php7.0-dev \
  re2c \
  runawk \
  wget

COPY src /src

# INSTALL PACKAGES DEPENDENCIES
RUN mkdir -p /pkg && \
  mkdir -p "/opt/libxl-${LIBXL_VERSION}" && \ 
  wget -qO- "http://www.libxl.com/download/libxl-lin-${LIBXL_VERSION}.tar.gz" | tar xvz -C "/opt/libxl-${LIBXL_VERSION}" --strip=1

# CREATE PACKAGE
RUN wget -qO- https://github.com/iliaal/php_excel/releases/download/Excel-${VERSION}-PHP7/excel-${VERSION}-php7.tgz | tar zxv && \
  cd excel-$VERSION && \
  cp -r /src/* /root/excel-$VERSION/. && \
  phpize && \
  ./configure --with-libxl-incdir="/opt/libxl-${LIBXL_VERSION}/include_c/" --with-libxl-libdir="/opt/libxl-${LIBXL_VERSION}/lib64/" --with-excel=shared && \
  checkinstall -y --install=no --pkgname='php7.0-excel' --pkgversion='$VERSION' --pkggroup='php' --pkgsource='https://github.com/iliaal/php_excel' --maintainer='Marcelo Almeida \<marcelo.almeida@jumia.com\>' --requires='php7.0-common, libxl \(\>= 2.8.2\)' --include=include_etc

VOLUME ["/pkg"]
