from ubuntu

ENV USERNAME="dev"

ENV GOVERSION=1.14
ENV GOOS=linux
ENV GOARCH=amd64

ENV GOPROXY=""
ENV GOPATH="/home/$USERNAME/go"

# install tools 
RUN apt update && apt install -y wget curl jq ansible git sudo iputils-ping

# add user and allow sudo
RUN useradd -m $USERNAME && echo "$USERNAME:$USERNAME" | chpasswd && adduser $USERNAME sudo

# install go sdk
RUN wget -nv https://dl.google.com/go/go$GOVERSION.$GOOS-$GOARCH.tar.gz && tar -C /usr/local -xzf go$GOVERSION.$GOOS-$GOARCH.tar.gz && rm go$GOVERSION.$GOOS-$GOARCH.tar.gz

# configure go sdk
RUN echo 'export PATH=$PATH:/usr/local/go/bin:'"$GOPATH/bin" >> /etc/profile
RUN echo "export GOPATH='$GOPATH'" >> /etc/profile 
RUN echo "export GOPROXY='$GOPROXY'" >> /etc/profile 

USER $USERNAME
WORKDIR /home/$USERNAME

# install some go tools
# RUN go get github.com/magefile/mage

CMD ["/bin/bash", "--login"]
