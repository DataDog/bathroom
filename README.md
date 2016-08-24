# Background

You can find more details on the project and implementation on [Datadog's Engineering blog](http://engineering.datadoghq.com/restroom-hacks/).

# Setup

```
sudo apt-get install daemontools-run git ucspi-tcp

git clone git@github.com:DataDog/bathroom.git

# Test sensor hookup
BATHROOM_CONFIG="12 men left:14:nc,12 men right:15:nc" bathroom/bin/bathroom_status

# Going the djb way mostly because this version of raspbian doesn't have a sane
# init system.
sudo mkdir /service
sudo mv bathroom /service/bathroom
ln -s /service/bathroom . # for convenience if you want
mkdir /service/bathroom/envdir/
echo "12 men left:14:nc,12 men right:15:nc" > /service/bathroom/envdir/BATHROOM_CONFIG # set according to your setup
sudo adduser --system --shell=/usr/sbin/nologin --ingroup=gpio bathroom
sudo ln -s /service/bathroom /etc/service/bathroom
```

# Usage

```
$ nc bathroom.example.com 50
Bathroom Status:
12 men left: Available
12 men right: Available
```
