FROM zikalino/python-sdk-dev
MAINTAINER zikalino

RUN mkdir -p /workspaces/az
RUN cd /workspaces/az; git clone https://github.com/Azure/azure-cli
RUN cd /workspaces/az; git clone https://github.com/Azure/azure-cli-extensions

RUN python3 -m venv env
ENV VIRTUAL_ENV /env
ENV PATH /env/bin:$PATH
RUN pip install azdev

RUN cd /azure-cli-extensions; git pull
RUN cd /azure-cli-extensions; git checkout addin-apimgmt-extension
RUN azdev setup -r /azure-cli-extensions -e apim -c /azure-cli
RUN pip install azure-mgmt-apimanagement
ADD run.sh /run.sh
ENTRYPOINT ["bash", "/run.sh"]
