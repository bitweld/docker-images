# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# Cloudera removed an access to CDH5 repositories in April 2021.
# In order to build new image version we use last released version as base.
# Previous Dockerfile version is archived in archived/cdh5.15-hive.
FROM ghcr.io/trinodb/testing/cdh5.15-hive-kerberized-kms:38

# COPY CONFIGURATION
COPY ./files /

RUN \
    set -xeu && \
    # Install additional Zulu JDK 17.0.0
    rpm -i https://cdn.azul.com/zulu/bin/zulu17.28.13-ca-jdk17.0.0-linux.x86_64.rpm && \
    # Upgrade Zulu JDK to 11.0.11
    rpm -Ui https://cdn.azul.com/zulu/bin/zulu11.48.21-ca-jdk11.0.11-linux.x86_64.rpm && \
    # Set JDK 11 as a default one
    alternatives --set java /usr/lib/jvm/zulu-11/bin/java && \
    alternatives --set javac /usr/lib/jvm/zulu-11/bin/javac && \
    echo "Done"

CMD supervisord -c /etc/supervisord.conf
