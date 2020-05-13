# litecoin-foke-guide

litecoin-fork-guide
Dependencies:
sudo apt-get install git

sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils

sudo apt-get install libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-dev libboost-thread-dev

sudo apt-get install libboost-all-dev

sudo apt-get install software-properties-common

sudo add-apt-repository ppa:bitcoin/bitcoin

sudo apt-get update

sudo apt-get install libdb4.8-dev libdb4.8++-dev

sudo apt-get install libminiupnpc-dev

sudo apt-get install libzmq3-dev

sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler

sudo apt-get install libqt4-dev libprotobuf-dev protobuf-compiler

git clone -b 0.8 https://github.com/litecoin-project/litecoin.git

find . -type f -print0 | xargs -0 sed -i 's/litecoin/testcoin/g'
find . -type f -print0 | xargs -0 sed -i 's/Litecoin/Testcoin/g'
find . -type f -print0 | xargs -0 sed -i 's/LiteCoin/Testcoin/g'
find . -type f -print0 | xargs -0 sed -i 's/LITECOIN/TESTCOIN/g'
find . -type f -print0 | xargs -0 sed -i 's/LTC/TST/g'
find . -type f -print0 | xargs -0 sed -i 's/9333/2333/g'
find . -type f -print0 | xargs -0 sed -i 's/9332/2332/g'
download these to set up valertpubkey
openssl ecparam -genkey -name secp256k1 -out alertkey.pem
openssl ec -in alertkey.pem -text > alertkey.hex
openssl ecparam -genkey -name secp256k1 -out testnetalert.pem
openssl ec -in testnetalert.pem -text > testnetalert.hex
openssl ecparam -genkey -name secp256k1 -out genesiscoinbase.pem
openssl ec -in testnetalert.pem -text > genesiscoinbase.hex
date +%s

paste the code to generate genesis hash
if (false && block.GetHash() != hashGenesisBlock)
       {
           printf("Searching for genesis block...\n");
           // This will figure out a valid hash and Nonce if you're
           // creating a different genesis block:
           uint256 hashTarget = CBigNum().SetCompact(block.nBits).getuint256();
           uint256 thash;
           char scratchpad[SCRYPT_SCRATCHPAD_SIZE];

           loop
           {
#if defined(USE_SSE2)
               // Detection would work, but in cases where we KNOW it always has SSE2,
               // it is faster to use directly than to use a function pointer or conditional.
#if defined(_M_X64) || defined(__x86_64__) || defined(_M_AMD64) || (defined(MAC_OSX) && defined(__i386__))
               // Always SSE2: x86_64 or Intel MacOS X
               scrypt_1024_1_1_256_sp_sse2(BEGIN(block.nVersion), BEGIN(thash), scratchpad);
#else
               // Detect SSE2: 32bit x86 Linux or Windows
               scrypt_1024_1_1_256_sp(BEGIN(block.nVersion), BEGIN(thash), scratchpad);
#endif
#else
               // Generic scrypt
               scrypt_1024_1_1_256_sp_generic(BEGIN(block.nVersion), BEGIN(thash), scratchpad);
#endif
               if (thash <= hashTarget)
                   break;
               if ((block.nNonce & 0xFFF) == 0)
               {
                   printf("nonce %08X: hash = %s (target = %s)\n", block.nNonce, thash.ToString().c_str(), hashTarget.ToString().c_str());
               }
               ++block.nNonce;
               if (block.nNonce == 0)
               {
                   printf("NONCE WRAPPED, incrementing time\n");
                   ++block.nTime;
               }
           }
           printf("block.nTime = %u \n", block.nTime);
           printf("block.nNonce = %u \n", block.nNonce);
           printf("block.GetHash = %s\n", block.GetHash().ToString().c_str());
       }
end
in src/qt/aboutdialog.cpp
 
Fix line 22: ui->copyrightLabel->setText(tr("Copyright") + QString(" &copy; 2009-%1 ").arg(COPYRIGHT_YEAR) + tr("The Bitcoin developers") + QString("<br>") + tr("Copyright") + QString(" &copy; ") + tr("2011-%1 The Litecoin developers").arg(ABOUTDIALOG_COPYRIGHT_YEAR)+ QString("<br>") + tr("Copyright") +QString(" &copy; ") + tr("%1 Funcoin Developer").arg(2017));
 
in src/qt/splashscreen.cpp
 
line 22, add int line4 = 39;
Fix line 30 and add 31: QString copyrightText3   = QChar(0xA9)+QString(" %1 ").arg(2017) + QString(tr("Funcoin Developer"));
Change line 48: pixPaint.drawText(paddingLeftCol2,paddingTopCol2+line4,versionText);
Add line 54: pixPaint.drawText(paddingLeftCol2,paddingTopCol2+line3,copyrightText3);
 
in src/qt/res/bitcoin-qt.rc:
 
Fix line 11: #define COPYRIGHT_STR          "2009-" STRINGIZE(COPYRIGHT_YEAR) " The Bitcoin developers 2011-" STRINGIZE(COPYRIGHT_YEAR) " The Litecoin developers 2017 Funcoin Developer"
 
in src/qt/aboutdialog.ui:
 
Below line 94, paste:
Copyright &amp;copy; 2011-YYYY The Litecoin developers
Copyright &amp;copy; 2017 Testcoin Developer</string>
 
1228, net.cpp
 
perl script:
 
#!/usr/bin/perl
 
# Twobits twobit integer dotted quad to reverse hex convertor
#  designed for q&d use to put seeds into pnSeeds in *coins
 
my $ip;
 
if (@ARGV) {
    $ip = shift @ARGV;
} else {
    print "Enter an (dotted quad) ip address: ";
    chomp( $ip = <STDIN> );
}
 
