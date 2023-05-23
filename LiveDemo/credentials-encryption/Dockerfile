FROM debian:bullseye-20230502-slim
RUN  apt-get update \
  && apt-get install -y wget \
  && apt-get install -y vim \
  && apt-get install -y gnupg \
  && wget https://github.com/mozilla/sops/releases/download/v3.7.3/sops-v3.7.3.linux.arm64 \
  && mv sops-v3.7.3.linux.arm64 /usr/local/bin/sops \
  && chmod 111 /usr/local/bin/sops
COPY *.yaml /config/
COPY *.pub /gpg-keys/
RUN gpg --import /gpg-keys/*

CMD ["/bin/bash"]