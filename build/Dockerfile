FROM ubuntu:22.04
RUN apt-get update -y && apt install -y tzdata
ENV TZ Asia/Ho_Chi_Minh
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt install -y curl expect && curl -o /tmp/Nessus.deb -L "https://www.tenable.com/downloads/api/v1/public/pages/nessus/downloads/16496/download?i_agree_to_tenable_license_agreement=true" && \
  apt install -y /tmp/*.deb && rm -f /tmp/Nessus.deb

ADD adduser.expect /tmp/adduser.expect
RUN cd /tmp && expect -f /tmp/adduser.expect && rm -rf /tmp/adduser.expect

CMD /etc/init.d/nessusd start && sleep 1m && (while ps ax | grep -v grep | grep nessus-service; do sleep 1m; done)