printf "0x%08x\n",  unpack 'N', pack 'C4', reverse split '\.', $ip;
LAST STEPS
Permit root users over SSH:
 
sed -i 's/^PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config
/etc/init.d/ssh restart
 
After logging in as root over SSH:
 
apt-get install git ruby sudo apt-cacher-ng qemu-utils debootstrap lxc python-cheetah parted kpartx bridge-utils make ubuntu-archive-keyring curl
adduser debian sudo
 
echo "%sudo ALL=NOPASSWD: /usr/bin/lxc-start" > /etc/sudoers.d/gitian-lxc
echo "%sudo ALL=NOPASSWD: /usr/bin/lxc-execute" >> /etc/sudoers.d/gitian-lxc
echo '#!/bin/sh -e' > /etc/rc.local
echo 'brctl addbr br0' >> /etc/rc.local
echo 'ifconfig br0 10.0.3.2/24 up' >> /etc/rc.local
echo 'iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE' >> /etc/rc.local
echo 'echo 1 > /proc/sys/net/ipv4/ip_forward' >> /etc/rc.local
echo 'exit 0' >> /etc/rc.local
echo 'export USE_LXC=1' >> /home/debian/.profile
echo 'export GITIAN_HOST_IP=10.0.3.2' >> /home/debian/.profile
echo 'export LXC_GUEST_IP=10.0.3.5' >> /home/debian/.profile
reboot
 
After logging in as debian over SSH:
 
wget http://archive.ubuntu.com/ubuntu/pool/universe/v/vm-builder/vm-builder_0.12.4+bzr494.orig.tar.gz
echo "76cbf8c52c391160b2641e7120dbade5afded713afaa6032f733a261f13e6a8e  vm-builder_0.12.4+bzr494.orig.tar.gz" | sha256sum -c
# (verification -- must return OK)
tar -zxvf vm-builder_0.12.4+bzr494.orig.tar.gz
cd vm-builder-0.12.4+bzr494
sudo python setup.py install
cd ..
 
Clone your coin into debian's home folder using git:
 
git clone https://github.com/schyczewski/funcoin.git
(Obviously replace my info with yours)
 
Build base VM:
 
bin/make-base-vm --lxc --arch amd64 --suite precise
 
Dependencies (make sure this is done in the gitian-builder directory):
 
mkdir -p inputs; cd inputs/
 
wget 'http://miniupnp.free.fr/files/download.php?file=miniupnpc-1.9.20140401.tar.gz' -O 'miniupnpc-1.9.20140401.tar.gz'
wget 'https://www.openssl.org/source/openssl-1.0.1k.tar.gz'
wget 'http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz'
wget 'https://www.zlib.net/fossils/zlib-1.2.8.tar.gz'
wget 'ftp://ftp.simplesystems.org/pub/libpng/png/src/history/libpng16/libpng-1.6.8.tar.gz'
wget 'http://fukuchi.org/works/qrencode/qrencode-3.4.3.tar.bz2'
wget 'http://downloads.sourceforge.net/project/boost/boost/1.55.0/boost_1_55_0.tar.bz2'
wget 'https://download.qt.io/archive/qt/4.8/4.8.5/qt-everywhere-opensource-src-4.8.5.tar.gz'
wget 'https://svn.boost.org/trac/boost/raw-attachment/ticket/7262/boost-mingw.patch' -O boost-mingw-gas-cross-compile-2013-03-03.patch
 
Building depencies (in gitian-builder, replace instances of 'funcoin' with whatever you named your clone):
 
./bin/gbuild ../funcoin/contrib/gitian-descriptors/boost-win32.yml
mv build/out/boost-*.zip inputs/
 
./bin/gbuild ../funcoin/contrib/gitian-descriptors/deps-win32.yml
mv build/out/bitcoin*.zip inputs/
 
./bin/gbuild ../funcoin/contrib/gitian-descriptors/qt-win32.yml
mv build/out/qt*.zip inputs/
 
Compile your coin (remember tag & name change):
 
./bin/gbuild --commit funcoin=v0.8 ../testcoin/contrib/gitian-descriptors/gitian-win32.yml
Git file permissions on Windows
$ git diff --summary origin/epsilon master/epsilon
 mode change 100644 => 100755 ants/dist/sample_bots/csharp/compile.sh
 mode change 100644 => 100755 ants/dist/starter_bots/coffeescript/MyBot.coffee
 mode change 100644 => 100755 ants/dist/starter_bots/coffeescript/ants.coffee
 mode change 100644 => 100755 ants/util/block_test.sh
 mode change 100644 => 100755 manager/mass_skill_update.py
 mode change 100644 => 100755 worker/jailguard.py
 mode change 100644 => 100755 worker/release_stale_jails.py
 mode change 100644 => 100755 worker/start_worker.sh
setting up block explorer
Iquidus github repo: https://github.com/iquidus/explorer
Instaling guide
--Block explorer pastes
 
sudo apt-get update
sudo apt install nodejs-legacy
sudo apt-get install npm
sudo apt-get install
 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
 
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl start mongod
 
Start mongodb cli:
mongo
use explorerdb
db.createUser( { user: "iquidus", pwd: "3xp!0reR", roles: [ "readWrite" ] } )
exit
 
git clone https://github.com/iquidus/explorer explorer
cd explorer && npm install --production
cp ./settings.json.template ./settings.json
 
To use forever to start (run in directory of explorer):
forever start -c "npm start" ./
 
crontab information:
*/1 * * * * cd explorer && /usr/bin/nodejs scripts/sync.js index update > /dev/null 2>&1
*/5 * * * * cd explorer && /usr/bin/nodejs scripts/peers.js > /dev/null 2>&1
