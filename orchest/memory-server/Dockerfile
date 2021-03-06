FROM python:3.7-slim

# Install git, because it is not included in the python-slim image.
RUN apt-get update \
    && apt-get install -y --no-install-recommends git \
    && apt-get purge -y --auto-remove \
    && rm -rf /var/lib/apt/lists/*

# We can simply copy the entire build context, because in the 
# dockerignore we specified precisely what we want to include in the
# image.
COPY ./ /orchest/

WORKDIR /orchest/orchest/memory-server
RUN pip3 install -r requirements.txt

# Since we want to be able to specify the SDK branch, we have to manually
# install that too. Overwriting the default master branch from the 
# requirements.txt
ARG sdk_branch=master
RUN pip3 install git+https://github.com/orchest/orchest-sdk.git@${sdk_branch}#subdirectory=python

CMD ["python", "app/main.py"]
