# 工作站验证平台使用

### 1. UT/IT

* rules file： `/02verification_data/dv/cnn25/tests/`
* cfg file：`/02verification_data/flow/SIM/configs/`
* txt file: `/home/xdata1/projects/tp1609/cnn25/`

#### 1. 环境设置

```text
setwa;
source sourceme;
source ./setup/setup.cshrc;
```

#### 2. 编译cmodel

```text
cd 02verification_data/cmdel/caffe-generator;
    make clean;
    make -j32;
    make py;
cd ../CaffeSimulator;
    make clean;
    make -j32;
    make py;
cd ../fxptxt_gen;
    make clean;
    make -j32;
```

#### 3. 运行命令

1）单条case: `xrun cnn25:eltwise4k.eltwise_instr_001_01 -- +dump` 

2）多条case: `xregression -cfg eltwise_200_1grp.rules -max=10 -- +dump` 

3）software\_ut: `xregression -cfg -flow software[_4k] -max=10` 

4）只编译一次

提前在tests中添加build `spawn.py eltwise4k build/build_4k`;删除build使用`spawn.py eltwise4k -no`

```text
xrun cnn25:build [-flow aisc_4k]
xrun cnn25:eltwise4k.eltwise_instr_001_01 -flow cluster/cluster_4k
xregression -cfg eltwise_200_1grp -flow cluster/cluster_4k -max=10
```

* software\_ut如遇到以下错误则为pass

  `Fatal Error: Cycle limit 1000 reached!`

#### 4. 命令参数

* `-flow asic_4k` 执行4k用例
* `-recomp` 重新执行xrun不用重新打开verdi
* `-seed=xxxx` 种子
* `-max=xx`同时提交最多用例

### 2. 覆盖率收集

* 运行覆盖率收集之前更新所有代码，避免版本不同导致无法merge
* 如果俩次运行之间有RTL代码或验证平台变动，需要删除cov.vdb中所有数据

  ```text
  xrun cnn25:build -flow coverage[_4k]
    xrun cnn25:first.smoke_net -flow cov_cluster[_4k]
    xregression -cfg xx.cfg -flow cov_cluster[_4k] -max=10
  ```

### 3. 其他

1. 如果回归测试没有产生report则用以下脚本导出

   ```text
   find . -name "simv.log" | xargs grep -e "^\s*cnn2" > tmp.log
   sort tmp.log > collect.log
   ```

2. 查找ERROR或PASS case

   ```text
   grep "ERROR" layer*/simv.log | grep -v "Cycle limit" | wc
   ```

