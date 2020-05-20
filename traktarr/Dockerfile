FROM python:3.7-alpine3.10

ENV TRAKTARR_VERSION 1.2.5

ENV \
  APP_DIR=traktarr \
  TRAKTARR_CONFIG=/config/config.json \
  TRAKTARR_CACHEFILE=/config/cache.db \
  TRAKTARR_LOGFILE=/config/traktarr.log

RUN apk add wget tar

RUN DIR=$(mktemp -d) && cd ${DIR}
RUN wget -q -O ${TRAKTARR_VERSION}.tar.gz https://github.com/l3uddz/traktarr/archive/${TRAKTARR_VERSION}.tar.gz
RUN tar -zxvf ${TRAKTARR_VERSION}.tar.gz && rm ${TRAKTARR_VERSION}.tar.gz
RUN mv traktarr-${TRAKTARR_VERSION} /${APP_DIR}
RUN rm -rf ${DIR}

RUN \
  apk --no-cache -U upgrade && \
  echo "** Install PIP dependencies **" && \
  pip install --no-cache-dir --upgrade pip setuptools && \
  pip install --no-cache-dir --upgrade -r /${APP_DIR}/requirements.txt

# Change directory
WORKDIR /${APP_DIR}

# Entrypoint
CMD ["python", "traktarr.py", "run", "--run-now"]
