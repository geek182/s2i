# lighttpd-centos7
FROM openshift/base-centos7

# TODO: Put the maintainer name in the image metadata
LABEL maintainer="Leandro Azevedo geek182@gmail.com"

# TODO: Rename the builder environment variable to inform users about application you provide them
ENV LIGHTTPD_VERSION=1.4.35 

# TODO: Set labels used in OpenShift to describe the builder image
LABEL io.k8s.description="Platform for serving static HTML files" \
      io.k8s.display-name="Lighttpd 1.4.35" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,html,lighttpd"

# TODO: Install required packages here:
# RUN yum install -y ... && yum clean all -y
RUN wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && rpm -ivh epel-release-latest-7.noarch.rpm
RUN yum install -y lighttpd && \
    # clean yum cache files, as they are not needed and will only make the image bigger in the end
        yum clean all -y

# TODO (optional): Copy the builder files into /opt/app-root
# COPY ./<builder_folder>/ /opt/app-root/

# TODO: Copy the S2I scripts to /usr/libexec/s2i, since openshift/base-centos7 image
# sets io.openshift.s2i.scripts-url label that way, or update that label
COPY ./s2i/bin/ /usr/libexec/s2i

# Copy the lighttpd configuration file
COPY ./etc/ /opt/app-root/etc

# TODO: Drop the root user and make the content of /opt/app-root owned by user 1001
RUN chown -R 1001:1001 /opt/app-root

# This default user is created in the openshift/base-centos7 image
USER 1001

# TODO: Set the default port for applications built using this image
EXPOSE 8080

# TODO: Set the default CMD for the image
CMD ["/usr/libexec/s2i/usage"]
