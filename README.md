https://www.tpc.org/tpch/default5.asp

```sh
cd dbgen
cp makefile.suite Makefile

# Makefileを下記のように編集
CC = gcc
DATABASE = ORACLE
MACHINE = LINUX
WORKLOAD = TPCH
```

```sh
# 事前にgccとmakeをインストールしておく
# dbgenとqgenコマンドが作成されていたら成功
make
```

データの生成
```sh
# dbgenコマンドでデータを作成する
# -sオプションでscalefactorを指定。1で1GBほどのデータ作成になる
./dbgen -s 1

# 成功するとカレントディレクトリに.tbl拡張子のデータが生成される
# 各tblファイルは縦棒区切りでレコードが格納されている
```

クエリの生成
```sh
export DSS_QUERY=<dbgen/queriesディレクトリのフルパス>
# qgenのscalefactorも-sオプションでdbgenに合わせておく
# カレントディレクトリに出力される
for i in $(seq 1 22); do ./qgen -s 1 $i > $i.sql; done
```
