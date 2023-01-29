### cac_obs_cli工具开发使用

#### 脚本编写

[代码仓](https://codehub-g.huawei.com/cloudscope-sre/obs-cmc/obs-cac-plugin/merge_requests)

#### 推包

[流水线**OBS_L2_CAC_Script_Test**](https://fuxi.huawei.com/mine/components/10057745/pipeline/list/279959), 实验室环境。

![2023-01-04_154918](D:\Leslie\MMark\images\cac_obs_cli工具使用.assets\2023-01-04_154918.png)

任务名称修改成`cac_obs_cli_for_dataPlus`

[参考资料](https://clouddevops.huawei.com/domains/28589/wiki/2609/WIKI2022071300111)

#### 验证

**平台验证**

[实验室环境脚本执行平台](https://gd.cloudops-w3.inhuawei.com/CloudAutoChange-cf2/#/cac/jobPlatform/executeScript/131994)

![image-20230104154926267](D:\Leslie\MMark\images\cac_obs_cli工具使用.assets\image-20230104154926267.png)

* 参数解释
  * **1** **user**                  # oam登录用户
  * **2** **password**        #oam用户密码， 密码需要base64编码
  
  ```shell
  #oam节点上执行 实验室oam节点：8.40.226.224 
  echo Dfvgo@678! | base64 # 编码password # RGZ2Z29ANjc4IQo=
  python /home/oam/base64decode.py RGZ2Z29ANjc4IQo= # 验证编码是否成功
  ```
  
  * **3** **service**            # 默认
  * **4** **change**            # 执行操作
  * **5** **key**                   # 配置文件名，例如`fw-forward-rule-config`
  * **6** **value**               # 配置项名字，例如`ddmc-user-new-2022-policy`

**本地验证**

登录oam平台之后执行

1. 修改脚本`/home/oam/cac_obs_cli_for_dataPlus.py`为你变编写的脚本
2. 执行脚本

```shell
python /home/oam/cac_obs_cli_for_dataPlus.py "admin" "RGZ2Z29ANjc4IQo=" "service" "change" "fw-forward-rule-config" "ddmc-user-new-2022-policy"
python /home/oam/cac_obs_cli_for_dataPlus.py "admin" "RGZ2Z29ANjc4IQo=" "service" "show" "signedSubResourceList"
```
