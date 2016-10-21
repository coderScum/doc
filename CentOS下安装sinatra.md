## CentOS下安装sinatra
###安装所需的工具包
通过一下命令安装所需的工具包

	yum install -y gcc-c++ patch readline readline-devel zlib zlib-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison sqlite-devel iconv-devel
###安装rvm
运行

	curl -sSL https://get.rvm.io | bash -s stable

如果出现

	Warning, RVM 1.26.0 introduces signed releases and automated check of signatures when GPG software found.  
	Assuming you trust Michal Papis import the mpapis public key (downloading the signatures).  
	  
	GPG signature verification failed for '/usr/local/rvm/archives/rvm-1.26.11.tgz' - 'https://github.com/rvm/rvm/releases/download/1.26.11/1.26.11.tar.gz.asc'!  
	try downloading the signatures:  
	  
	   gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3  
	  
	or if it fails:  
	  
	   command curl -sSL https://rvm.io/mpapis.asc | gpg2 --import -  
	  
	the key can be compared with:  
	  
	   https://rvm.io/mpapis.asc  
	   https://keybase.io/mpapis  

 那么复制

	gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3  

在控制台运行一次，然后再次运行

	curl -sSL https://get.rvm.io | bash -s stable

安装成功最后会提示：

	# Administrator,  
	#  
	#   Thank you for using RVM!  
	#   We sincerely hope that RVM helps to make your life easier and more enjoyable!!!  
	#  
	# ~Wayne, Michal & team. 
运行如下命令：

	echo "source /etc/profile.d/rvm.sh" >> ~/.bashrc && source /etc/profile.d/rvm.sh 

###使用rvm安装Ruby
使用下列命令查看Ruby版本：

	rvm list known
列出rvm知道的ruby版本，那么在这里就可以看到有什么版本可以安装了,下面命令安装2.3.0。

	rvm install ruby-2.3.0  

 rvm可以帮助我们将ruby所依赖的包也一起安装进来。
 
选择要使用的Ruby版本:
 
	 rvm use ruby-2.3.0
	 
输出变量参数:

	echo "export rvm_max_time_flag=20" >> ~/.rvmrc

如果未科学上网，可以更换 gem sources，替换成 `https://ruby.taobao.org`

	gem sources --remove https://rubygems.org/ 
	gem sources -a https://ruby.taobao.org
###安装 sinatra
通过gem安装**sinatra**

	gem install sinatra
###测试是否安装成功
创建 myapp.rb

	# myapp.rb
	require 'sinatra'
	
	get '/' do
	  'Hello world!'
	end
运行:

	ruby myapp.rb
内网:在该地址查看：` http://localhost:4567`
如果是外网，外网IP为：X.X.X.X
需要设置绑定IP，myapp.rb 变为如下：

	# myapp.rb
	require 'sinatra'
	set :bind, 'X.X.X.X'
	get '/' do
	  'Hello world!'
	end
在该地址查看：`http://X.X.X.X:4567`

如果sinatra 安装成功会在界面显示`Hello world!`



