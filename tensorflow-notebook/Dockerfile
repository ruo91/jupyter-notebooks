FROM centos/python-36-centos7:latest
USER root

ADD .s2i /tmp/src/.s2i
ADD Dockerfile /tmp/src/Dockerfiles
ADD requirements.txt /tmp/src/requirements.txt
ADD facets.tar.gz /tmp
RUN chown -R 1001:1001 /tmp/facets

RUN rm -rf /tmp/src/.git* && \
    chown -R 1001 /tmp/src && \
    chgrp -R 0 /tmp/src && \
    chmod -R g+w /tmp/src && \
    rm -rf /tmp/scripts && \
    mv /tmp/src/.s2i/bin /tmp/scripts

ENV XDG_CACHE_HOME=/opt/app-root/src/.cache

USER 1001
RUN /tmp/scripts/assemble

CMD [ "/opt/app-root/builder/run" ]
