#
# Copyright © 2025 BellSoft (info@bell-sw.com)
#
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
#

FROM bellsoft/liberica-runtime-container:jdk-21.0.7_9-stream-musl as builder
ARG project
ENV project=${project}

WORKDIR /app
ADD ${project} /app/${project}
ADD ../pom.xml ./
RUN cd ${project} && ./mvnw -Dmaven.test.skip=true clean package


FROM bellsoft/liberica-runtime-container:jre-21.0.7_9-musl
ARG project
ENV project=${project}

RUN apk add curl
WORKDIR /app
ENTRYPOINT ["java", "-jar", "/app/app.jar"]
COPY --from=builder /app/${project}/target/*.jar /app/app.jar
