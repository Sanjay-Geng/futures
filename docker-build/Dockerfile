FROM centos:centos7

#simhei.ttf  pyfile
RUN mkdir /opt/files
COPY files/* /opt/files/

RUN yum install -y python36-devel \
 &&  yum install libtiff-devel libjpeg-devel libzip-devel freetype-devel lcms2-devel libwebp-devel tcl-devel tk-devel -y \
 && yum install wget gcc bzip2 fontconfig  mkfontscale -y \
 && useradd future \
 && cd /home/future \
 && wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 \
 && bzip2 -d phantomjs-2.1.1-linux-x86_64.tar.bz2 \
 && tar xf phantomjs-2.1.1-linux-x86_64.tar \
 && mv phantomjs-2.1.1-linux-x86_64 /usr/local/phantomjs \
 && ln -s /usr/local/phantomjs/bin/phantomjs /usr/bin/ \
 && rm -rf phantomjs* \
 && mkdir /usr/share/fonts/chinese \
 && cp /opt/files/simhei.ttf /usr/share/fonts/chinese/ \
 && chmod -R 755 /usr/share/fonts/chinese \
 && cd /usr/share/fonts/chinese \
 && mkfontscale \
 && mkfontdir \
 && fc-cache \
 && cp /opt/files/schedule_future.py /home/future/ \
 && chown future:future /home/future/schedule_future.py \
 && rm -rf /opt/files


USER future
RUN pip3 install --user --default-timeout=1000 schedule \
 && pip3 install --user --default-timeout=1000 selenium==3.8.0 \
 && pip3 install --user --default-timeout=1000 requests \
 && pip3 install --user --default-timeout=1000 pillow --no-cache-dir -i https://pypi.doubanio.com/simple/ \
 && echo "export LC_ALL=en_US.UTF-8" >> ~/.bashrc \
 && echo "export LANG=en_US.UTF-8" >>  ~/.bashrc 

WORKDIR /home/future
