FROM opnfv/functest-core:euphrates  
  
ARG BRANCH=stable/euphrates  
ARG OPENSTACK_TAG=stable/ocata  
ARG ODL_TAG=e12ba90cd27577c4c6c70ee54f7d599b5f6777ba  
ARG FDS_TAG=stable/euphrates  
ARG REFSTACK_TAG=4e187b07672dd1c41cb7c94658f1c91edebf53a2  
  
RUN apk --no-cache add --virtual .build-deps \--update \  
python-dev build-base linux-headers libffi-dev \  
openssl-dev libjpeg-turbo-dev git && \  
git clone --depth 1 https://github.com/openstack/refstack-client.git
/src/refstack-client && \  
(cd src/refstack-client && git checkout -b $REFSTACK_TAG) && \  
update-requirements -s --source /src/openstack-requirements /src/refstack-
client/ && \  
pip install --no-cache-dir --src /src \  
-chttps://git.openstack.org/cgit/openstack/requirements/plain/upper-constraints.txt?h=$OPENSTACK_TAG \  
-chttps://git.opnfv.org/functest/plain/upper-constraints.txt?h=$BRANCH \  
-e/src/refstack-client && \  
git clone --depth 1 https://git.opendaylight.org/gerrit/p/integration/test.git
/src/odl_test && \  
(cd src/odl_test && git checkout -b $ODL_TAG) && \  
git clone --depth 1 -b $FDS_TAG https://gerrit.opnfv.org/gerrit/fds /src/fds
&& \  
ln -s /src/tempest /src/refstack-client/.tempest && \  
virtualenv --system-site-packages /src/tempest/.venv && \  
rm -r /src/refstack-client/.git /src/odl_test/.git /src/fds/.git && \  
apk del .build-deps  
COPY testcases.yaml /usr/lib/python2.7/site-
packages/functest/ci/testcases.yaml  
CMD ["bash","-c","prepare_env start && run_tests -t all"]  

