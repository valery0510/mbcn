# 第3章 比特币客户端

## 3.1 比特币核心：参考实现 

你可以从bitcoin.org下载标准客户端，即比特币核心，也叫“中本聪客户端”（satoshi client）。它实现了比特币系统的所有方面，包括钱包、对整个交易账簿（区块链）完整拷贝的交易确认引擎，和点对点比特币网络中的一个完整网络节点。

[在Bitcoin网站的选择钱包页面](https://bitcoin.org/en/choose-your-wallet)，下载参考客户端比特币核心。根据操作系统不同，你将下载不同的可执行安装工具。对于Windows，它是一个ZIP归档文件或.exe格式的可执行文件。对于Mac OS，它是一个.dmg格式的磁盘映像。Linux版本包括用于Ubuntu系统的PPA包，或是 tar.gz格式的压缩包。图3-1所示的Bitcoin.org页面上列出了一些推荐的比特币客户端。

> ![](Images/Fig 3-1.png) 
<br> 图3-1 选择比特币客户端

### 3.1.1 第一次运行比特币核心

如果你下载了一个安装包，比如.exe、.dmg、或PPA，你可以和安装其它任何应用程序一样，在你的操作系统上安装它。对于Windows，运行.exe文件，按照提示一步步操作。对于Mac OS，启动.dmg文件，然后将Bitcoin-QT 图标拖拽到你的应用程序目录就可以了。对于Ubuntu，在文件资源管理器中双击PPA文件，会打开程序包管理器来安装它。一旦完成了安装，在你的应用程序列表中会有一个新的应用叫Bitcoin-QT。双击这个图标就可以启动比特币客户端了。

第一次运行比特币核心时，它会开始下载整个区块链，这个过程可能需要数天（见下图）。让它在后台运行，直到显示“已同步”，并且余额旁边不再显示“数据同步中”。

> ![](Images/Icon 1.png) 
<br> 比特币核心拥有交易账簿（区块链）的一份完整拷贝，里面记录了自2009年比特币网络被发明以来发生在比特币网络上的每一笔交易。这个数据集有几个GB（在2013年底大约是16GB），并且需要几天的时间完成增量形式的下载（从区块0顺次下载到最新区块）。在整个区块链数据集下载完成前，客户端将不能处理任何交易或是更新账户余额。在下载数据集的过程中，客户端账户余额旁会显示“数据同步中”，底部会显示“正在同步”。请确保你有足够的磁盘空间、带宽和时间来完成初始同步。

### 3.1.2 从源码编译比特币核心比特币核心

对于开发者，可以选择下载包含完整源代码的ZIP包，也可以从Github上克隆权威的源码仓库。在面[GitHub上的比特币页面](https://github.com/bitcoin/bitcoin)，在侧边栏选择下载ZIP。或者使用git命令行（git command line）在自己系统上创建源码的本地拷贝。在下面的例子中，我们将通过unix风格的命令行，在Linux或是Mac OS 上克隆源代码：

```
$ git clone https://github.com/bitcoin/bitcoin.git
Cloning into 'bitcoin'...
remote: Counting objects: 31864, done.
remote: Compressing objects: 100% (12007/12007), done.
remote: Total 31864 (delta 24480), reused 26530 (delta 19621)
Receiving objects: 100% (31864/31864), 18.47 MiB | 119 KiB/s, done.
Resolving deltas: 100% (24480/24480), done.
$
```

> ![](Images/Icon 1.png) 
<br> 终端上的提示和输出结果可能会因版本有所不同。即使你的屏幕上输出的内容跟这里的例子有点不一样，请遵照代码中的文档，这些都是正常的。

在git clone操作完成后，在你本地的bitcoin目录就会有一份完整的源码拷贝。通过在命令提示行输入cd bitcoin切换到这个目录下：

`$ cd bitcoin`

默认情况下，本地拷贝将与最新的代码同步，这可能是bitcoin的一个不稳定或是 beta 版本。在编译这些代码之前，签出发布标签（realease tag）以选择某一特定版本（a specific version）。 这将通过一个关键的标签标记，让本地拷贝与代码仓库的特定快照同步。开发者用标签来标记代码的特定发行版本号（version numBTCer）。首先，要找到可用的标签，可以通过git tag命令：

```
$ git tag
v0.1.5
v0.1.6test1
v0.2.0
v0.2.10
v0.2.11
v0.2.12
     
[... many more tags ...]
     
v0.8.4rc2
v0.8.5
v0.8.6
v0.8.6rc1
v0.9.0rc1```


列出的标签是bitcoin的所有发行版本。按照约定，带有rc后缀的是预发行版本，可以用来测试。没有后缀的稳定版本可以直接在产品环境上运行。从上面的列表中，选择最新的发行版本，目前是v0.9.0rc1。为了让本地代码跟这个版本一致，我们需要用git checkout 命令： 

```
$ git checkout v0.9.0rc1
Note: checking out 'v0.9.0rc1'.

HEAD is now at 15ec451... Merge pull request #3605
$```

源代码包含文档，可以在多个文件夹中找到。在命令提示行输入more
README.md可以在bitcoin目录下的README.md中查看主文档，用空格键可以翻页。在这一章，我们将构建命令行的比特币客户端，在linux上称作bitcoind。在您的平台上，通过输入more doc/build-unix.md，可以阅读编译bitcoind命令行客户端的说明。Mac OSX和Windows平台的说明可以在doc目录下找到，分别是build-osx.md或是build-msw.md。

仔细阅读build文档第一部分中build的必备条件。这些是在你编译之前你的系统上必须具备的库文件。如果缺少这些必备条件，构建过程将会出现错误并导致失败。如果因为缺少一个必备条件而发生这种情况，你可以先安装它，然后在你停下的地方重新构建。假设这些必备条件已经具备，你就可以开始构建过程，通过authgen.sh脚本，生成一组构建脚本。

> ![](Images/Icon 1.png) 
<br> 从v0.9版本开始，比特币核心的构建过程改用autogen/configure/make 体系。旧版本是用一个简单的Makefile，并且和下面的例子稍微有一点不同。请遵照你想要编译版本的说明文档。v0.9版本引入的 autogen/configure/make 构建体系可能用于未来所有版本的代码，是下面的例子中演示的系统

```
$ ./autogen.sh
configure.ac:12: installing `src/build-aux/config.guess'
configure.ac:12: installing `src/build-aux/config.sub'
configure.ac:37: installing `src/build-aux/install-sh'
configure.ac:37: installing `src/build-aux/missing'
src/Makefile.am: installing `src/build-aux/depcomp'
$
```

autogen.sh脚本创建了一系列的自动配置脚本，会询问你的系统以发现正确的设置，确保你已安装必要的库来编译源码。这里面最重要的是configure脚本，它会提供许多不同的选项来定制构建过程。输入./configure --help 可以查看各种不同的选项：

```
$ ./configure --help

`configure' configures Bitcoin Core 0.9.0 to adapt to many kinds of systems.

Usage: ./configure [OPTION]... [VAR=VALUE]...

To assign environment variables (e.g., CC, CFLAGS...), specify them as VAR=VALUE.  

See below for descriptions of some of the useful variables.

Defaults for the options are specified in brackets.

Configuration:
  -h, --help              display this help and exit
      --help=short        display options specific to this package
      --help=recursive    display the short help of all the included packages
  -V, --version           display version information and exit

[... many more options and variables are displayed below ...]

Optional Features:
  --disable-option-checking  ignore unrecognized --enable/--with options
  --disable-FEATURE       do not include FEATURE (same as    --enable-FEATURE=no)
  --enable-FEATURE[=ARG]  include FEATURE [ARG=yes]

[... more options ...]

Use these variables to override the choices made by `configure' or to help it to find libraries and programs with nonstandard names/locations.

Report bugs to <info@bitcoin.org>.

$
```

通过使用--enable-FEATURE和--disable-FEATURE选项，configure脚本允许你启用或是禁用某些功能，FEATURE需要被替换成功能名称，在上面的帮助输出中可以找到。在这一章，我们将用默认的功能来构建bitcoind客户端。这里不会使用配置选项，但是你应该检查一遍，明白哪些可选的功能可以作为客户端的一部分。下一次，运行configure脚本就可以自动发现所有必要的库，然后为我们的系统创建一个定制的构建脚本。

```
$ ./configure
checking build system type... x86_64-unknown-linux-gnu
checking host system type... x86_64-unknown-linux-gnu
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /bin/mkdir -p
checking for gawk... no
checking for mawk... mawk
checking whether make sets $(MAKE)... yes

[... many more system features are tested ...]

configure: creating ./config.status
config.status: creating Makefile
config.status: creating src/Makefile
config.status: creating src/test/Makefile
config.status: creating src/qt/Makefile
config.status: creating src/qt/test/Makefile
config.status: creating share/setup.nsi
config.status: creating share/qt/Info.plist
config.status: creating qa/pull-tester/run-bitcoind-for-test.sh
config.status: creating qa/pull-tester/build-tests.sh
config.status: creating src/bitcoin-config.h
config.status: executing depfiles commands
$
```

如果一切顺利，configure命令将会以创建可定制的构建脚本结束。这些构建脚本允许我们编译bitcoind。如果有缺失的库或是错误，configur命令将会以错误信息终止。如果出现了错误，可能是因为缺少库或是有不兼容的库。重新检查构建文档，确认你已经安装缺失的必备条件。然后运行configure，看看错误是否消失了。下一步，你将编译源代码，这个过程可能需要1个小时完成。在编译的过程中，你应该过几秒或是几分钟看一下输出结果。如果出现了问题，你会看到错误。如果中断了，编译的过程可以在任何时候恢复。输入make命令就可以开始编译了：

```
$ make
Making all in src
make[1]: Entering directory `/home/ubuntu/bitcoin/src'
make  all-recursive
make[2]: Entering directory `/home/ubuntu/bitcoin/src'
Making all in .
make[3]: Entering directory `/home/ubuntu/bitcoin/src'
    CXX    addrman.o
    CXX    alert.o
    CXX    rpcserver.o
    CXX    bloom.o
    CXX    chainparams.o

    [... many more compilation messages follow ...]

    CXX    test_bitcoin-wallet_tests.o
    CXX    test_bitcoin-rpc_wallet_tests.o
    CXXLD  test_bitcoin
make[4]: Leaving directory `/home/ubuntu/bitcoin/src/test'
make[3]: Leaving directory `/home/ubuntu/bitcoin/src/test'
make[2]: Leaving directory `/home/ubuntu/bitcoin/src'
make[1]: Leaving directory `/home/ubuntu/bitcoin/src'
make[1]: Entering directory `/home/ubuntu/bitcoin'
make[1]: Nothing to be done for `all-am'.
make[1]: Leaving directory `/home/ubuntu/bitcoin'
$
```

如果一切顺利，bitcoind现在已经编译完成。最后一步就是通过make命令，安装 bitcoind 可执行文件到你的系统路径下：

```
$ sudo make install
Making install in src
Making install in .
    /bin/mkdir -p '/usr/local/bin'
    /usr/bin/install -c bitcoind bitcoin-cli '/usr/local/bin'
Making install in test
make  install-am
 /bin/mkdir -p '/usr/local/bin'
  /usr/bin/install -c test_bitcoin '/usr/local/bin'
$
```

你可以通过询问系统下面2个可执行文件的路径，来确认bitcoin是否安装成功。

```
$ which bitcoind
/usr/local/bin/bitcoind

$ which bitcoin-cli
/usr/local/bin/bitcoin-cli
```

bitcoind 默认的安装位置是/usr/local/bin。当你第一次运行bitcoind时，它会提醒你用一个安全密码给JSON-RPC接口创建一个配置文件。通过在终端输入bitcoind就可以运行bitcoind了：

```
$ bitcoind
Error: To use the "-server" option, you must set a rpcpassword in the configuration file:
/home/ubuntu/.bitcoin/bitcoin.conf
It is recommended you use the following random password:
rpcuser=bitcoinrpc
rpcpassword=2XA4DuKNCbtZXsBQRRNDEwEY2nM6M4H9Tx5dFjoAVVbK
(you do not need to remember this password)
The username and password MUST NOT be the same.
If the file does not exist, create it with owner-readable-only file permissions.
It is also recommended to set alertnotify so you are notified of problems;
for example: alertnotify=echo %s | mail -s "Bitcoin Alert" admin@foo.com
```

在你喜欢的编辑器中编辑配置文件并设置参数，将其中的密码替换成bitcoind推荐的强密码。不要使用出现在这里的密码。在.bitcoin目录下创建一个名为.bitcoin/bitcoin.conf 的文件，然后输入用户名和密码：

```
rpcuser=bitcoinrpc
rpcpassword=2XA4DuKNCbtZXsBQRRNDEwEY2nM6M4H9Tx5dFjoAVVbK
```

当你正在编辑配置文件的时候，你可能想要设置一些其他选项，例如txindex（见<a href="chapter03.html#%E4%BA%A4%E6%98%93%E6%95%B0%E6%8D%AE%E5%BA%93%E7%B4%A2%E5%BC%95%E5%8F%8Atxindex%E9%80%89%E9%A1%B9">“交易数据库索引及txindex选项”</a>）。通过输入`bitcoind --help`，可以查看所有可用的选项列表。

现在可以运行比特币核心客户端。当你第一次运行的时候，它会下载所有的区块，重新构建比特币区块链。这是一个好几个GB的文件，可能需要大约2天的时间全部下载完。你可以通过[SourceForge](http://sourceforge.net/projects/bitcoin/files/Bitcoin/blockchain/)上的BitTorrent客户端下载区块链的部分拷贝来缩短区块链的初始化时间。

选项 -daemon 可以以后台模式运行 bitcoind。

```
$ bitcoind -daemon

Bitcoin version v0.9.0rc1-beta (2014-01-31 09:30:15 +0100)
Using OpenSSL version OpenSSL 1.0.1c 10 May 2012
Default data directory /home/bitcoin/.bitcoin
Using data directory /bitcoin/
Using at most 4 connections (1024 file descriptors available)
init message: Verifying wallet...
dbenv.open LogDir=/bitcoin/database ErrorFile=/bitcoin/db.log
Bound to [::]:8333
Bound to 0.0.0.0:8333
init message: Loading block index...
Opening LevelDB in /bitcoin/blocks/index
Opened LevelDB successfully
Opening LevelDB in /bitcoin/chainstate
Opened LevelDB successfully

[... more startup messages ...]
```

## 3.2 通过命令行使用比特币核心的JSON-RPC API接口

比特币核心客户端实现了JSON-RPC接口，这个接口也可以通过命令行帮助程序bitcoin-cli访问。命令行可以使用API进行编程，让我们有能力进行交互实验。开始前，调用help命令查看可用的比特币RPC命令列表：

```
$ bitcoin-cli help
addmultisigaddress nrequired ["key",...] ( "account" )
addnode "node" "add|remove|onetry"
backupwallet "destination"
createmultisig nrequired ["key",...]
createrawtransaction [{"txid":"id","vout":n},...] {"address":amount,...}
decoderawtransaction "hexstring"
decodescript "hex"
dumpprivkey "bitcoinaddress"
dumpwallet "filename"
getaccount "bitcoinaddress"
getaccountaddress "account"
getaddednodeinfo dns ( "node" )
getaddressesbyaccount "account"
getbalance ( "account" minconf )
getbestblockhash
getblock "hash" ( verbose )
getblockchaininfo
getblockcount
getblockhash index
getblocktemplate ( "jsonrequestobject" )
getconnectioncount
getdifficulty
getgenerate
gethashespersec
getinfo
getmininginfo
getnettotals
getnetworkhashps ( blocks height )
getnetworkinfo
getnewaddress ( "account" )
getpeerinfo
getrawchangeaddress
getrawmempool ( verbose )
getrawtransaction "txid" ( verbose )
getreceivedbyaccount "account" ( minconf )
getreceivedbyaddress "bitcoinaddress" ( minconf )
gettransaction "txid"
gettxout "txid" n ( includemempool )
gettxoutsetinfo
getunconfirmedbalance
getwalletinfo
getwork ( "data" )
help ( "command" )
importprivkey "bitcoinprivkey" ( "label" rescan )
importwallet "filename"
keypoolrefill ( newsize )
listaccounts ( minconf )
listaddressgroupings
listlockunspent
listreceivedbyaccount ( minconf includeempty )
listreceivedbyaddress ( minconf includeempty )
listsinceblock ( "blockhash" target-confirmations )
listtransactions ( "account" count from )
listunspent ( minconf maxconf ["address",...] )
lockunspent unlock [{"txid":"txid","vout":n},...]
move "fromaccount" "toaccount" amount ( minconf "comment" )
ping
sendfrom "fromaccount" "tobitcoinaddress" amount ( minconf "comment" "commentto"
)
sendmany "fromaccount" {"address":amount,...} ( minconf "comment" )
sendrawtransaction "hexstring" ( allowhighfees )
sendtoaddress "bitcoinaddress" amount ( "comment" "comment-to" )
setaccount "bitcoinaddress" "account"
setgenerate generate ( genproclimit )
settxfee amount
signmessage "bitcoinaddress" "message"
signrawtransaction "hexstring" ( [{"txid":"id","vout":n,"scriptPub-
Key":"hex","redeemScript":"hex"},...] ["privatekey1",...] sighashtype )
stop
submitblock "hexdata" ( "jsonparametersobject" )
validateaddress "bitcoinaddress"
verifychain ( checklevel numBTClocks )
verifymessage "bitcoinaddress" "signature" "message"
walletlock
walletpassphrase "passphrase" timeout
walletpassphrasechange "oldpassphrase" "newpassphrase"
```

### 3.2.1 获得比特币核心客户端状态的信息

命令：`getinfo`

比特币`getinfo`RPC命令显示关于比特币网络节点、钱包、区块链数据库状态的基础信息。使用```bitcoin-cli```运行它：

```
$ bitcoin-cli getinfo
{
"version" : 90000,
"protocolversion" : 70002,
"walletversion" : 60000,
"balance" : 0.00000000,
"blocks" : 286216,
"timeoffset" : -72,
"connections" : 4,
"proxy" : "",
"difficulty" : 2621404453.06461525,
"testnet" : false,
"keypoololdest" : 1374553827,
"keypoolsize" : 101,
"paytxfee" : 0.00000000,
"errors" : ""
}
```

数据以JSON格式显示，JSON是一种可以很容易被编程语言“消耗”，但同时对人类可读性也很高的格式。在这些数据中，我们看到比特币软件客户端的版本编号（90000），协议编号（70002），钱包编号（60000）。我们看到钱包中的当前余额是0。我们看到当前的区块高度，这可以告诉我们有多少区块对此客户端已知（286216）。我们同样看到关于比特币网络和关于此客户端的各种数据。我们将在其他章节中更具体地探索这些设置。

> ![](Images/Icon 1.png) 
<br> bitcoind客户端需要花费可能超过一天的时间从其他比特币客户端下载区块以“赶上”当前区块链高度。你可以使用getinfo命令查看已知区块的数字以检查同步进度。

### 3.2.2 钱包设置及加密

命令：`encryptwallet`、`walletpassphrase`

在你向前生成秘钥和其他命令之前，你应当先用密码加密钱包。对于本例，将使用`encryptwallet`命令，密码为“foo”。很明显，在你自己操作的时候记得使用强且复杂的密码替换“foo”。

```
$ bitcoin-cli encryptwallet foo
wallet encrypted; Bitcoin server stopping, restart to run with encrypted wallet.
The keypool has been flushed, you need to make a new backup.
$
```

你可以再次使用`getinfo`命令以验证钱包是否已经加密。这次你将发现有个叫做`unlocked_until`的新条目。这是一个计数器，告诉你保持钱包处于解锁状态的解密密码将在内存中存储多久。最初计数器设置为0，意味着钱包是被锁定的：

```
$ bitcoin-cli getinfo
{
     "version" : 90000,
#[... other information...]
     "unlocked_until" : 0,
     "errors" : ""
}
$
```

想解锁钱包，要使用`walletpassphrase`命令。`walletpassphrase`命令需要两个参数——密码，和多久钱包会再次被自动锁定的秒数数字（计时器）：

```
$ bitcoin-cli walletpassphrase foo 360
$
```

你可以确认钱包是解锁状态然后通过再次运行`getinfo`查看超过时限：

```
$ bitcoin-cli getinfo
{
     "version" : 90000,
#[... other information ...]
     "unlocked_until" : 1392580909,
     "errors" : ""
}
```

### 3.2.3 钱包备份、纯文本导出及恢复

命令：`backupwallet`、`importwallet`、`dumpwallet`

下一步，我们将练习创建钱包的备份文件，然后从备份文件重新加载钱包。使用`backupwallet`命令备份，提供文件名作为命令参数。这里我们将钱包备份为文件*wallet.backup*：

```
$ bitcoin-cli backupwallet wallet.backup
$
```

现在，为了重新加载备份文件，我们使用`importwallet`命令。如果你的钱包处于锁定状态，你将需要先将钱包解锁（参考下一节的`walletpassphrase`）以导入备份文件：

```
$ bitcoin-cli importwallet wallet.backup
$
```

`dumpwallet` 命令用来将钱包转储为人类可读的文本文件：

```
$ bitcoin-cli dumpwallet wallet.txt
$ more wallet.txt
# Wallet dump created by Bitcoin v0.9.0rc1-beta (2014-01-31 09:30:15 +0100)
# * Created on 2014-02- 8dT20:34:55Z
# * Best block at time of backup was 286234
(0000000000000000f74f0bc9d3c186267bc45c7b91c49a0386538ac24c0d3a44),
# mined on 2014-02- 8dT20:24:01Z

KzTg2wn6Z8s7ai5NA9MVX4vstHRsqP26QKJCzLg4JvFrp6mMaGB9 2013-07- 4dT04:30:27Z
change=1 # addr=16pJ6XkwSQv5ma5FSXMRPaXEYrENCEg47F
Kz3dVz7R6mUpXzdZy4gJEVZxXJwA15f198eVui4CUivXotzLBDKY 2013-07- 4dT04:30:27Z
change=1 # addr=17oJds8kaN8LP8kuAkWTco6ZM7BGXFC3gk
[... many more keys ...]

$
```

### 3.2.4 钱包地址及接收交易

命令：`getnewaddress`、`getreceivedbyaddress`、`listtransactions`、`getaddressesbyaccount`、`getbalance`

比特币参考客户端维护了一个地址池，地址池的大小可以用`getinfo`命令`keypoolsize`参数获取。这些地址是自动生成的，可以被用作公开接收地址或零钱地址。使用`getnewaddress`命令可以获得其中的一个地址：

```
$ bitcoin-cli getnewaddress
1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL
```

现在我们可以使用这个地址从一个外部钱包（假设你在其他交易所、在线钱包或其他bitcoind钱包有一些比特币）向我们的bitcoind钱包发送一小笔比特币。在本例中，我们将向下面的地址中发送50mBTC（0.050比特币）。

我们可以询问bitcoind客户端此地址已经接收到的比特币数额，以及指定该数额要被加到余额中所需要的确认数。在本例中，我们指定只需要0个确认。在从另一个钱包发送比特币数秒之后，我们将在这个钱包看到反应。我们用`getreceivedbyaddress`命令、这个地址及设置确认数为0：

```
$ bitcoin-cli getreceivedbyaddress 1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL 0
0.05000000
```

如果我们忽略这个命令后面的0，我们将只能在至少`minconf`个确认之后才能看到数额，`minconf`是想要某笔交易出现在余额中所设置的最少确认数。`minconf`设置在bitcoind配置文件指定。由于这笔发送比特币的交易仅在数秒之前完成，它还没有被确认，因而我们将看到余额是0：

```
$ bitcoin-cli getreceivedbyaddress 1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL
0.00000000
```

整个钱包接收到的交易可以通过使用`listtransactions`命令展示出来：

```
$ bitcoin-cli listtransactions
[
  {
      "account" : "",
      "address":"1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL",
      "category" : "receive",
      "amount" : 0.05000000,
      "confirmations" : 0,
      "txid" : "9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309ac
bae2c14ae3",
      "time" : 1392660908,
      "timereceived" : 1392660908
  }
]
```

我们可以使用`getaddressesbyaccount`命令列出整个钱包的所有地址：

```
$ bitcoin-cli getaddressesbyaccount ""
[
     "1LQoTPYy1TyERbNV4zZbhEmgyfAipC6eqL",
     "17vrg8uwMQUibkvS2ECRX4zpcVJ78iFaZS",
     "1FvRHWhHBBZA8cGRRsGiAeqEzUmjJkJQWR",
     "1NVJK3JsL41BF1KyxrUyJW5XHjunjfp2jz",
     "14MZqqzCxjc99M5ipsQSRfieT7qPZcM7Df",
     "1BhrGvtKFjTAhGdPGbrEwP3xvFjkJBuFCa",
     "15nem8CX91XtQE8B1Hdv97jE8X44H3DQMT",
     "1Q3q6taTsUiv3mMemEuQQJ9sGLEGaSjo81",
     "1HoSiTg8sb16oE6SrmazQEwcGEv8obv9ns",
     "13fE8BGhBvnoy68yZKuWJ2hheYKovSDjqM",
     "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL",
     "1KHUmVfCJteJ21LmRXHSpPoe23rXKifAb2",
     "1LqJZz1D9yHxG4cLkdujnqG5jNNGmPeAMD"
]
```

最后，`getbalance`命令将显示所有经过至少`minconf`个确认的交易加和后的余额：

```
$ bitcoin-cli getbalance
0.05000000
```

> ![](Images/Icon 1.png) 
<br> 如果交易还未被确认，getbalance返回的余额将为0。配置项“minconf”决定了交易在余额中体现的最少确认数。

### 3.2.5 探索及解码交易

命令：`gettransaction`、`getrawtransaction`、`decoderawtransaction`

我们将使用`gettransaction`命令探索前面列出的入账交易。我们使用`gettransaction`命令通过交易哈希值获取一笔交易，交易哈希值出现在前面的txid条目：

```
$ bitcoin-cli gettransaction
9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3
{
     "amount" : 0.05000000,
     "confirmations" : 0,
     "txid":"9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3",
     "time" : 1392660908,
     "timereceived" : 1392660908,
     "details" : [
    {
     "account" : "",
     "address":"1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL",
     "category" : "receive",
     "amount" : 0.05000000
    }
  ]
}
```
> ![](Images/Icon 1.png) 
<br> 交易ID在交易确认之前并不权威。区块链中找不到交易哈希值并不意味着此笔交易没有进行。这被称作“交易延展性”，因为交易哈希值在区块确认之前是可以更改的。在确认之后txid是不变且权威的。

用`gettransaction`命令显示的交易格式为简化格式。若要得到整个交易代码并且将之解码，我们将使用两个命令：`getrawtransaction`和`decoderawtransaction`。第一，`getrawtransaction`把交易哈希值（txid）当做一个参数，并且把整个交易以一个“原始”的十六进制字符串的形式返回，而这也正是交易在比特币网络上存在的形式：

```
$ bitcoin-cli getrawtransaction 9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae30100000001d717279515f88e2f56ce4e8a31e2ae3e9f00ba1d0add648e80c480ea22e0c7d3000000008b483045022100a4ebbeec83225dedead659bbde7da3d026c8b8e12e61a2df0dd0758e227383b302203301768ef878007e9ef7c304f70ffaf1f2c975b192d34c5b9b2ac1bd193dfba2014104793ac8a58ea751f9710e39aad2e296cc14daa44fa59248be58ede65e4c4b884ac5b5b6dede05ba84727e34c8fd3ee1d6929d7a44b6e111d41cc79e05dbfe5ceaffffffff02404b4c00000000001976a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac1f312906000000001976a914107b7086b31518935c8d28703d66d09b3623134388ac00000000
```

要解码这个十六进制字符串，我们使用`decoderawtransaction`命令。复制粘贴这个十六进制字符串作为`decoderawtransaction`的第一个参数以将整个内容解读为JSON数据格式（由于格式原因，在下面例子中十六进制字符串被缩短）：

```
$ bitcoin-cli decoderawtransaction 0100000001d717...388ac00000000
{
    "txid":"9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3",
    "version" : 1,
    "locktime" : 0,
    "vin" : [
        {
                "txid":"d3c7e022ea80c4808e64dd0a1dba009f3eaee2318a4ece562f8ef815952717d7",
            "vout" : 0,
            "scriptSig" : {
                "asm" : "3045022100a4ebbeec83225dedead659bbde7da3d026c8b8e12e61a2df0dd0758e227383b302203301768ef878007e9ef7c304f70ffaf1f2c975b192d34c5b9b2ac1bd193dfba20104793ac8a58ea751f9710e39aad2e296cc14daa44fa59248be58ede65e4c4b↵
884ac5b5b6dede05ba84727e34c8fd3ee1d6929d7a44b6e111d41cc79e05dbfe5cea",
                "hex": "483045022100a4ebbeec83225dedead659bbde7da3d026c8b8e12e61a2df0dd0758e227383b302203301768ef878007e9ef7c304f70ffaf1f2c975b192d34c5b9b2ac1bd193dfba2014104793ac8a58ea751f9710e39aad2e296cc14daa44fa59248be58ede65e4c4b884ac5b5b6dede05ba84727e34c8fd3ee1d6929d7a44b6e111d41cc79e05dbfe5cea"
            },
            "sequence" : 4294967295
        }
    ],
    "vout" : [
        {
            "value" : 0.05000000,
            "n" : 0,
            "scriptPubKey" : {
                "asm" : "OP_DUP OP_HASH160 07bdb518fa2e6089fd810235cf1100c9c13d1fd2 OP_EQUALVERIFY OP_CHECKSIG",
                "hex" :"76a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac",
                "reqSigs" : 1,
                "type" : "pubkeyhash",
                "addresses" : [
                    "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL"
                ]
            }
        },
        {
            "value" : 1.03362847,
            "n" : 1,
            "scriptPubKey" : {
                "asm" : "OP_DUP OP_HASH160 107b7086b31518935c8d28703d66d09b36231343 OP_EQUALVERIFY OP_CHECKSIG",
                "hex" : "76a914107b7086b31518935c8d28703d66d09b3623134388ac",
                "reqSigs" : 1,
                "type" : "pubkeyhash",
                "addresses" : [
                    "12W9goQ3P7Waw5JH8fRVs1e2rVAKoGnvoy"
                ]
            }
        }
    ]
}
```

交易解码展示这笔交易的所有成分，包括交易的输入及输出。在这个例子中，我们可以看到这笔给我们新地址存入50mBTC的交易使用了一个输入并且产生两个输出。这笔交易的输入是前一笔确认交易的输出（展示位以d3c7开头的vin txid）。两个输出则是50mBTC存入额度及返回给发送者的找零。

我们可以使用相同命令（例如`gettransaction`）通过检查由本次交易的txid索引的前一笔交易进一步探索区块链。通过从一笔交易跳到另外一笔交易，我们可以追溯一连串的交易，因为币值一定是从一个拥有者的地址传送到另一个拥有者的地址。

一旦我们接收到的交易以记录在区块中的方式被确认，`gettransaction`命令将返回附加信息，显示包含交易的区块的哈希值（标识符）。

```
$ bitcoin-cli gettransaction 9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3
{
    "amount" : 0.05000000,
    "confirmations" : 1,
    "blockhash" : "000000000000000051d2e759c63a26e247f185ecb7926ed7a6624bc31c2a717b",
    "blockindex" : 18,
    "blocktime" : 1392660808,
    "txid" : "9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3",
    "time" : 1392660908,
    "timereceived" : 1392660908,
    "details" : [
        {
            "account" : "",
            "address" : "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL",
            "category" : "receive",
            "amount" : 0.05000000
        }
    ]
}
```

这里，我们在区块哈希值（这笔交易所在区块的哈希值）条目看到新信息，以及值为18的区块索引（表明我们的交易为此区块的第18笔交易）。

> ###交易数据库索引及txindex选项

> 比特币核心默认建立包含仅与用户钱包相关交易的数据库。若你想使用类似`gettransaction`的命令访问所有交易，你需要配置比特币核心去建立一个完整的交易索引，这个可以通过txindex选项实现。在比特币核心配置文件中将`txindex`赋值为1（通常在安装目录的*.bitcoin/bitcoin.conf*中可以找到）。一旦你改变了此参数，你需要重启bitcoind，并等待其重建索引。

### 3.2.6 探索区块

命令：`getblock`、`getblockhash`

既然我们知道我们的交易在哪个区块中，我们可以使用`getblock`命令，并把区块哈希值作为参数来查询对应的区块：

```
$ bitcoin-cli getblock 000000000000000051d2e759c63a26e247f185ecb7926ed7a6624b↵ c31c2a717b true
{
    "hash" : "000000000000000051d2e759c63a26e247f185ecb7926ed7a6624bc31c2a717
b",
    "confirmations" : 2,
    "size" : 248758,
    "height" : 286384,
    "version" : 2,
    "merkleroot" : "9891747e37903016c3b77c7a0ef10acf467c530de52d84735bd55538719f9916",
    "tx" : [
        "46e130ab3c67d31d2b2c7f8fbc1ca71604a72e6bc504c8a35f777286c6d89bf0",
        "2d5625725b66d6c1da88b80b41e8c07dc5179ae2553361c96b14bcf1ce2c3868",
        "923392fc41904894f32d7c127059bed27dbb3cfd550d87b9a2dc03824f249c80",
        "f983739510a0f75837a82bfd9c96cd72090b15fa3928efb9cce95f6884203214",
        "190e1b010d5a53161aa0733b953eb29ef1074070658aaa656f933ded1a177952",
        "ee791ec8161440262f6e9144d5702f0057cef7e5767bc043879b7c2ff3ff5277",
        "4c45449ff56582664abfadeb1907756d9bc90601d32387d9cfd4f1ef813b46be",
        "3b031ed886c6d5220b3e3a28e3261727f3b4f0b29de5f93bc2de3e97938a8a53",
        "14b533283751e34a8065952fd1cd2c954e3d37aaa69d4b183ac6483481e5497d",
        "57b28365adaff61aaf60462e917a7cc9931904258127685c18f136eeaebd5d35",
        "8c0cc19fff6b66980f90af39bee20294bc745baf32cd83199aa83a1f0cd6ca51",
        "1b408640d54a1409d66ddaf3915a9dc2e8a6227439e8d91d2f74e704ba1cdae2",
        "0568f4fad1fdeff4dc70b106b0f0ec7827642c05fe5d2295b9deba4f5c5f5168",
        "9194bfe5756c7ec04743341a3605da285752685b9c7eebb594c6ed9ec9145f86",
        "765038fc1d444c5d5db9163ba1cc74bba2b4f87dd87985342813bd24021b6faf",
        "bff1caa9c20fa4eef33877765ee0a7d599fd1962417871ca63a2486476637136",
        "d76aa89083f56fcce4d5bf7fcf20c0406abdac0375a2d3c62007f64aa80bed74",
        "e57a4c70f91c8d9ba0ff0a55987ea578affb92daaa59c76820125f31a9584dfc",
        "9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3",
      
#[... many more transactions ...]

    ],
    "time" : 1392660808,
    "nonce" : 3888130470,
    "bits" : "19015f53",
    "difficulty" : 3129573174.52228737,
    "chainwork" : "000000000000000000000000000000000000000000001931d1658fc04879e466",
    "previousblockhash" : "0000000000000000177e61d5f6ba6b9450e0dade9f39c257b4d48b4941ac77e7",
    "nextblockhash" : "0000000000000001239d2c3bf7f4c68a4ca673e434702a57da8fe0d829a92eb6" 
    ```

这个区块包含367笔交易，并且如你所见，列出的第18笔交易（`9ca8f9…`）就是存入50mBTC到我们地址的txid我们可以通过heigh条目来判断：这就是整个区块链中第286,384个区块。

我们同样可以使用`getblockhash`命令通过区块高度来检索一个区块，这样需要将区块高度作为参数，并返回那个区块的区块哈希值。

```
$ bitcoin-cli getblockhash 0000000000019d6689c085ae165831e934ff763ae46a2a6c17↵
    2b3f1b60a8ce26f
$ bitcoin-cli getblockhash 
```

这里，我们获得了“创世区块”的区块哈希值，这是被中本聪所挖的第一个区块，高度为0。所获得的区块信息如下：

```
$ bitcoin-cli getblock 000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1↵
b60a8ce26f
{
    "hash" : "000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26↵f",
    "confirmations" : 286388,
    "size" : 285,
    "height" : 0,
    "version" : 1,
    "merkleroot" : "4a5e1e4baab89f3a32518a88c31bc87f618f76673e2cc77ab2127b7af↵
    deda33b",
    "tx" : [
        "4a5e1e4baab89f3a32518a88c31bc87f618f76673e2cc77ab2127b7afdeda33b"
    ],
    "time" : 1231006505,
    "nonce" : 2083236893,
    "bits" : "1d00ffff",
    "difficulty" : 1.00000000,
    "chainwork" : "0000000000000000000000000000000000000000000000000000000100010001",
    "nextblockhash" : "00000000839a8e6886ab5951d76f411475428afc90947ee320161bbf18eb6048"
    }
    ```
    
`getblock`、`getblockhash`和`gettransaction`命令可以按照一定编程准则，去探索区块链数据库。

### 3.2.7 基于UTXO（未花费的交易输出）的建立、签名与提交

命令：`listunspent`、`gettxout`、`createrawtransaction`、`decoderawtransaction`、`signrawtransaction`、`sendrawtransaction`  

比特币的交易是基于花费“输出”上的，即上一笔交易的支出，整个交易在地址之间转移所有权。我们的钱包现在收到了一笔向我们钱包地址发来的钱（输出）。一旦它被确定之后，那笔钱就属于我们了。

首先，我们可以使用`listunspent`命令去查看我们钱包中所有剩余的从之前交易中已确认的支出：

   ```
$ bitcoin-cli listunspent
[
    { 
        "txid" : "9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3",
        "vout" : 0,
        "address" : "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL",
        "account" : "",
        "scriptPubKey" : "76a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac",
        "amount" : 0.05000000,
        "confirmations" : 7
    } 
] 
```

我们发现交易`9ca8f9`建立了一个被指派到`1hvzSo`地址的输出（“vout”一项为0）对于50mBTC数量的比特币在这个时间点已经收到了7次确认。通过参考交易之前的txit和vout指数，交易系统将先前的输出变为本次的输入。我们现在可以创立一个花费第0个vout的易`9ca8f9`的账单。利用他的输入分配成新的输出，即给新地址赋值。

首先，让我们仔细观察输出的结果。我们可以使用`gettxout`命令来得到未花费的输出的详细细节。交易输出通常可以参考txid和vout两个指标。以下就是我们通过`gettxout`命令得到的结果：

```
$ bitcoin-cli gettxout 9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3 0
{
    "bestblock" : "0000000000000001405ce69bd4ceebcdfdb537749cebe89d371eb37e13899fd9",
    "confirmations" : 7,
    "value" : 0.05000000,
    "scriptPubKey" : {
        "asm" : "OP_DUP OP_HASH160 07bdb518fa2e6089fd810235cf1100c9c13d1fd2
        OP_EQUALVERIFY OP_CHECKSIG",
        "hex" : "76a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac",
        "reqSigs" : 1,
        "type" : "pubkeyhash",
        "addresses" : [
            "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL"
        ]
    },
    "version" : 1,
    "coinbase" : false
}
```

在这里我们看到由50mBTC分配到我们的账户地址`1hvz…`中。如果我们想用掉剩余的比特币，我们要重新建立一笔新的交易。首先，我们为这笔交易建立一个新的地址，告诉它将去往哪里：

```
$ bitcoin-cli getnewaddress 1LnfTndy3qzXGN19Jwscj1T8LR3MVe3JDb
```

我们将25mBTC送往我们钱包中新的地址`1LnfTn…`。在这笔新的交易中，我们将要花费50mBTC并且放入25mBTC到这个新地址中。因为我们必须花费所有之前交易的输出，同时我们必然产生一些找零。我们将产生的找零放回1hvz…的地址之中，即将找零放回到原先产生比特币的地址之中。最后，我们必须为这次交易支出一些费用——我们将0.5mBTC作为交易费，最终再存入24.5mBTC的找零。新的输出（25mBTC＋24.5mBTC＝49.5mBTC）和输入（50 mBTC）之间的差额就是奖励给矿工的交易费。

我们用`createrawtransaction`命令去建立一笔交易。我们将交易的收入（50已确认未支出的mBTC）和两笔交易的输出（送往新地址的比特币和从原先账户找回的零钱）作为`createrawtransaction`的参数。

```
$ bitcoin-cli createrawtransaction '[{"txid" : "9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3", "vout" : 0}]' '{"1LnfTndy3qzXGN19Jwscj1T8LR3MVe3JDb": 0.025, "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL": 0.0245}'
    
0100000001e34ac1e2baac09c366fce1c2245536bda8f7db0f6685862aecf53ebd69f9a89c0000000000ffffffff02a0252600000000001976a914d90d36e98f62968d2bc9bbd68107564a156a9bcf88ac50622500000000001976a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac00000000
```

`createrawtransaction`命令产生了一个原始十六进制字符串，其中编码了这笔交易的诸多细节。我们首先要通过`decoderawtransaction`命令来解码这个字符串，以确认所有的细节准确无误:

```
 $ bitcoin-cli decoderawtransaction 0100000001e34ac1e2baac09c366fce1c2245536bda8f7db0f6685862aecf53ebd69f9a89c0000000000ffffffff02a0252600000000001976a914d90d36e98f62968d2bc9bbd68107564a156a9bcf88ac50622500000000001976a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac00000000
{
    "txid" : "0793299cb26246a8d24e468ec285a9520a1c30fcb5b6125a102e3fc05d4f3cba",
    "version" : 1,
    "locktime" : 0,
    "vin" : [
        {
            "txid" : "9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3",
            "vout" : 0,
            "scriptSig" : {
                "asm" : "",
                "hex" : "" 
            },
            "sequence" : 4294967295
        }
    ],
    "vout" : [
        {
            "value" : 0.02500000,
            "n" : 0,
            "scriptPubKey" : {
                "asm" : "OP_DUP OP_HASH160 d90d36e98f62968d2bc9bbd68107564a156a9bcf OP_EQUALVERIFY OP_CHECKSIG",
                "hex" : "76a914d90d36e98f62968d2bc9bbd68107564a156a9bcf88ac",
                "reqSigs" : 1,
                "type" : "pubkeyhash",
                "addresses" : [
                    "1LnfTndy3qzXGN19Jwscj1T8LR3MVe3JDb"
                ]
            }
        },
        {
            "value" : 0.02450000,
            "n" : 1,
            "scriptPubKey" : {
                "asm" : "OP_DUP OP_HASH160 07bdb518fa2e6089fd810235cf1100c9c13d1fd2 OP_EQUALVERIFY OP_CHECKSIG",
                "hex" : "76a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac",
                "reqSigs" : 1,
                "type" : "pubkeyhash",
                "addresses" : [
                    "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL"
                ]
            } 
        }
    ] 
} 
```

结果无误！我们的交易“消耗了”从我们已确认的交易中未花费的输出，然后将它变成两笔输出，一个是走向了新地址的25mBTC，另一个是从原来地址返回的24.5mBTC零钱。这之间0.5mBTC的差额作为交易费，以奖励挖出包含我们这笔交易区块的矿工。

你有可能注意到，交易中包含一个空的条目`scriptSig`，因为我们并没有给它签名。如果没有签名，那么交易是没有意义的；同时我们也不能证明我们拥有未花费的输出的来源地址的所有权。通过签名，我们移除了输出上的障碍同时证明了我们的输出可靠。我们使用`signrawtransaction` 命令去签名交易。它需要原始十六进制的字符串作为参数：

> ![](Images/Icon 1.png) 
<br> 一个加密的钱包在签名之前必须解密，因为签名需要利用钱包中的秘钥。

```
$ bitcoin-cli walletpassphrase foo 360
$ bitcoin-cli signrawtransaction 0100000001e34ac1e2baac09c366fce1c2245536bda8↵
f7db0f6685862aecf53ebd69f9a89c0000000000ffffffff02a0252600000000001976a914d90↵
d36e98f62968d2bc9bbd68107564a156a9bcf88ac50622500000000001976a91407bdb518fa2e↵
6089fd810235cf1100c9c13d1fd288ac00000000
{
    "hex" : "0100000001e34ac1e2baac09c366fce1c2245536bda8f7db0f6685862aecf53ebd69f9a89c000000006a47304402203e8a16522da80cef66bacfbc0c800c6d52c4a26d1d86a54e0a1b76d661f020c9022010397f00149f2a8fb2bc5bca52f2d7a7f87e3897a273ef54b277e4af52051a06012103c9700559f690c4a9182faa8bed88ad8a0c563777ac1d3f00fd44ea6c71dc5127ffffffff02a0252600000000001976a914d90d36e98f62968d2bc9bbd68107564a156a9bcf88ac50622500000000001976a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac00000000",
    "complete" : true
    }
```

输入`signrawtransaction`命令后，得到另一串十六进制的原始加密交易。我们要对它进行解密，然后去查看发生的变化，请输入`decoderawtransaction`命令：

```
$ bitcoin-cli decoderawtransaction0100000001e34ac1e2baac09c366fce1c2245536bda8f7db0f6685862aecf53ebd69f9a89c000000006a47304402203e8a16522da80cef66bacfbc0c800c6d52c4a26d1d86a54e0a1b76d661f020c9022010397f00149f2a8fb2bc5bca52f2d7a7f87e3897a273ef54b277e4af52051a06012103c9700559f690c4a9182faa8bed88ad8a0c563777ac1d3f00fd44ea6c71dc5127ffffffff02a0252600000000001976a914d90d36e98f62968d2bc9bbd68107564a156a9bcf88ac50622500000000001976a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac00000000
{
    "txid" : "ae74538baa914f3799081ba78429d5d84f36a0127438e9f721dff584ac17b346",
    "version" : 1,
    "locktime" : 0,
    "vin" : [
        {
            "txid" : "9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3",
            "vout" : 0,
            "scriptSig" : {
                "asm" : "304402203e8a16522da80cef66bacfbc0c800c6d52c4a26d1d86a54e0a1b76d661f020c9022010397f00149f2a8fb2bc5bca52f2d7a7f87e3897a273ef54b277e4af52051a0601 03c9700559f690c4a9182faa8bed88ad8a0c563777ac1d3f00fd44ea6c71dc5127",
                "hex" : "47304402203e8a16522da80cef66bacfbc0c800c6d52c4a26d1d86a54e0a1b76d661f020c9022010397f00149f2a8fb2bc5bca52f2d7a7f87e3897a273ef54b277e4af52051a06012103c9700559f690c4a9182faa8bed88ad8a0c563777ac1d3f00fd44ea6c71dc5127"
}, 
            "sequence" : 4294967295
        }
    ],
    "vout" : [ 
        {
            "value" : 0.02500000,
            "n" : 0,
            "scriptPubKey" : {
                "asm" : "OP_DUP OP_HASH160 d90d36e98f62968d2bc9bbd68107564a156a9bcf OP_EQUALVERIFY OP_CHECKSIG",
                "hex" : "76a914d90d36e98f62968d2bc9bbd68107564a156a9bcf88ac",
                "reqSigs" : 1,
                "type" : "pubkeyhash",
                "addresses" : [
                    "1LnfTndy3qzXGN19Jwscj1T8LR3MVe3JDb"
                ]
            } 
        }, 
        {
            "value" : 0.02450000,
            "n" : 1,
            "scriptPubKey" : {
                "asm" : "OP_DUP OP_HASH160 07bdb518fa2e6089fd810235cf1100c9c13d1fd2 OP_EQUALVERIFY OP_CHECKSIG",
                "hex" : "76a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac",
                "reqSigs" : 1,
                "type" : "pubkeyhash",
                "addresses" : [
                    "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL"
                ]
            } 
        } 
    ] 
} 
```

现在，交易中的收入包含了`scritSig`，一串证明钱包地址`1hvz…`所有权的数字签名，同时移除了支出上的障碍，然后我们可以对钱包中的钱进行消费。签名可以让这笔交易被比特币交易网络中的任何节点验证，使他们变得可靠。

现在，该是提交新交易到比特币网络的时候了。我们使用由原始十六进制`signrawtransaction`命令生成的`sendrawtransaction`命令。以下就是和刚才解码时类似的字符串：

```
$ bitcoin-cli sendrawtransaction0100000001e34ac1e2baac09c366fce1c2245536bda8f7db0f6685862aecf53ebd69f9a89c000000006a47304402203e8a16522da80cef66bacfbc0c800c6d52c4a26d1d86a54e0a1b76d661f020c9022010397f00149f2a8fb2bc5bca52f2d7a7f87e3897a273ef54b277e4af52051a06012103c9700559f690c4a9182faa8bed88ad8a0c563777ac1d3f00fd44ea6c71dc5127ffffffff02a0252600000000001976a914d90d36e98f62968d2bc9bbd68107564a156a9bcf88ac50622500000000001976a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac00000000ae74538baa914f3799081ba78429d5d84f36a0127438e9f721dff584ac17b346
```

当使用`sendrawtransaction`命令发布交易到比特币网络时，它会返回交易的哈希值。我们现在可以通过`gettransaction`命令查询交易ID：

```
 $ bitcoin-cli gettransaction ae74538baa914f3799081ba78429d5d84f36a0127438e9f721dff584ac17b346
{
    "amount" : 0.00000000,
    "fee" : -0.00050000,
    "confirmations" : 0,
    "txid" : "ae74538baa914f3799081ba78429d5d84f36a0127438e9f721dff584ac17b346", 
    "time" : 1392666702,
    "timereceived" : 1392666702,
    "details" : [
        {
            "account" : "",
            "address" : "1LnfTndy3qzXGN19Jwscj1T8LR3MVe3JDb",                "category" : "send",
            "amount" : -0.02500000,
            "fee" : -0.00050000
        }, 
        {
            "account" : "",
            "address" : "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL",                 "category" : "send",
            "amount" : -0.02450000,
            "fee" : -0.00050000
        }, 
        {
            "account" : "",
            "address" : "1LnfTndy3qzXGN19Jwscj1T8LR3MVe3JDb",                "category" : "receive",
            "amount" : 0.02500000
        }, 
        {
            "account" : "",
            "address" : "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL",                 "category" : "receive",
            "amount" : 0.02450000
        }
    ]
}
```

和以前一样，我们同样可以通过使用`getrawtransaction`和`decodetransaction`命令来检查交易中的细节。这些命令会得到一个在发送到比特币网络之前进行编码和解码并且十分精准的原始十六进制字符串。

## 3.3 其他替代客户端、资料库、工具包

除了参考客户端（bitcoind），还可以使用其他的客户端和资料库去连接比特币网络和数据结构。这些工具都由一系列的编程语言执行，用他们各自的语言为比特币程序提供原生的交互。

其他的执行方式包括：

▷ [libbitcoin和sx tools](https://libbitcoin.dyne.org/)
<br>一款C++，通过命令行完成的全节点多线程客户端与程序库

▷ [bitcoinj](https://bitcoinj.github.io/)
<br>一款全节点java客户端和程序库

▷ [btcd](https://opensource.conformal.com/wiki/btcd)
<br>一款全节点GO 语言的比特币客户端

▷ [Bits of Proof（BOP）](https://bitsofproof.com/)
<br>一款Java企业级平台的比特币工具

▷ [picocoin](https://github.com/jgarzik/picocoin)
<br>一款轻量级比特币执行客户端

▷ [pybitcointools](https://github.com/vbuterin/pybitcointools)
<br>一款Python语言的比特币程序库

▷ [pycoin](https://github.com/richardkiss/pycoin)
<br>另一款Python语言的比特币程序库

在其他的编程语言中，还有许多形式的比特币（程序）库。开发者也尽其所能，一直在尽力创造新的比特币工具。

### 3.3.1 Libbitcoin和sx Tools

Libbitcoin程序是一款基于C++层面，可扩展、多线程、模块化的执行工具。它可以支持全节点客户端和一款叫做sx的命令行工具，并可以提供我们本章所讨论的比特币命令相同的功能。Sx工具同时提供了管理和操作工具，是bitcoind所不能提供的，包括type-2型确定性密钥和密码助记工具。

####安装sx

若要安装sx工具以及相关libbitcoin库，请在Linux操作系统中下载并安装在线安装包:

```
$ wget http://sx.dyne.org/install-sx.sh
$ sudo bash ./install-sx.sh
```

现在你应当已经安装好了sx工具。输入没有参数的sx命令来显示帮助文档，帮助文档列出了所有可用的命令（详见附录4）。

> ![](Images/Icon 1.png) 
<br> sx工具提供了许多实用的编码与解码地址的命令，可以从不同的编码方式转化，也可以转化成不同的方式。通过他们，可以探索更多的编码方式，比如Base58，Base58Check，hex，等等。
	
### 3.3.2 pycoin

[pycoin](https://github.com/richardkiss/pycoin)最初由Richard Kiss创立并维护，是一款基于Python库，并可以支持比特币密钥的操作和交易的客户端，甚至可以支持编译语言从而处理非标准交易。

Pycoin库同时支持Python2（2.7x）与Python3，以及一些便于使用的命令行工具，比如ku和tx。如果在Python3的虚拟环境下安装 pycoin0.42，请输入以下命令：

```
$ python3 -m venv /tmp/pycoin
$ . /tmp/pycoin/bin/activate
$ pip install pycoin==0.42
Downloading/unpacking pycoin==0.42
  Downloading pycoin-0.42.tar.gz (66kB): 66kB downloaded
  Running setup.py (path:/tmp/pycoin/build/pycoin/setup.py) egg_info for pack-age pycoin
    
Installing collected packages: pycoin
  Running setup.py install for pycoin
  
    Installing tx script to /tmp/pycoin/bin
    Installing cache_tx script to /tmp/pycoin/bin
    Installing bu script to /tmp/pycoin/bin
    Installing fetch_unspent script to /tmp/pycoin/bin
    Installing block script to /tmp/pycoin/bin
    Installing spend script to /tmp/pycoin/bin
    Installing ku script to /tmp/pycoin/bin
    Installing genwallet script to /tmp/pycoin/bin
Successfully installed pycoin
Cleaning up...
$
```

这里有一个简单的Python脚本，通过pycoin库来交易比特币：

  ```
#!/usr/bin/env python

from pycoin.key import Key 
from pycoin.key.validate import is_address_valid, is_wif_valid from pycoin.services import spendables_for_address
from pycoin.tx.tx_utils import create_signed_tx 

def get_address(which): 
    while 1: 
        print("enter the %s address=> " % which, end='') 
        address = input()
        is_valid = is_address_valid(address)
        if is_valid: 
            return address
        print("invalid address, please try again") 
        
src_address = get_address("source")
spendables = spendables_for_address(src_address) print(spendables) 

while 1:
    print("enter the WIF for %s=> " % src_address, end='') 
    wif = input()
    is_valid = is_wif_valid(wif)
    if is_valid: 
        break
    print("invalid wif, please try again") 

key = Key.from_text(wif)
if src_address not in (key.address(use_uncompressed=False), key.address(use_un compressed=True)): 
    print("** WIF doesn't correspond to %s" % src_address) 
print("The secret exponent is %d" % key.secret_exponent()) 
    
dst_address = get_address("destination")
    
tx = create_signed_tx(spendables, payables=[dst_address], wifs=[wif])
    
print("here is the signed output transaction") 
print(tx.as_hex()) 
```

更多的ku与tx命令行样例，请参考附录2。

### 3.3.3 btcd

btcd是一款基于Go语言的全节点比特币工具。目前，它通过使用精准的规则（包括bugs），下载、验证和服务区块链。它同时依靠新发掘出来的区块来维持交易池，同时依赖没有形成区块的单独交易。在缜密的规则以及检查下，确保了每笔独立交易的安全，并且可以过滤基于矿工需求的交易。

btcd与bitcoind的一个主要区别是btcd不包含比特币钱包的功能，其实这是一个精心的设计。这意味着你不能直接通过btcd进行比特币交易。然而这项功能可以由正在研发的btcwallet与btcgui两个项目提供。另一个显著的区别是btcd同时支持HTTP POST（比如bitcoind）与推荐使用的Websockets两种通信协议的请求。并且btcd的RPC连接默认设置为TLS-开启。

#### 安装btcd

若要安装Windows版btcd，请[从GitHub下载](https://github.com/btcsuite/btcd/releases)并运行msi；如果你已经安装了Go语言，请在Linux中输入以下命令行：

```
$ go get github.com/conformal/btcd/...
```

若要更新btcd到最新版本，请输入：

```
$ go get -u -v github.com/conformal/btcd/...
```

#### 调试btcd

btcd拥有许多配置选项，可以通过以下命令来查看：

```
$ btcd --help 
```

btcd预装了许多好用的功能包，比如btcctl。它是一种可以通过RPC来控制和查询的令行工具。Btcd并没有默认开启了RPC服务器，你必须通过以下命令行来配置RPC用户名及密码：

▷ btcd.conf:

```
[Application Options]
rpcuser=myuser
rpcpass=SomeDecentp4ssw0rd
```

▷btcctl.conf:

```
[Application Options]
rpcuser=myuser
rpcpass=SomeDecentp4ssw0rd
```

若果你想要重写配置，请输入以下命令：

```
$ btcd -u myuser -P SomeDecentp4ssw0rd
$ btcctl -u myuser -P SomeDecentp4ssw0rd
```

可以通过以下命令来查询一系列的选项：

```
$ btcctl --help
```

