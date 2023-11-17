FROM ringcentral/chrome-vnc:chrome119-firefox119
ENV DISPLAY :99
ARG NODE_VERSION=16

#
#install node
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add - \
    && apt-get update -yq \
    && apt-get install curl openjdk-8-jdk -yq \
    && curl -sL https://deb.nodesource.com/setup_${NODE_VERSION}.x | bash \
    && apt-get install nodejs -yq

#It's a good idea to use dumb-init to help prevent zombie chrome processes.
ADD https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64 /usr/local/bin/dumb-init
RUN chmod +x /usr/local/bin/dumb-init



#Install tools :selenium-standalone need install java
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn lame
RUN npm install selenium-standalone -g 
# RUN npm init -y
# RUN yarn add puppeteer
# RUN yarn global add lerna



# Set Timezone
#RUN echo "Asia/Shanghai" > /etc/timezone
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN dpkg-reconfigure -f noninteractive tzdata

#ENTRYPOINT ["dumb-init", "--"]
