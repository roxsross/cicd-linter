FROM ubuntu:22.10
LABEL org.opencontainers.image.vendor="roxsross" \
	 org.opencontainers.image.title="linter" \
 	org.opencontainers.image.description="DevOps environment" 

ENV KUBELINTER_VERSION 0.6.4 
ARG DEBIAN_FRONTEND=noninteractive
SHELL ["/bin/bash", "-euxo", "pipefail", "-c"]

RUN apt-get update && \
    apt-get install -y -qqy \
	wget \
	bash \
	curl \
	unzip && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /tmp/

# hadolint:
ARG HADOLINT_VERSION=2.12.0
RUN curl -OfsSL \
        "https://github.com/hadolint/hadolint/releases/download/v${HADOLINT_VERSION}/hadolint-Linux-x86_64"; \
    install -m 0755 -o root -g root hadolint-Linux-x86_64 /usr/local/bin/hadolint; \
    rm hadolint-Linux-x86_64

# kubelinter:
ARG KUBELINTER_VERSION=0.6.4 
RUN curl -OfsSL \
        "https://github.com/stackrox/kube-linter/releases/download/v0.6.4/kube-linter-linux.tar.gz"; \
		tar -xzf kube-linter-linux.tar.gz ; \
    install -m 0755 -o root -g root kube-linter /usr/local/bin/kube-linter; \
    rm kube-linter

ENV PATH="/home/docs/.local/bin:${PATH}"

WORKDIR /docs

ENTRYPOINT ["/bin/bash", "-c"]
