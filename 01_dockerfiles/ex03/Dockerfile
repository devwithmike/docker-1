FROM ubuntu:16.04

RUN apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
      ca-certificates \
      openssh-server \
      curl \
      postfix

WORKDIR /
RUN curl -LO https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh

RUN bash script.deb.sh

RUN EXTERNAL_URL="http://gitlab.example.com" apt-get install -yq gitlab-ce

RUN apt install -yq tzdata && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22 80

ADD https://gist.githubusercontent.com/rizkyario/bc236974f3b0c9ce60cdb722bf12a702/raw/634df1395ab9c4187250b81d1c4a38e7e0934779/gitlab-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

CMD [ "bash", "/entrypoint.sh" ]

#docker build -t gitlabed .
#docker run -it --rm -p 80:80 -p 21:22 --privileged gitlabed
