FROM redmine
RUN apt-get update && \
    apt-get install fontconfig fonts-noto-cjk && \
    wget https://github.com/jgm/pandoc/releases/download/3.12/pandoc-3.12-1-arm64.deb && \
    dpkg -i pandoc-3.12-1-arm64.deb  && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -f pandoc-3.12-1-arm64.deb && \
    fc-cache -fv
COPY ./additional_environment.rb /usr/src/redmine/config/additional_environment.rb
