# oracle.2015
本リポジトリはDatabase2(オラクル)の授業に関する情報を共有するために使用する

## オラクルサーバへの接続するための環境設定手順

1. 「[Oracleインスタントクライアントのダウンロード](http://www.oracle.com/technetwork/jp/topics/index-099943-ja.html)から以下をダウンロードし、展開。  
「instantclient_12_1」ディレクトリが作成されていることを確認
	* instantclient-basic-linux.x64-12.1.0.2.0.zip
	* instantclient-sqlplus-linux.x64-12.1.0.1.0.zip  
1. 「非同期IO(libio)」のインストール  
$ sudo aptitude install libaio1  
1. 「リードラインラッパー(rlwrap)」のインストール  
$ sudo aptitude install rlwrap  
1. 「[oracle.2015](https://github.com/KimiyukiYamauchi/oracle.2015.git)」を「git clone」
  $ git clone https://github.com/KimiyukiYamauchi/oracle.2015.git (任意のディレクトリ名)  
1. cloneしたリポジトリに移動  
1. Oracleサーバへの接続確認  
	1. 接続のためのスクリプトを作成  
$ vi sqlplus.sh<br >
で、ファイルを開き、以下を入力。  
この時、「instantclient_12_1」ディレクトリのパスは各自の環境に  
沿って、記述すること  
::: ここから :::  
LD_LIBRARY_PATH=/home/yamauchi/instantclient_12_1  
PATH=/home/yamauchi/instantclient_12_1:$PATH  
NLS_LANG=JAPANESE_JAPAN.AL32UTF8  
export LD_LIBRARY_PATH PATH NLS_LANG  
export no_proxy=localhost,172.16.40.4  
echo -n "ユーザ名："  
read user  
stty -echo  
echo -n "パスワード："  
read pass  
stty echo  
rlwrap sqlplus $user/$pass@172.16.40.4:1521/db11  
::: ここまで :::
	2. 作成したスクリプトを実行し、接続できること  
$ ./sqlplus.sh  
ユーザ名：hr  
パスワード：hr (パスワードの入力はエコーバックしないので注意！)  
=> これで接続できること！  
6. 各自の環境の設定
	1. 各自のアカウントでサーバに接続  
$ ./sqlplus.sh  
ユーザ名：(学籍番号)  
パスワード：password (パスワードの入力はエコーバックしないので注意！)  
=> 各自のアカウントで接続される  
	1. テーブルを作成するためのスクリプトを実行  
SQL> @create_tbl_oracle.sql  
	1. 以下のSELECT文を実行し、テーブルが作成できていることを確認  
また、それぞれのテーブルに対して、SELECT文を実行し、データがちゃんと入っていることを確認  
SQL> select table_name from user_tables;  
SQL> select tname from tab;

		- ORDERS
		- ORD_DETAILS
		- SALGRADES
		- EMPLOYEES
		- PRODUCTS
		- CUSTOMERS
		- DEPARTMENTS