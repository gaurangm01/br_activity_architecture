
## Installation

Steps for library creation

**Step 1:** Install libraries for creation and publishing of cusotm libraries 

```bash
pip install wheel
pip install setuptools
pip install twine
```

**Step 2:** Create a library which will have custom functions to be utilised(You can check the implemenation in repository for setup file and functionality)

**Step 3:** Convert into wheel file

```bash
python setup.py bdist_wheel
```

**Step 4:** Start a private PyPI Server
```bash
# docker-compose.yaml

version: '3.7'

services:
  pypi-server:
    image: pypiserver/pypiserver:latest
    ports:
      - 8080:8080
    command: -P . -a . /data/packages
    restart: always
    volumes:
      - pypi-server:/data

volumes:
  pypi-server:
```


```bash
docker-compose up -d --build
```

**Step 5:** Upload package to private PyPI Server
```bash
twine upload --repository-url http://<IP-ADDRESS>:8080 dist/*
```

**Step 6:** Download Package in other project 
```bash
pip install --index-url http://<IP-ADDRESS>:8080 <PACKAGE NAME> --trusted-host <PUBLIC-IP-ADDRESS>
```