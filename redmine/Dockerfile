FROM redmine
ARG TARGETARCH
RUN apt-get update && \
    apt-get install -y \
    fonts-noto-cjk \
    fontconfig && \
    rm -rf /var/lib/apt/lists/* && \
    fc-cache -fv && \
    case "$TARGETARCH" in \
      amd64|arm64) \
        wget https://github.com/jgm/pandoc/releases/download/3.10.1/pandoc-3.10.1-1-${TARGETARCH}.deb; \
        dpkg -i pandoc-3.10.1-1-${TARGETARCH}.deb;; \
      *) \
        ;; \
    esac && \
    apt-get clean
COPY ./additional_environment.rb /usr/src/redmine/config/additional_environment.rb
COPY ./configuration.yml /usr/src/redmine/config/configuration.yml
