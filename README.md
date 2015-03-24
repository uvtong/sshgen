<h1>概述</h1>
此脚本可以在服务器上快速生成用于登录的公钥和私钥，并自动修改配置文件（/etc/ssh/sshd_config），达到禁用明文密码登录的效果，快速布置安全的服务器环境。


<h1>使用方法</h1>
<h3>下载脚本</h3>
<pre><code>
git clone https://github.com/junorz/sshgen.git ~/.sshgen
</code></pre>

<h3>运行</h3>
<pre><code>
bash ~/.sshgen/gen.sh
</code></pre>

<h3>配置</h3>
<p>1.你可以自己设定密钥的密码，但是保持生成的文件位置为默认（/root/.ssh/）。</p>
<p>2.出现“Now please download id_rsa file you have generated just now and press Enter”提示后请使用WinSCP等软件下载位于服务器/root/.ssh/位置的id_rsa文件。</p>
<p>  或者在本地命令行输入<code>scp root@1.2.3.4:/root/.ssh/id_rsa ~/Documents/keys/id_rsa</code>（示例）进行下载。</p>
<p>3.出现“Please try logging in with key file, if it succeed please enter Y”提示后请在本地新开一个命令行使用ssh连接，并尝试使用密钥文件登录。</p>
<p><code>ssh root@1.2.3.4 -i ~/Documents/keys/id_rsa</code>（示例）</p>
<p>4.如果登录成功，输入y确认，脚本会自动禁用明文密码登录，此后仅能使用私钥来登录服务器，所以请保管好私钥。</p>
<p>5.如果登录不成功，请输入n或Ctrl+C取消脚本的运行，否则你将会无法登录服务器。</p>

<h1>如何实现免密码登录</h1>
<p>以Mac系统为例子，你需要把在第3步登录时使用的私钥加入系统的<code>~/.ssh/id_rsd</code>中，你可能需要先<code>touch ~/.ssh/id_rsa</code>来建立这个文件。</p>
<p>假设私钥的地址是<code>~/Documents/keys/id_rsa</code>，那么可以用这个命令加入到系统中（如果不这样做每次登录还需要那串长长的-i参数来指定私钥地址）：</p>
<pre><code>sudo cat ~/Documents/keys/id_rsa >> ~/.ssh/id_rsa</code></pre>
<p>然后你也许会想给服务器起个名字，因为每次ssh都要输入IP实在太麻烦了。</p>
<p>比如你有个在Linode的VPS，IP是1.2.3.4，那么可以这么写：</p>
<pre><code>sudo echo "1.2.3.4 linode1" >> /etc/hosts</code></pre>
<p>以后管理VPS时只需要<code>ssh root@linode1</code>就可以自动登录了，是不是很方便？</p>

<h1>注意</h1>
请自行承担使用此脚本后带来的一切后果。
