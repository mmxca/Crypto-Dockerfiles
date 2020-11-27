FROM ubuntu

RUN apt-get update

ENV LC_ALL en_US.UTF-8

ENV WALLET=bitcoin
ENV WALLET_VERSION=0.20.1
ENV WALLET_PORT=8333
ENV WALLET_RPC_PORT=8332

RUN apt-get -y install wget vim unzip

RUN adduser --disabled-password --home /${WALLET} --gecos "" ${WALLET}
RUN echo "${WALLET} ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

WORKDIR /usr/local/src
RUN wget https://${WALLET}core.org/bin/${WALLET}-core-${WALLET_VERSION}/${WALLET}-${WALLET_VERSION}-x86_64-linux-gnu.tar.gz
RUN tar -xzvf ${WALLET}-${WALLET_VERSION}-x86_64-linux-gnu.tar.gz
RUN chmod +x ${WALLET}-${WALLET_VERSION}/bin/${WALLET}d ${WALLET}-${WALLET_VERSION}/bin/${WALLET}-cli
RUN ln -s /usr/local/src/${WALLET}-${WALLET_VERSION}/bin/${WALLET}d /usr/local/bin/${WALLET}d
RUN ln -s /usr/local/src/${WALLET}-${WALLET_VERSION}/bin/${WALLET}-cli /usr/local/bin/${WALLET}-cli

RUN mkdir  /${WALLET}/.${WALLET} 
RUN chown -R ${WALLET}:${WALLET} /${WALLET}/.${WALLET}

USER ${WALLET}
ENV HOME /${WALLET}
WORKDIR /${WALLET}

RUN mkdir /${WALLET}/data
VOLUME /${WALLET}/data

EXPOSE ${WALLET_RPC_PORT} ${WALLET_PORT}

CMD ["${WALLET}d"]