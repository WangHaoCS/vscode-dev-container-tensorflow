ARG IMAGE_TAG
FROM tensorflow/tensorflow:$IMAGE_TAG

# Use the [Option] comment to specify true/false arguments that should appear in VS Code UX
#
# [Option] Install zsh
ARG INSTALL_ZSH="false"
# [Option] Install OhMyZsh
ARG INSTALL_OHMYZSH=$INSTALL_ZSH
# [Option] Upgrade OS packages to their latest versions
ARG UPGRADE_PACKAGES="false"

# Install needed packages and setup non-root user. Use a separate RUN statement to add your own dependencies.
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
COPY common-debian.sh /tmp/

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && /bin/bash /tmp/common-debian.sh "${INSTALL_ZSH}" "${USERNAME}" "${USER_UID}" "${USER_GID}" "${UPGRADE_PACKAGES}" "${INSTALL_OHMYZSH}" "false"\
    && rm -rf /tmp/common-debian.sh \
    #
    # ****************************************************************************
    # * TODO: Add any additional OS packages you want included in the definition *
    # * here. We want to do this before cleanup to keep the "layer" small.       *
    # ****************************************************************************
    # && apt-get -y install --no-install-recommends <your-package-list-here> \
    #
    # Install autopep8 and pylint
    && apt-get -y install --no-install-recommends python3-autopep8 pylint3 \
    # Clean up
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts
