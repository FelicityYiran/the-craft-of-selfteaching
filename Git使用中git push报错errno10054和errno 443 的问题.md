
Git使用中git push报错errno 10054 和errno 443 的问题
并且出现username 和password输入了也输入的情况的处理方法

这两天终于开始重新使用git，鉴于网络老卡了，所以就开了ssl(VPN)，clone没问题，但是在提交新的修改时，即完成git add. /git commit -am “ ** ”后在git push时就开始报错443和10054，在看到网上说要进行设置http.sslVerify "false"之后，即输入git config --global http.sslVerify "false" 后还是报错errno 10054，尝试更新hosts（可参考以下链接）(注意在修改好hosts后别忘了刷新hosts ,用“ipconfig /flushdns”刷新),就可以输入邮箱和密码了。
1）最新hosts地址
https://gitee.com/ChinaTiger9527/hosts
2）如何在windows修改hosts
https://blog.csdn.net/RedaTao/article/details/113366659


然后就出现了要输入git用户名和密码的情况，我是输入了好几次邮箱和密码，怎么输入都没有用，后来找到了这个链接，发现人家说是因为不能直接用密码，而是在command line的界面中必须用personal access token，然后试了果然有用，按照这个链接方式可以设置自己的personal access token（以下链接如果用chrom电脑端看不了，就发送到手机微信可以看，不知道为什么电脑端闪一下就不显示了）
https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
回答来源：
https://stackoverflow.com/questions/17659206/git-push-results-in-authentication-failed/21027728#21027728?newreg=c1e311fc6fb04a5ca31db4a995f5d968


最后还有个设置，本来我其实一开始我要是不动也没错，但是改着改着报错，就是这个system http.sslcainfo的报错，根据网上其他人的回答，别人的是这样的：
git config --system http.sslcainfo "C:\Program Files (x86)\git\bin\curl-ca-bundle.crt"
最后我试了我的curl-ca-bundle.crt文件，一共有6个位置，最后用的这个位置
C:\Users\TZB\scoop\apps\git\2.23.0.windows.1\mingw64\ssl\certs，就没有问题了，即：
git config --system http.sslcainfo “C:\Program Files (x86)\git\bin\curl-ca-bundle.crt"
这个是什么设置我也没搞懂，但是这么做有用所以先记录在这里，具体方式是在搜索自己电脑中的ca-bundle，然后一个个地址换着试试，然后就可能好了。
参考资料：
https://blog.csdn.net/sdhongjun/article/details/52144253
