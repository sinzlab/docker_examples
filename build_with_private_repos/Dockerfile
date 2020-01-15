FROM sinzlab/pytorch as intermediate
    

# use ssh key
WORKDIR /

# Copy your private key from the context
COPY .ssh/private.pem .
# Register that private key and use it to clone private repositories
RUN eval $(ssh-agent) && \
    ssh-add private.pem && \
    ssh-keyscan -H github.com >> /etc/ssh/ssh_known_hosts && \
    git clone git@github.com:sinzlab/nnfabrik /src/nnfabrik && \
    git clone git@github.com:sinzlab/ml-utils /src/ml-utils && \
    git clone git@github.com:sinzlab/mei /src/mei

# Now start another stage of build
FROM sinzlab/pytorch

# ...and only copy the cloned repository from the first image
# into this new image, leaving behind any SSH keys
COPY --from=intermediate /src /src
WORKDIR /src
RUN pip install -e ./ml-utils && \
    pip install -e ./nnfabrik && \
    pip install -e ./mei

# ...continue with any other steps of your build
