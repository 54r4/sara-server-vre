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
if [ "_$1" = _ ]; then
	BASE=/tmp/sara
else
	BASE="$1"
	shift
fi

if [ "$#" -eq 0 ]; then
	GITDIR="$BASE/sara-server"
	if ! [ -d "$GITDIR" ]; then
		echo "checking out to $GITDIR..."
		mkdir -p "$GITDIR"
		git clone git@git.uni-konstanz.de:sara/SARA-server.git "$GITDIR"
		cd "$GITDIR"
		git submodule update --init
	else
		echo "updating $GITDIR..."
		cd "$GITDIR"
		git pull
		git submodule update
	fi
else
	GITDIR="$1"
	echo "using existing working copy in $GITDIR"
	# IMO we shouldn't pull it here
	# the user "owns" that directory, so we better not mess with it
	/bin/echo -e '\e[1;33mplease "git pull" it manually if necessary!\e[0m'
	cd "$GITDIR"
fi

/bin/echo -e '\e[32m' # sometimes, dash sucks!
echo "===================================================="
/bin/echo -en '\e[1m'
echo "IF THIS IS YOUR INITAL RUN, PELASE DO THE FOLLOWING:"
/bin/echo -e '\e[0;32m'
echo " 1) Import the SARA code as 'Existing Maven Project'"
echo " 2) Open 'bwfdm.sara.Application' and right-click 'Run' -> 'Java Application'"
echo " 3) Wait for Spring to start, connect to 'http://localhost:8080'"
echo " 4) Congrats ... you're done!"
/bin/echo -e '\e[0m'

echo "calling eclipse"
/opt/eclipse/eclipse -configuration "$BASE/eclipseconfig" -data "$BASE"
echo "Exiting Container..."
sync
sleep 3 # make user think we're doing this properly
echo "..."
sleep 3 # it's really there to give all Java processes a chance to quit
