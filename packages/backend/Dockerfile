# This dockerfile builds an image for the backend package.
# It should be executed with the root of the repo as docker context.
#
# Before building this image, be sure to have run the following commands in the repo root:
#
# yarn install
# yarn tsc
# yarn build
#
# Once the commands have been run, you can build the image using `yarn build-image`

FROM node:16-buster-slim

RUN apt-get -qq update \
  && apt-get -qq install -y --no-install-recommends python3-pip python3-setuptools \
  && rm -rf /var/lib/apt/lists/* \
  && pip3 install --quiet --no-cache-dir mkdocs-techdocs-core==0.2.2

WORKDIR /app

# Copy repo skeleton first, to avoid unnecessary docker cache invalidation.
# The skeleton contains the package.json of each package in the monorepo,
# and along with yarn.lock and the root package.json, that's enough to run yarn install.
COPY --chown=node yarn.lock package.json ./
ADD --chown=node packages/backend/dist/skeleton.tar.gz ./
RUN yarn install --frozen-lockfile --production --network-timeout 300000 && rm -rf "$(yarn cache dir)"

# Then copy the rest of the backend bundle, along with any other files we might want.
COPY --chown=node app-config.yaml ./
ADD --chown=node packages/backend/dist/bundle.tar.gz ./

# Run as non-root user
RUN usermod --uid 1000 node && chown node /app -R
USER 1000

CMD ["node", "packages/backend", "--config", "app-config.yaml"]
