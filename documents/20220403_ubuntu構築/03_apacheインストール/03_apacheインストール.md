# apacheインストール

作成日：2022-04-03

作成者：石田　和希

------

[TOC]

------





### 1.インストール

```bash
#  whoami
root


`インストール
# apt -y install apache2 



`apacheのバージョン情報をWEBに表示しないように設定
# vi /etc/apache2/conf-enabled/security.conf 
-----------------------------------------------------------------------------------------------------
#### 2022-04-03 CHANGE start (hisashi)
#### hisashi ####ServerTokens OS
ServerTokens Prod
#### 2022-04-03 CHANGE end (hisashi)
-----------------------------------------------------------------------------------------------------


`ディレクトリ名のみでアクセスできるファイル名を設定
# vi /etc/apache2/mods-enabled/dir.conf 
-----------------------------------------------------------------------------------------------------
<IfModule mod_dir.c>

    #### 2022-04-03 CHANGE start (hisashi)
    #### hisashi ####DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
    DirectoryIndex index.html index.php index.htm
    #### 2022-04-03 CHANGE end (hisashi)

</IfModule>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
-----------------------------------------------------------------------------------------------------


`サーバ情報設定
# vi /etc/apache2/apache2.conf 
-----------------------------------------------------------------------------------------------------
#### 2022-04-03 ADD start (hisashi)
ServerName www.hisashi.world
ServerAdmin k@hisashi.biz
#### 2022-04-03 ADD end (hisashi)
-----------------------------------------------------------------------------------------------------


`サービス再起動
# systemctl restart apache2.service


`ufw調整
# ufw allow in on ens160 to any port http
Rule added


`ブラウザでアクセスし、ページが表示されることを確認する
```




