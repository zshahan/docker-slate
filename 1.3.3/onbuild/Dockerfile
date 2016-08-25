FROM            nginx:mainline-alpine

ENV             VERSION=1.3.3

COPY            staticfiles.conf /etc/nginx/conf.d/
RUN             rm -rf /usr/share/nginx/html/*

ONBUILD COPY    source/ /tmp/slate/source/
ONBUILD RUN     mkdir -p /opt/src/ && cd /opt/src && \
                apk --no-cache add --virtual .build-deps \
                    build-base \
                    curl \
                    ruby-dev \
                    ruby-bundler \
                    ruby-io-console \
                    nodejs \
                    libxml2-dev \
                    libxslt-dev \
                    linux-headers \
                    libffi-dev \
                    zlib-dev && \
                curl -L https://github.com/lord/slate/archive/v$VERSION.tar.gz | tar -xz && \
                cd slate-$VERSION && \
                mkdir -p /tmp/slate/source/ && \
                cp -R /tmp/slate/source/* source/ && \
                export BUNDLE_SILENCE_ROOT_WARNING=1 && \
                bundle config build.nokogiri --use-system-libraries && \
                bundle install && \
                bundle exec middleman build --clean && \
                rm -rf /usr/share/nginx/html/ && \
                cp -R build /usr/share/nginx/html && \
                apk del .build-deps && \
                rm -rf /opt/src /tmp/slate
