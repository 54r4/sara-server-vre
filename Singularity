Bootstrap: docker
From: ubuntu:16.10

%file 
eclipse-jee-oxygen-1-linux-gtk-x86_64.tar.gz

%post
apt-get update && apt-get -y install git wget vim openjdk-8-jdk
mkdir -p /opt
cd /tmp
wget http://www.uni-ulm.de/~nsn25/SARA/eclipse-jee-oxygen-1-linux-gtk-x86_64.tar.gz
sha256sum eclipse-jee-oxygen-1-linux-gtk-x86_64.tar.gz # c2435e8f52fbe94859e8786d3c631c3c3b592c5f58d4c49de615fc414f6dfe3c
tar -xzf eclipse-jee-oxygen-1-linux-gtk-x86_64.tar.gz
mv /tmp/eclipse /opt

%environment
export PATH="/opt/eclipse:$PATH"

%runscript
if [ "$#" -eq 0 ]; then
  echo "calling without gitdir, checking out git..."
  GITDIR="/tmp/sara-server"
  rm -rf "$GITDIR" && mkdir -p "$GITDIR" && cd "$GITDIR"
  git clone git@git.uni-konstanz.de:sara/SARA-server.git $GITDIR
  git submodule update --init
else
  echo "calling with gitdir=$1..."
  GITDIR="$1"
fi

cd $GITDIR
git pull
git submodule update

echo "==========================================="
echo "IF THIS IS YOUR INITAL RUN DO THE FOLLOWING:"
echo " 1) Open up a clean workspace"
echo " 2) Import the SARA code as 'Maven Project'"
echo " 3) Set 'bwfdm.sara.Application under 'Run'-'Run Configuration'"
echo " 4) 'Run as' select 'SpringBoot App' -> connect to 'localhost:8080'"
echo " 5) Congrats ... you're done!"

echo "calling eclipse"
/opt/eclipse/eclipse # -clean -purgeHistory -noSplash -data /tmp/sara-server #-application bwfdm.sara.Application
echo "Exiting Container..."
sync
sleep 3
echo "..."
sleep 3

