# C++ 大作业

学号：18062019

姓名：蒋杨龙

GitHub作业库地址：<https://github.com/TTTTerry/cpp_homework> 

大作业报告文件名为：Cpp_BP.md 

修改文件路径：src/common/time/test/WallClockTest.cpp

---

## 实验过程

### 安装 Nebula Graph

按照[Nebula Graph 手册](https://github.com/vesoft-inc/nebula/tree/master/docs/manual-CN )中[视频](https://space.bilibili.com/472621355 )的步骤,[通过编译源码](https://www.bilibili.com/video/av78217553 )安装 Nebula Graph。

### 尝试更改并上传文件（Git）

1. 更改现有分支

   ```
   jjjerry@jjjerry-virtual-machine:~/nebula$ git remote -v
   origin	git@github.com:Ricardo-MJ/nebula.git (fetch)
   origin	git@github.com:Ricardo-MJ/nebula.git (push)
   
   jjjerry@jjjerry-virtual-machine:~/nebula$ git remote rm origin
   error: could not lock config file .git/config: 权限不够
   fatal: 不能取消设置 'branch.master.remote'
   
   jjjerry@jjjerry-virtual-machine:~/nebula$ sudo git remote rm origin
   [sudo] jjjerry 的密码： 
   
   jjjerry@jjjerry-virtual-machine:~/nebula$ git remote add origin https://github.com/TTTTerry/nebula.git
   error: could not lock config file .git/config: 权限不够
   fatal: 不能设置 'remote.origin.url' 为 'https://github.com/TTTTerry/nebula.git'
   
   jjjerry@jjjerry-virtual-machine:~/nebula$ sudo git remote add origin https://github.com/TTTTerry/nebula.git
   
   jjjerry@jjjerry-virtual-machine:~/nebula$ git remote -v
   origin	https://github.com/TTTTerry/nebula.git (fetch)
   origin	https://github.com/TTTTerry/nebula.git (push)
   ```

   > 过程还算顺利，就是总是忘记 `sudo` 

2. 改动一个文件

   ```
   jjjerry@jjjerry-virtual-machine:~/nebula$ git status
   位于分支 master
   尚未暂存以备提交的变更：
     （使用 "git add <文件>..." 更新要提交的内容）
     （使用 "git checkout -- <文件>..." 丢弃工作区的改动）
   
   	修改：     src/common/time/test/WallClockTest.cpp
   
   修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
   ```

3. `root`

   ```
   jjjerry@jjjerry-virtual-machine:~/nebula$ sudo su
   [sudo] jjjerry 的密码： 
   ```

4. 创建自己的分支

   ```
   root@jjjerry-virtual-machine:/home/jjjerry/nebula# git branch Try
   
   root@jjjerry-virtual-machine:/home/jjjerry/nebula# git checkout Try
   M	src/common/time/test/WallClockTest.cpp
   切换到分支 'Try'
   ```

5. 添加说明

   ```
   root@jjjerry-virtual-machine:/home/jjjerry/nebula# git add src/common/time/test/WallClockTest.cpp 
   
   root@jjjerry-virtual-machine:/home/jjjerry/nebula# git commit -m "just a try"
   Performing C++ linters...
   [Try 9e02f0b] just a try
    1 file changed, 1 insertion(+), 1 deletion(-)
   ```

6. 上传代码

   ```
   root@jjjerry-virtual-machine:/home/jjjerry/nebula# git push --set-upstream origin Try
   Username for 'https://github.com': TTTTerry
   Password for 'https://TTTTerry@github.com': 
   对象计数中: 7, 完成.
   Delta compression using up to 8 threads.
   压缩对象中: 100% (7/7), 完成.
   写入对象中: 100% (7/7), 522 bytes | 11.00 KiB/s, 完成.
   Total 7 (delta 6), reused 0 (delta 0)
   remote: Resolving deltas: 100% (6/6), completed with 6 local objects.
   remote: 
   remote: Create a pull request for 'Try' on GitHub by visiting:
   remote:      https://github.com/TTTTerry/nebula/pull/new/Try
   remote: 
   To https://github.com/TTTTerry/nebula.git
    * [new branch]      Try -> Try
   分支 'Try' 设置为跟踪来自 'origin' 的远程分支 'Try'。
   ```

7. 完成

### 测试改动

1. 先 `make` 

2. 运行 `wallclock_test`

   ```
   jjjerry@jjjerry-virtual-machine:~/nebula/build/src/common/time/test/_build$ ./wallclock_test 
   [==========] Running 2 tests from 1 test case.
   [----------] Global test environment set-up.
   [----------] 2 tests from WallClock
   [ RUN      ] WallClock.TimePointInSeconds
   [       OK ] WallClock.TimePointInSeconds (0 ms)
   [ RUN      ] WallClock.TimePointInMilliSeconds
   [       OK ] WallClock.TimePointInMilliSeconds (0 ms)
   [----------] 2 tests from WallClock (0 ms total)
   
   [----------] Global test environment tear-down
   [==========] 2 tests from 1 test case ran. (0 ms total)
   [  PASSED  ] 2 tests.
   ```

3. 完成

## 总结

在这次实验中我了解并实际操作了 `git` 对 `git` 有了更为深入的了解，但是因为我没有完全明白 `nebula` 的工作原理，找到我可以完成的小问题，所以在这个实验里我并没有在真正意义上提交一个 `pr` ，这算是一个遗憾吧。

通过这次实验，我感受到了在 `GitHub` 中参与到一个开源的大项目的感觉。这次实验让我知道了如何参与到一个开源项目中，这对我未来的学习和工作有着很大的作用，让我学习到了不少，真是受益匪浅。