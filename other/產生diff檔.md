## 原因

* 在進行專案上版的時候會需要將有修改過的程式碼跟客戶講，這種情況在簡單的就是直接產生diff檔

## 方法

### git diff

* 如果專案有用 **git** 管控，可以用以下指令產生 diff 檔 or patch 檔
* 必須是在兩個不同的分支才能用以下指令
* 前面的branch是原始版本，後面的是修改過後的版本
```shell
git diff main release > main-vs-release.diff
```
 * 如果是要比較commit之間的不同可以用下面的指令，並且這個commit是可以不同branch的
 * 前面的commit 是原始版本，後面的是修改或後的版本
 ```shell
 git diff b71c3 a628c > test.diff
```

### diff -run

* 這個指令是內建在 **linus** 、**unix** 、**macOS** 裡面
* 如果要在windows裡面使用，可以安裝 **git bash** 然後在裡面使用
* 可以用這兩種方式排除不要比較的檔案
	* --exclude=obj  //這代表不要比較 obj 資料夾
	* -X exclude-list.txt //這代表將該txt裡面有寫到的東西排掉
 * 這個指令有區分大小寫

```txt
// exclude-list
bin
obj
package
Readme.md
```

```shell
$ diff -ruN   --exclude=bin   --exclude=obj   --exclude=packages --exclude=Readme.md /d/diff/origin/test /d/VSProjects/test > test.diff
```
* 上面跟下面的指令的結果是一樣的，因為都排除一樣的檔案、資料夾
```shell 
diff -ruN -X exclude-list.txt /d/diff/origin/test /d/VSProjects/test > test.diff
```

#diff #git