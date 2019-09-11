ARG SDC_VERSION
FROM streamsets/datacollector:${SDC_VERSION}
#any additional args must go after FROM
ARG SDC_VERSION
ARG PREINSTALL_SDC_LIBS
ARG SDC_BASE_URL
ARG SDC_HTTP_PORT
ARG SDC_HTTPS_PORT
ARG SDC_KEYSTORE_PATH
ARG SDC_KEYSTORE_PASSWORD
#verify the build environment
RUN env
#modify sdc.properties
RUN sed -i "s|#sdc.base.http.url=.*$|sdc.base.http.url=${SDC_BASE_URL}|" /etc/sdc/sdc.properties
RUN sed -i "s|http.port=.*$|http.port=${SDC_HTTP_PORT}|" /etc/sdc/sdc.properties
RUN sed -i "s|https.port=.*$|https.port=${SDC_HTTPS_PORT}|" /etc/sdc/sdc.properties
RUN sed -i "s|https.keystore.path=.*$|https.keystore.path=${SDC_KEYSTORE_PATH}|" /etc/sdc/sdc.properties

#update keystore password
RUN echo -n "${SDC_KEYSTORE_PASSWORD}" > /etc/sdc/keystore-password.txt
#modify sdc-security.policy
RUN sed -i '/file:\/groovy\/script*/apermission java.security.AllPermission;' /etc/sdc/sdc-security.policy
#install stage libraries
RUN "${SDC_DIST}/bin/streamsets" stagelibs -install=${PREINSTALL_SDC_LIBS}
