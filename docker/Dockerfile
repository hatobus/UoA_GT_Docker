FROM frolvlad/alpine-glibc:latest

ENV PATH /usr/local/texlive/2019/bin/x86_64-linux:$PATH

RUN apk add --no-cache perl fontconfig-dev freetype-dev curl && \
    set -ex; \
    apk add --no-cache --virtual .fetch-deps wget xz tar su-exec curl && \
    mkdir /tmp/install-tl-unx && \
    curl ftp://tug.org/historic/systems/texlive/2019/install-tl-unx.tar.gz | \
    tar -xz -C /tmp/install-tl-unx --strip-components=1 && \
    printf "%s\n" \
      "selected_scheme scheme-basic" \
      "tlpdbopt_install_docfiles 0" \
      "tlpdbopt_install_srcfiles 0" \
      > /tmp/install-tl-unx/texlive.profile && \
    /tmp/install-tl-unx/install-tl \
      --profile=/tmp/install-tl-unx/texlive.profile && \
    tlmgr install \
      collection-latexextra \
      collection-fontsrecommended \
      collection-langjapanese \
      latexmk && \
    rm -fr /tmp/install-tl-unx && \
    apk del .fetch-deps

# install newtxfont
RUN tlmgr info tcolorbox --repository http://mirror.ctan.org/systems/texlive/tlnet/ && \
    tlmgr update --self && \
    tlmgr init-usertree; \
    tlmgr install newtx fontaxes boondox txfonts helvetic kastrup tex-gyre mweights algorithmicx algorithms

WORKDIR /workdir

