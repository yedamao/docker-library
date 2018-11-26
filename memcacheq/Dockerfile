FROM alpine:3.6

COPY start_memcacheq.sh /start_memcacheq.sh

RUN echo "==> Installing dependencies..." \
&& apk update \
&& apk add --virtual build-deps \
binutils gcc make git autoconf automake musl-dev \
&& apk add libevent-dev db-dev

RUN echo "==> clone memcacheq from github..." \
&& cd /tmp && git clone https://github.com/stvchu/memcacheq.git \
&& echo "==> build memcacheq ...." \
&& cd /tmp/memcacheq \
&& ./autogen.sh && ./configure CC='gcc -std=gnu89' && make && make install \
&& echo "==> cleaning ...." \
&& apk del build-deps && cd / && rm -rf /tmp/*

EXPOSE 22201

CMD ["sh", "/start_memcacheq.sh"]
