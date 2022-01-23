FROM image-registry.openshift-image-registry.svc:5000/common/gcc:11.2.0 AS BUILD
WORKDIR /tmp/workdir/
COPY . .
RUN gcc -c -Wall -Werror -pthread -O2 -o main.o main.c && \
    gcc -o main main.o -pthread && \
    chmod 0770 main

FROM image-registry.openshift-image-registry.svc:5000/common/ubi8-minimal:8.5
COPY --from=BUILD --chown=0:0 /tmp/workdir/main /main
USER 1001:0
WORKDIR /
ENTRYPOINT ["/main"]
