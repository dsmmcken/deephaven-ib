ARG VERSION

FROM ghcr.io/deephaven/server:${VERSION}

ARG DH_IB_VERSION
ARG DH_IB_BRANCH

# Install requirements
RUN apt update && \
    apt install --yes git python3-venv make && \
    python3 -m pip install --upgrade pip && \
    python3 -m pip install --upgrade setuptools wheel build twine sphinx sphinx-autodoc-typehints furo

# Build and install deephaven-ib
RUN mkdir /build && \
    cd /build && \
    git clone --branch ${DH_IB_BRANCH} https://github.com/deephaven-examples/deephaven-ib.git && \
    cd deephaven-ib && \
    python3 -m build && \
    pip3 install dist/*.whl

# Build sphinx
ENTRYPOINT cd /build/deephaven-ib/sphinx && make html && touch build/html/.nojekyll


