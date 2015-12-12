[ Languages:
[English](README.md), [Español](README-es.md), [Italiano](README-it.md), [日本語](README-ja.md), [한국어](README-ko.md), [Português](README-pt.md), [Русский](README-ru.md), [Slovenščina](README-sl.md), [Українська](README-uk.md), [中文](README-zh.md)
]


# 命令行的藝術

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [必讀](#必讀)
- [基礎](#基礎)
- [日常使用](#日常使用)
- [文件及數據處理](#文件及數據處理)
- [系統調試](#系統調試)
- [單行腳本](#單行腳本)
- [冷門但有用](#冷門但有用)
- [僅限 MacOS X 系統](#僅限-macos-x-系統)
- [更多資源](#更多資源)
- [免責聲明](#免責聲明)
- [授權條款](#授權條款)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

熟練使用命令行是一種常常被忽視，或被認爲難以掌握的技能，但實際上，它會提高你作爲工程師的靈活性以及生產力。本文是一份我在 Linux 上工作時，發現的一些命令行使用技巧的摘要。有些技巧非常基礎，而另一些則相當複雜，甚至晦澀難懂。這篇文章並不長，但當你能夠熟練掌握這裏列出的所有技巧時，你就學會了很多關於命令行的東西了。

這篇文章是[許多作者和譯者](AUTHORS.md)共同的成果。這裏的大部分內容
[首次](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[出現](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
於 [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know)，但考慮到這裏的人們都具有學習的天賦且樂於接受別人的建議，使用 Github 來做這件事是更佳的選擇。如果你在本文中發現了錯誤或者存在可以改善的地方，請果斷提交 Issue 或 Pull Request！(當然在提交前請看一下必讀節和已有的 PR/issue）。


## 必讀

涵蓋範圍：

- 這篇文章對剛接觸命令行的新手以及具有命令行使用經驗的人都有用處。本文致力於做到*覆蓋面廣*（儘量包括一切重要的內容），*具體*（給出最常見的具體的例子）以及*簡潔*（避免不必要的，或是可以在其他地方輕鬆查到的細枝末節）。每個技巧在特定情境下或是基本的，或是能顯著節約時間。
- 本文爲 Linux 所寫，除了[僅限 MacOS X 系統](#僅限-macos-x-系統)節。其它節中的大部分內容都適用於其它 Unix 系統或 MacOS 系統，甚至 Cygwin。
- 本文關注於交互式 Bash，儘管很多技巧也適用於其他 shell 或 Bash 腳本。
- 本文包括了“標準的”Unix 命令和需要安裝特定包的命令，只要它們足夠重要。

注意事項：

- 爲了能在一頁內展示儘量多的東西，一些具體的信息會被間接的包含在引用頁裏。聰明機智的你如果掌握了使用 Google 搜索引擎的基本思路與命令，那麼你將可以查閱到更多的詳細信息。使用 `apt-get`／`yum`／`dnf`／`pacman`／`pip`／`brew`（以及其它合適的包管理器）來安裝新程序。
- 使用 [Explainshell](http://explainshell.com/) 去獲取相關命令、參數、管道等內容的解釋。


## 基礎

- 學習 Bash 的基礎知識。具體來說，輸入 `man bash` 並至少全文瀏覽一遍; 它很簡單並且不長。其他的 shell 可能很好用，但 Bash 功能強大且幾乎所有情況下都是可用的 （ *只*學習 zsh，fish 或其他的 shell 的話，在你自己的電腦上會顯得很方便，但在很多情況下會限制你，比如當你需要在服務器上工作時）。

- 學習並掌握至少一個基於文本的編輯器。通常 Vim （`vi`） 會是你最好的選擇，因爲在終端裏進行隨機編輯 Vim 真的毫無敵手，哪怕是 Emacs、某大型 IDE 甚至時下非常流行的編輯器。

- 學會如何使用 `man` 命令去閱讀文檔。學會使用 `apropos` 去查找文檔。瞭解有些命令並不對應可執行文件，而是Bash內置的，可以使用 `help` 和 `help -d` 命令獲取幫助信息。

- 學會使用 `>` 和 `<` 來重定向輸出和輸入，學會使用 `|` 來重定向管道。明白 `>` 會覆蓋了輸出文件而 `>>` 是在文件未添加。瞭解標準輸出 stdout 和標準錯誤 stderr。

- 學會使用通配符 `*` （或許再算上 `?` 和 `[`...`]`） 和引用以及引用中 `'` 和 `"` 的區別。

- 熟悉 Bash 任務管理工具：`&`，**ctrl-z**，**ctrl-c**，`jobs`，`fg`，`bg`，`kill` 等。

- 瞭解 `ssh`，以及學會通過使用 `ssh-agent`，`ssh-add` 等命令來實現基本的無密碼認證。

- 學會基本的文件管理：`ls` 和 `ls -l` （瞭解 `ls -l` 中每一列代表的意義），`less`，`head`，`tail` 和 `tail -f` （甚至 `less +F`），`ln` 和 `ln -s` （瞭解硬鏈接與軟鏈接的區別），`chown`，`chmod`，`du` （硬盤使用情況概述：`du -hs *`）。 關於文件系統的管理，學習 `df`，`mount`，`fdisk`，`mkfs`，`lsblk`。知道 inode 是什麼（與 `ls -i` 和 `df -i` 等命令相關）。

- 學習基本的網絡管理：`ip` 或 `ifconfig`，`dig`。

- 熟悉正則表達式，以及 `grep`／`egrep` 裏不同參數的作用，例如 `-i`，`-o`，`-v`，`-A`，`-B` 和 `-C`，這些參數是值得學習並掌握的。

- 學會使用 `apt-get`，`yum`，`dnf` 或 `pacman` （取決於你使用的 Linux 發行版）來查找或安裝軟件包。並確保你的環境中有 `pip` 來安裝基於 Python 的命令行工具 （接下來提到的部分程序使用 `pip` 來安裝會很方便）。


## 日常使用

- 在 Bash 中，可以使用 **Tab** 自動補全參數，使用 **ctrl-r** 搜索命令行歷史（在按下之後，鍵入便可以搜索，重覆按下 **ctrl-r** 會在更多匹配中循環，按下 **Enter** 會執行找到的命令，按下右方向鍵會將結果放入當前行中，使你可以進行編輯）。

- 在 Bash 中，可以使用 **ctrl-w** 刪除你鍵入的最後一個單詞，使用 **ctrl-u** 刪除整行，使用 **alt-b** 和 **alt-f** 以單詞爲單位移動光標，使用 **ctrl-a** 將光標移至行首，使用 **ctrl-e** 將光標移至行尾，使用 **ctrl-k** 刪除光標至行尾的所有內容，使用 **ctrl-l** 清屏。鍵入 `man readline` 查看 Bash 中的默認快捷鍵，內容很多。例如 **alt-.** 循環地移向前一個參數，以及 **alt-*** 展開通配符。

- 你喜歡的話，可以鍵入 `set -o vi` 來使用 vi 風格的快捷鍵，而 `set -o emacs` 可以把它改回來。

- 爲了方便地鍵入長命令，在設置你的編輯器後（例如 `export EDITOR=vim`），鍵入 **ctrl-x** **ctrl-e** 會打開一個編輯器來編輯當前命令。在 vi 模式下則鍵入 **escape-v** 實現相同的功能。

- 鍵入 `history` 查看命令行歷史記錄。其中有許多縮寫，例如 `!$`（最後鍵入的參數）和 `!!`（最後鍵入的命令），儘管通常被 **ctrl-r** 和 **alt-.** 取代。

- 回到上一個工作路徑：`cd -`

- 如果你輸入命令的時候改變了主意，按下 **alt-#** 來在行首添加 `#`，或者依次按下 **ctrl-a**， **#**， **enter**。這樣做的話，之後你可以很方便的利用命令行歷史回到你剛纔輸入到一半的命令。

- 使用 `xargs` （ 或 `parallel`）。他們非常給力。注意到你可以控制每行參數個數（`-L`）和最大並行數（`-P`）。如果你不確定它們是否會按你想的那樣工作，先使用 `xargs echo` 查看一下。此外，使用 `-I{}` 會很方便。例如：
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` 有助於展示進程樹。

- 使用 `pgrep` 和 `pkill` 根據名字查找進程或發送信號（`-f` 參數通常有用）。

- 瞭解你可以發往進程的信號的種類。比如，使用 `kill -STOP [pid]` 停止一個進程。使用 `man 7 signal` 查看詳細列表。

- 使用 `nohup` 或 `disown` 使一個後臺進程持續運行。

- 使用 `netstat -lntp` 或 `ss -plat` 檢查哪些進程在監聽端口（默認是檢查 TCP 端口; 使用參數 `-u` 檢查 UDP 端口）。

- 有關打開套接字和文件，請參閱 `lsof`。

- 使用 `uptime` 或 `w` 來查看系統已經運行多長時間。

- 使用 `alias` 來創建常用命令的快捷形式。例如：`alias ll='ls -latr'` 使你可以方便地執行`ls -latr`命令。

- 在 Bash 腳本中，使用 `set -x` 去調試輸出，儘可能的使用嚴格模式，使用 `set -e` 令腳本在發生錯誤時退出而不是繼續運行，使用 `set -u` 來檢查是否使用了未賦值的變量，使用 `set -o pipefail` 嚴謹地對待錯誤（儘管問題可能很微妙）。當牽扯到很多腳本時，使用 `trap`。一個好的習慣是在腳本文件開頭這樣寫，這會使它檢測一些錯誤，並在錯誤發生時中斷程序並輸出信息：
```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- 在 Bash 腳本中，子 shell（使用括號 `(...)`）是一種組織參數的便捷方式。一個常見的例子是臨時地移動工作路徑，代碼如下：
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- 在 Bash 中，要注意其中有許多形式的擴展。檢查變量是否存在：`${name:?error message}`。例如，當 Bash 腳本需要一個參數時，可以使用這樣的代碼 `input_file=${1:?usage: $0 input_file}`。數學表達式：`i=$(( (i + 1) % 5 ))`。序列：`{1..10}`。截斷字符串：`${var%suffix}` 和 `${var#prefix}`。例如，假設 `var=foo.pdf`，那麼 `echo ${var%.pdf}.txt` 將輸出 `foo.txt`。

- 使用括號擴展（`{`...`}`）來減少輸入相似文本，並自動化文本組合。這在某些情況下會很有用，例如 `mv foo.{txt,pdf} some-dir`（同時移動兩個文件），`cp somefile{,.bak}`（會被擴展成 `cp somefile somefile.bak`）或者 `mkdir -p test-{a,b,c}/subtest-{1,2,3}`（會被擴展成所有可能的組合，並創建一個目錄樹）。

- 通過使用 `<(some command)` 可以將輸出視爲文件。例如，對比本地文件 `/etc/hosts` 和一個遠程文件：
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- 瞭解 Bash 中的“here documents”，例如 `cat <<EOF ...`。

- 在 Bash 中，同時重定向標準輸出和標準錯誤，`some-command >logfile 2>&1`。通常，爲了保證命令不會在標準輸入裏殘留一個打開了的文件句柄導致你當前所在的終端無法操作，添加 `</dev/null` 是一個好習慣。

- 使用 `man ascii` 查看具有十六進制和十進制值的ASCII表。`man unicode`，`man utf-8`，以及 `man latin1` 有助於你去瞭解通用的編碼信息。

- 使用 `screen` 或 [`tmux`](https://tmux.github.io/) 來使用多個屏幕，當你在使用 ssh 時（保存 session 信息）將尤爲有用。另一個輕量級的解決方案是 `dtach`。

- ssh 中，瞭解如何使用 `-L` 或 `-D`（偶爾需要用 `-R`）去開啓隧道是非常有用的，例如當你需要從一臺遠程服務器上訪問 web。

- 對 ssh 設置做一些小優化可能是很有用的，例如這個 `~/.ssh/config` 文件包含了防止特定環境下斷開連接、壓縮數據、多通道等選項：
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- 部分其他的關於 ssh 的選項是安全敏感且應當小心啓用的。例如在可信任的網絡中：`StrictHostKeyChecking=no`，`ForwardAgent=yes`

- 考慮使用 [`mosh`](https://mosh.mit.edu/) 作爲 ssh 的替代品，它使用 UDP 協議。

- 獲取文件的八進制格式權限，使用類似如下的代碼：
```sh
      stat -c '%A %a %n' /etc/timezone
```

- 使用 [`percol`](https://github.com/mooz/percol) 或者 [`fzf`](https://github.com/junegunn/fzf) 可以交互式地從另一個命令輸出中選取值。

- 使用 `fpp`（[PathPicker](https://github.com/facebook/PathPicker)）可以與基於另一個命令(例如 `git`）輸出的文件交互。

- 將 web 服務器上當前目錄下所有的文件（以及子目錄）暴露給你所處網絡的所有用戶，使用：
`python -m SimpleHTTPServer 7777` （使用端口 7777 和 Python 2）或`python -m http.server 7777` （使用端口 7777 和 Python 3）。

- 以某種權限執行命令，使用`sudo`（root 權限）或`sudo -u`（其他用戶）。使用`su`或者`sudo bash`來啓動一個以對應用戶權限運行的 shell。使用`su -`模擬其他用戶的登錄。

## 文件及數據處理

- 在當前路徑下通過文件名定位一個文件，`find . -iname '*something*'`（或類似的）。在所有路徑下通過文件名查找文件，使用 `locate something` （但請記住 `updatedb` 可能沒有對最近新建的文件建立索引）。

- 使用 [`ag`](https://github.com/ggreer/the_silver_searcher) 在源代碼或數據文件裏檢索（比 `grep -r` 更好）。

- 將 HTML 轉爲文本：`lynx -dump -stdin`

- Markdown，HTML，以及所有文檔格式之間的轉換，試試 [`pandoc`](http://pandoc.org/)。

- 如果你不得不處理 XML，`xmlstarlet` 寶刀未老。

- 使用 [`jq`](http://stedolan.github.io/jq/) 處理 JSON。

- 使用 [`shyaml`](https://github.com/0k/shyaml) 處理 YAML。

- Excel 或 CSV 文件的處理，[csvkit](https://github.com/onyxfish/csvkit) 提供了 `in2csv`，`csvcut`，`csvjoin`，`csvgrep` 等工具。

- 關於 Amazon S3，[`s3cmd`](https://github.com/s3tools/s3cmd) 很方便而 [`s4cmd`](https://github.com/bloomreach/s4cmd) 更快。Amazon 官方的 [`aws`](https://github.com/aws/aws-cli) 以及  [`saws`](https://github.com/donnemartin/saws) 是其他 AWS 相關工作的基礎。

- 瞭解如何使用 `sort` 和 `uniq`，包括 uniq 的 `-u` 參數和 `-d` 參數，詳見後文單行腳本節。另外可以瞭解一下 `comm`。

- 瞭解如何使用 `cut`，`paste` 和 `join` 來更改文件。很多人都會使用 `cut`，但幾乎都不會使用 `join`。

- 瞭解如何運用 `wc` 去計算新行數（`-l`），字符數（`-m`），單詞數（`-w`）以及字節數（`-c`）。

- 瞭解如何使用 `tee` 將標準輸入複製到文件甚至標準輸出，例如 `ls -al | tee file.txt`。

- 瞭解語言環境對許多命令行工具的微妙影響，包括排序的順序和性能。大多數 Linux 的安裝過程會將 `LANG` 或其他有關的變量設置爲符合本地的設置。意識到當你改變語言環境時，排序的結果可能會改變。明白國際化可能會使 sort 或其他命令運行效率下降*許多倍*。某些情況下（例如集合運算）你可以放心的使用 `export LC_ALL=C` 來忽略掉國際化並使用基於字節的順序。

- 瞭解 `awk` 和 `sed` 關於數據的簡單處理的用法。例如，將文本文件中第三列的所有數字求和：`awk '{ x += $3 } END { print x }'`. 這可能比同等作用的 Python 代碼快三倍且代碼量少三倍。

- 替換一個或多個文件中出現的字符串：
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- 使用 [`repren`](https://github.com/jlevy/repren) 來批量重命名，或是在多個文件中搜索替換。（有些時候 `rename` 命令也可以批量重命名，但要注意，它在不同 Linux 發行版中的功能並不完全一樣。）
```sh
      # Full rename of filenames, directories, and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # Recover backup files whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Same as above, using rename, if available:
      rename 's/\.bak$//' *.bak
```

- 根據 man 頁面的描述，`rsync` 真的是一個快速且非常靈活的文件複製工具。它通常被用於機器間的同步，但在本地也同樣有用。它同時也是刪除大量文件的[最快方法](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html)之一：
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- 使用 `shuf` 從一個文件中隨機選取多行。

- 瞭解 `sort` 的參數。處理數字方面，使用 `-n` 或者 `-h` 來處理可讀性數字（例如 `du -h` 的輸出）。明白鍵的工作原理（`-t` 和 `-k`）。例如，注意到你需要 `-k1，1` 來僅按第一個域來排序，而 `-k1` 意味着按整行排序。穩定排序（`sort -s`）在某些情況下很有用。例如，以第二個域爲主關鍵字，第一個域爲次關鍵字進行排序，你可以使用 `sort -k1，1 | sort -s -k2，2`。

- 如果你想在 Bash 命令行中寫 tab 製表符，按下 **ctrl-v** **[Tab]** 或鍵入 `$'\t'` （後者可能更好，因爲你可以複製粘貼它）。

- 標準的源代碼對比及合併工具是 `diff` 和 `patch`。使用 `diffstat` 查看變更總覽數據。注意到 `diff -r` 對整個文件夾有效。使用 `diff -r tree1 tree2 | diffstat` 查看變更總覽數據。

- 對於二進制文件，使用 `hd` 使其以十六進制顯示以及使用 `bvi` 來編輯二進制。

- 同樣對於二進制文件，`strings`（包括 `grep` 等等）允許你查找一些文本。

- 二進制文件對比（Delta 壓縮），使用 `xdelta3`。

- 使用 `iconv` 更改文本編碼。而更高級的用法，可以使用 `uconv`，它支持一些高級的 Unicode 功能。例如，這條命令將所有元音字母轉爲小寫並移除了：
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- 拆分文件，查看 `split`（按大小拆分）和 `csplit`（按模式拆分）。

- 用 [`dateutils`](http://www.fresse.org/dateutils/) 中的 `dateadd`, `datediff`, `strptime` 等工具操作日期和時間表達式。

- 使用 `zless`，`zmore`，`zcat` 和 `zgrep` 對壓縮過的文件進行操作。


## 系統調試

- `curl` 和 `curl -I` 可以便捷地被應用於 web 調試中，它們的好兄弟 `wget` 也可以，或者是更潮的 [`httpie`](https://github.com/jakubroztocil/httpie)。

- 使用 `iostat`、`netstat`、`top` （`htop` 更佳）和 `dstat` 去獲取硬盤、cpu 和網絡的狀態。熟練掌握這些工具可以使你快速的對系統的當前狀態有一個大概的認識。

- 使用 `netstat` 和 `ss` 查看網絡連接的細節。

- 若要對系統有一個深度的總體認識，使用 [`glances`](https://github.com/nicolargo/glances)。它在一個終端窗口中向你提供一些系統級的數據。這對於快速的檢查各個子系統非常有幫助。

- 若要瞭解內存狀態，運行並理解 `free` 和 `vmstat` 的輸出。尤其注意“cached”的值，它指的是 Linux 內核用來作爲文件緩存的內存大小，因此它與空閒內存無關。

- Java 系統調試則是一件截然不同的事，一個可以用於 Oracle 的 JVM 或其他 JVM 上的調試的技巧是你可以運行 `kill -3 <pid>` 同時一個完整的棧軌跡和堆概述（包括 GC 的細節）會被保存到標準輸出/日志文件。JDK 中的 `jps`，`jstat`，`jstack`，`jmap` 很有用。[SJK tools](https://github.com/aragozin/jvm-tools) 更高級.

- 使用 `mtr` 去跟蹤路由，用於確定網絡問題。

- 用 `ncdu` 來查看磁盤使用情況，它比常用的命令，如 `du -sh *`，更節省時間。

- 查找正在使用帶寬的套接字連接或進程，使用 `iftop` 或 `nethogs`。

- `ab` 工具（捆綁於 Apache）可以簡單粗暴地檢查 web 服務器的性能。對於更複雜的負載測試，使用 `siege`。

- `wireshark`，`tshark` 和 `ngrep` 可用於複雜的網絡調試。

- 瞭解 `strace` 和 `ltrace`。這倆工具在你的程序運行失敗、掛起甚至崩潰，而你卻不知道爲什麼或你想對性能有個總體的認識的時候是非常有用的。注意 profile 參數（`-c`）和附加到一個運行的進程參數 （`-p`）。

- 瞭解使用 `ldd` 來檢查共享庫。

- 瞭解如何運用 `gdb` 連接到一個運行着的進程並獲取它的堆棧軌跡。

- 學會使用 `/proc`。它在調試正在出現的問題的時候有時會效果驚人。比如：`/proc/cpuinfo`，`/proc/meminfo`，`/proc/cmdline`，`/proc/xxx/cwd`，`/proc/xxx/exe`，`/proc/xxx/fd/`，`/proc/xxx/smaps`（這裏的 `xxx` 表示進程的 id 或 pid）。

- 當調試一些之前出現的問題的時候，`sar` 非常有用。它展示了 cpu、內存以及網絡等的歷史數據。

- 關於更深層次的系統分析以及性能分析，看看 `stap`（[SystemTap](https://sourceware.org/systemtap/wiki)），[`perf`](http://en.wikipedia.org/wiki/Perf_(Linux))，以及[`sysdig`](https://github.com/draios/sysdig)。

- 查看你當前使用的系統，使用 `uname` ， `uname -a` （Unix／kernel 信息） 或者 `lsb_release -a` （Linux 發行版信息）。

- 無論什麼東西工作得很歡樂時試試 `dmesg`（可能是硬件或驅動問題）。


## 單行腳本

一些命令組合的例子：

- 當你需要對文本文件做集合交、並、差運算時，結合使用 `sort`/`uniq` 很有幫助。假設 `a` 與 `b` 是兩內容不同的文件。這種方式效率很高，並且在小文件和上G的文件上都能運用 （`sort` 不被內存大小約束，儘管在 `/tmp` 在一個小的根分區上時你可能需要 `-T` 參數），參閱前文中關於 `LC_ALL` 和 `sort` 的 `-u` 參數的部分。
```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```

- 使用 `grep . *`（每行都會附上文件名）或者 `head -100 *`（每個文件有一個標題）來閱讀檢查目錄下所有文件的內容。這在檢查一個充滿配置文件的目錄（如 `/sys`、`/proc`、`/etc`）時特別好用。

- 計算文本文件第三列中所有數的和（可能比同等作用的 Python 代碼快三倍且代碼量少三倍）：
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- 如果你想在文件樹上查看大小/日期，這可能看起來像遞歸版的 `ls -l` 但比 `ls -lR` 更易於理解：
```sh
      find . -type f -ls
```

- 假設你有一個類似於 web 服務器日志文件的文本文件，並且一個確定的值只會出現在某些行上，假設一個 `acct_id` 參數在URI中。如果你想計算出每個 `acct_id` 值有多少次請求，使用如下代碼：
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- 運行這個函數從這篇文檔中隨機獲取一條技巧（解析 Markdown 文件並抽取項目）：
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```


## 冷門但有用

- `expr`：計算表達式或正則匹配

- `m4`：簡單地宏處理器

- `yes`：多次打印字符串

- `cal`：漂亮的日曆

- `env`：執行一個命令（腳本文件中很有用）

- `printenv`：打印環境變量（調試時或在使用腳本文件時很有用）

- `look`：查找以特定字符串開頭的單詞

- `cut`、`paste` 和 `join`：數據修改

- `fmt`：格式化文本段落

- `pr`：將文本格式化成頁/列形式

- `fold`：包裹文本中的幾行

- `column`：將文本格式化成多列或表格

- `expand` 和 `unexpand`：製表符與空格之間轉換

- `nl`：添加行號

- `seq`：打印數字

- `bc`：計算器

- `factor`：分解因數

- [`gpg`](https://gnupg.org/)：加密並簽名文件

- `toe`：terminfo entries 列表

- `nc`：網絡調試及數據傳輸

- `socat`：套接字代理，與 `netcat` 類似

- [`slurm`](https://github.com/mattthias/slurm)：網絡可視化

- `dd`：文件或設備間傳輸數據

- `file`：確定文件類型

- `tree`：以樹的形式顯示路徑和文件，類似於遞歸的 `ls`

- `stat`：文件信息

- `time`：執行命令，並計算執行時間

- `lockfile`：使文件只能通過 `rm -f` 移除

- `logrotate`: 切換、壓縮以及發送日志文件

- `watch`：重複運行同一個命令，展示結果並高亮有更改的部分

- `tac`：反向輸出文件

- `shuf`：文件中隨機選取幾行

- `comm`：一行一行的比較排序過的文件

- `pv`：監視通過管道的數據

- `hd`，`hexdump`，`xxd`，`biew` 和 `bvi`：保存或編輯二進制文件

- `strings`：從二進制文件中抽取文本

- `tr`：轉換字母

- `iconv` 或 `uconv`：簡易的文件編碼

- `split` 和 `csplit`：分割文件

- `sponge`：在寫入前讀取所有輸入，在讀取文件後再向同一文件寫入時比較有用，例如 `grep -v something some-file | sponge some-file`

- `units`：將一種計量單位轉換爲另一種等效的計量單位（參閱 `/usr/share/units/definitions.units`）

- `apg`：隨機生成密碼

- `7z`：高比例的文件壓縮

- `ldd`：動態庫信息

- `nm`：提取 obj 文件中的符號

- `ab`：性能分析 web 服務器

- `strace`：系統調用調試

- `mtr`：更好的網絡調試跟蹤工具

- `cssh`：可視化的併發 shell

- `rsync`：通過 ssh 或本地文件系統同步文件和文件夾

- `wireshark` 和 `tshark`：抓包和網絡調試工具

- `ngrep`：網絡層的 grep

- `host` 和 `dig`：DNS 查找

- `lsof`：列出當前系統打開文件的工具以及查看端口信息

- `dstat`：系統狀態查看

- [`glances`](https://github.com/nicolargo/glances)：高層次的多子系統總覽

- `iostat`：硬盤使用狀態

- `mpstat`: CPU 使用狀態

- `vmstat`: 內存使用狀態

- `htop`：top 的加強版

- `last`：登入記錄

- `w`：查看處於登錄狀態的用戶

- `id`：用戶/組 ID 信息

- `sar`：系統歷史數據

- `iftop` 或 `nethogs`：套接字及進程的網絡利用

- `ss`：套接字數據

- `dmesg`：引導及系統錯誤信息

- `sysctl`: 在內核運行時動態地查看和修改內核的運行參數

- `hdparm`：SATA/ATA 磁盤更改及性能分析

- `lsb_release`：Linux 發行版信息

- `lsblk`：列出塊設備信息：以樹形展示你的磁盤以及磁盤分區信息

- `lshw`，`lscpu`，`lspci`，`lsusb` 和 `dmidecode`：查看硬件信息，包括 CPU、BIOS、RAID、顯卡、USB設備等

- `lsmod` 和 `modinfo`：列出內核模塊，並顯示其細節

- `fortune`，`ddate` 和 `sl`：額，這主要取決於你是否認爲蒸汽火車和莫名其妙的名人名言是否“有用”

## 僅限 MacOS X 系統

以下是*僅限於* MacOS 系統的技巧

- 用 `brew` （Homebrew）或者 `port` （MacPorts）進行包管理。這些可以用來在 Mac 系統上安裝以上的大多數命令。

- 用 `pbcopy` 複製任何命令的輸出到桌面應用，用 `pbpaste` 粘貼輸入。

- 若要在 Mac OS 終端中將 Option 鍵視爲 alt 鍵（例如在上面介紹的 **alt-b**, **alt-f** 等命令中用到），打開 偏好設置 -> 描述文件 -> 鍵盤 並勾選“使用 Option 鍵作爲 Meta 鍵”。

- 用 `open` 或者 `open -a /Applications/Whatever.app` 使用桌面應用打開文件。

- Spotlight： 用 `mdfind` 搜索文件，用 `mdls` 列出元數據（例如照片的 EXIF 信息）。

- 注意 MacOS 系統是基於 BSD UNIX 的，許多命令（例如 `ps`，`ls`，`tail`，`awk`，`sed`）都和 Linux 中有些微的不同，這些極大的被 System V-style Unix 和 GNU 工具影響。你可以通過標題爲 "BSD General Commands Manual" 的 man 頁面發現這些不同。在有些情況下 GNU 版本的命令也可能被安裝（例如 `gawk` 和 `gsed` 對應 GNU 中的 awk 和 sed ）。如果要寫跨平臺的 Bash 腳本，避免使用這些命令（例如，考慮 Python 或者 `perl` ）或者經過仔細的測試。

- 用 `sw_vers` 獲取 MacOS 的版本信息。


## 更多資源

- [awesome-shell](https://github.com/alebcay/awesome-shell)：一份精心組織的命令行工具及資源的列表。
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line)：一份針對 Mac OS 命令行的更深入的指南。
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/)：爲了編寫更好的腳本文件。
- [shellcheck](https://github.com/koalaman/shellcheck)：一個靜態 shell 腳本分析工具，本質上是 bash／sh／zsh 的 lint。
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html)：有關如何在 shell 腳本里正確處理文件名的細枝末節。


## 免責聲明

除去特別微小的任務，編寫代碼是出於方便閱讀的目的。能力往往伴隨着責任。你 *可以* 在 Bash 中做一些事並不意味着你應該去做！;)


## 授權條款

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

本文使用授權協議 [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/)。
