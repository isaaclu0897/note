#inProgress , #how-to, #nexus, #repository

### What is Nexus
### How to setup Nexus Server
1. download
https://help.sonatype.com/repomanager3/product-information/download
### How to setup Nexus Server as Yum repository management server?
### How to 
### How to backup/restore Nuexs data
備份db，db管yum設定、賬號設定等
備份blob

有點不知道這兩個有什麽差異，但是實驗過直接
備份~/sonatype-work/nexus3/{blob db}可以達到一樣的效果
在簡單一點也可以直接備份~/sonatype-work/nexus3，但是這樣會有很多垃圾資料，在長期使用後要想一下

nexus是什麽？
1. 

如何建立nexus？
1. https://help.sonatype.com/repomanager3/product-information/download

如何將nexus作爲yum repository？（hosted、proxy、group）

如何讓SUT連接nexus的yum repository？

如何上傳yum package到nexus？

如何下載yum package到nexus？

如何備份nexus數據？

備份db，db管yum設定、賬號設定等
備份blob

有點不知道這兩個有什麽差異，但是實驗過直接
備份~/sonatype-work/nexus3/{blob db}可以達到一樣的效果
在簡單一點也可以直接備份~/sonatype-work/nexus3，但是這樣會有很多垃圾資料，在長期使用後要想一下


https://help.sonatype.com/repomanager3/product-information/download/download-archives---repository-manager-3

外部代理跟内部倉庫要分開建立group


Deploying Packages to Yum Hosted Repositories
The Yum client does not come with a method for uploading RPMs; however, you can use many other tools to upload files to a hosted Yum repository using a simple HTTP PUT.

The following example uses the curl command and the admin user's default credentials to upload a test.rpm file to a hosted Yum repository with the name  test.rpm:

curl -v --user 'admin:admin123' --upload-file ./test.rpm http://localhost:8081/repository/yum-hosted/test.rpm
Be default, Yum metadata is generated after 60 seconds when you upload an RPM.

上傳nexus rpm的方法是用http put指令，之前
curl -v --user 'admin:admin' --upload-file ./test.rpm http://localhost:8081/repository/yum-hosted/test.rpm

nexus3
http://10.165.141.11:8081/
admin
xzdvcasdf <- 密碼要自己重新設定，第一次的密碼寫在安裝包文件中

download file
curl -v -O http://127.0.0.1:8081/repository/yum-local/8/x86_64/a.rpm

nexus2
http://10.165.141.11:8081/nexus/
admin
admin123

How do I Enable All Script Features in Version 3.21.2 and Newer
Edit $data-dir/etc/nexus.properties. Add the following on a new line, making sure the file is saved with an ending new line and with the original file permissions:
nexus.scripts.allowCreation=true
Restart NXRM to pick up the property change.

$data-dir/etc/nexus.properties
nexus.scripts.allowCreation=true
restart

cli
nexus3 download yum-local/7 test/ 下載到test folder


nexus3 download yum-local/7 . 下載到本地

在免費版還有很多東西做不到，但是都可以寫groovy脚本在server上作爲task運行
https://github.com/sonatype-nexus-community/nexus-scripting-examples/tree/master/nexus-script-example/src/main/groovy
https://gitlab.com/thiagocsf/nexus3-cli/-/blob/master/src/nexuscli/api/script/groovy/nexus3-cli-repository-get.groovy
https://nexus3-cli.readthedocs.io/en/latest/groovy-scripts.html#

目前的想法，可以把要導入的包都整合進nexus
fttcl開發的包

ref

> https://wiki.eryajf.net/pages/1803.html
> https://wiki.eryajf.net/pages/2002.html
> https://wiki.eryajf.net/pages/1b25e5/
