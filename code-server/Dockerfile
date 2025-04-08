FROM quay.io/devfile/universal-developer-image:ubi9-latest

# Optional: set ENV versions
ENV INSTRUCTLAB_PKG=instructlab
ENV INSTRUCTLAB_VERSION=

# Set working directory
WORKDIR /opt/app-root

# Install Python build tools and required libs
RUN pip install --upgrade pip \
 && pip install packaging wheel \
 && pip install torch==2.4.1 psutil==6.1.0 \
 && pip install flash_attn==2.6.3 --no-build-isolation \
 && pip install --no-deps llama_cpp_python[server]==0.2.79 \
        -C cmake.args="-DLLAMA_CUDA=off" \
        -C cmake.args="-DLLAMA_NATIVE=off" \
 && if [ "${INSTRUCTLAB_VERSION}" != "" ]; then \
        INSTRUCTLAB_PKG="${INSTRUCTLAB_PKG}==${INSTRUCTLAB_VERSION}" ; \
    fi \
 && pip install "${INSTRUCTLAB_PKG}" \
        -C cmake.args="-DLLAMA_CUDA=off" \
        -C cmake.args="-DLLAMA_NATIVE=off" \
 && pip install vllm@git+https://github.com/opendatahub-io/vllm@v0.6.2 \
 && pip install 'nvitop==1.3.2' \
 && chmod -R g+w /opt/app-root/lib/python3.11/site-packages \
 && fix-permissions /opt/app-root -P

# Optional: copy entrypoint or content if needed
# COPY . /opt/app-root

# Default CMD or entrypoint if needed
CMD [ "bash" ]
