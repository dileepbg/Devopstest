# Copyright 2016 The Kubernetes Authors.
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

FROM nginx

COPY ./default.conf /etc/nginx/conf.d/default.conf
COPY static.json /usr/share/nginx/html/static.json
RUN chmod +r /usr/share/nginx/html/static.json
#COPY ./testapp.conf /etc/nginx/conf.d/testapp.conf
#RUN chmod 777 /etc/nginx/conf.d/testapp.conf
COPY auto-reload-nginx.sh /home/auto-reload-nginx.sh
RUN chmod +x /home/auto-reload-nginx.sh

# install inotify

RUN apt-get update && apt-get install -y inotify-tools
