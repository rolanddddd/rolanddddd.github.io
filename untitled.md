# SVN大全

### 1. 常用操作

1. 第一次下载文件夹

   ```text
   svn checkout svn://192.168.1.1/xxx/y`
   ```

2. 添加文件

   ```text
   svn add test.f
   ```

3. 提交改动

   ```text
   svn commit -m [-N][--no-unlock] "logmessage" test.f
   ```

4. 加锁

   ```text
   svn lock -m "logmessage" [--force] test.f
   svn unlock test.f
   ```

5. 更新到某版本

   ```text
   svnup -r 2819 test.f
   svnup (update to lates)
   ```

6. 查看状态

   ```text
   svn st
   ```

* A新增；C冲突；D删除；G合并；U更新；E存在；R替换

1. 删除文件
2. 删除/复制文件夹务必要删除**.svn**文件

   ```text
   svn delete test.f -m "deletlog" test.f
   或者svn delete test.f / svnci -m "deletlog" test.f
   ```

3. 查看日志

   ```text
   svn log test.f
   查看最新5次更新log svn log -l 5
   ```

4. 查看文件详细信息

   ```text
   svn info test.f
   ```

5. 比较差异

   ```text
   本地与SVN对比  svn diff test.f
   不同版本对比   svn diff -r 4819:4817 test.f
   ```

6. 帮助

   ```text
   svn help
   svn help ci
   ```

### 2. 非常用操作

1. 显示所有属于版本库的文件和目录

   ```text
   svn ls
   ```

2. 创建纳入版本库的新目录

   ```text
   svn mkdir xxx
   ```

3. 未提交文件恢复本地修改到svn版本 -&gt;&gt; 很有用

   ```text
   svn revert
   ```

4. 解决冲突，移除冲突状态文件

   ```text
   svn resolved
   ```

### 3. 创建分支

```text
创建分支 svn cp/copy svn://127.0.0.1/project_1/trunk svn://127.0.0.1/branch/project_1_sub -m "branchlog"
删除分支 svn delete/rm/remove svn://127.0.0.1/branch/project_1_sub -m "branchlog"
分支合并（r11到当前版本） svn merge -r 11:HEAD svn://127.0.0.1/project_1_sub -m "mergelog"
```

