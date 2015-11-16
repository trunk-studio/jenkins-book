Q & A
=====

VM 問題排解
-----------

上課時使用 VM Bridged Adapter network setting 但後來連不到，為了讓課程上的更順利，先改成 NAT 但如此 Host 就沒有辦法連到 Guest VM ，本來要用 Windows Cmder 進行相關操作，只好讓學員用 ubuntu 內的 terminal 進行操作。

後來查了一下資料，用 NAT 要連進 Guest VM 其實很簡單，只要設置一下 Port Forwarding 即可，如下：

![](images/NAT.png)

![](images/forward.png)

給需要的人參考。

關於分支使用的策略
------------------

下面連結可以參考：

[COSCUP 開源工作坊: Git Workflows](https://github.com/hacking-thursday/coscup2015_workshop)

有更詳細的介紹。

希望 N 個 task 完成後才進行目標 task
------------------------------------

套件如下：

[Join Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Join+Plugin)

environment 替換
----------------

套件如下：

[EnvInject Plugin](https://wiki.jenkins-ci.org/display/JENKINS/EnvInject+Plugin)
