Vagrant.configure('2') do |config|
  # Ubuntu 14.04
  config.vm.box = "ubuntu/trusty64"

  # Docker
  config.vm.provision :docker

  # Install appc tools & rocket
  config.vm.provision :shell,inline: <<EOF

echo 'Install dependencies...'
sudo apt-get update -y 
sudo apt-get install --no-install-recommends -y -q \
                     curl \
                     build-essential \
                     ca-certificates \
                     git mercurial bzr \
                     libseccomp2 \
                     libseccomp-dev

GOVERSION=1.4.2
echo "Install Go v${GOVERSION}"
mkdir /home/vagrant/goroot
mkdir -p /home/vagrant/gopath/bin
curl https://storage.googleapis.com/golang/go${GOVERSION}.linux-amd64.tar.gz \
           | tar xvzf - -C /home/vagrant/goroot --strip-components=1

export GOROOT=/home/vagrant/goroot
export GOPATH=/home/vagrant/gopath
export PATH=$GOROOT/bin:$GOPATH/bin:$PATH
echo 'export GOROOT=/home/vagrant/goroot' > /home/vagrant/gopath
echo 'export GOPATH=/home/vagrant/gopath' >> /home/vagrant/gopath
echo 'export PATH=$GOROOT/bin:$GOPATH/bin:$PATH' >> /home/vagrant/gopath

echo "Install runc"
mkdir -p ${GOPATH}/src/github.com/opencontainers
cd ${GOPATH}/src/github.com/opencontainers
git clone https://github.com/opencontainers/runc
cd runc/
make
sudo make install
EOF
end
