FROM debian:stable as builder

WORKDIR /tmp

RUN apt-get update && apt-get install -y \
  curl \
  unzip

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip

FROM node:20.2.0-bullseye

# Type the pcluster version you want to use
ENV PCLUSTER_VERSION=3.6.0

COPY --from=builder /tmp/aws /tmp/aws
RUN /tmp/aws/install
RUN apt-get update && apt-get install -y \
  python3=3.9.2-3 \
  python3-pip \
  git \
  jq \
  fish \
  vim \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN pip3 install aws-parallelcluster==$PCLUSTER_VERSION \
  && mkdir /work