FROM perl:threaded
MAINTAINER Harkeet Bajaj <harkeet.bajaj@gmail.com>

RUN curl -L http://cpanmin.us | perl - App::cpanminus

RUN cpanm CPAN::Meta \
 Net::SNMP \
 POSIX \
 strict \
 threads \
 Thread::Queue \
 Thread::Semaphore \
 threads::shared

# Test BP
RUN cpanm warnings \
 Fcntl

RUN perl -MCPAN -e 'CPAN::Shell->install("DBI")'
RUN perl -MCPAN -e 'CPAN::Shell->install("DBD::mysql")'


COPY [ "./MotoPoll.pl", "/usr/local/sbin/MotoPoll.pl" ]
RUN [ "chmod", "+x",  "/usr/local/sbin/MotoPoll.pl" ]

WORKDIR /usr/local/sbin

#CMD [ "perl", "./MotoPoll.pl" ]

ENTRYPOINT ["perl", "MotoPoll.pl"]
