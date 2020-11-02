### PLSQL Developer 12 (64 bit)的环境配置
1. 安装oracle:ORA+11+G+R2+server+64bit+for+windows.iso包

2. 安装plsql dev:plsqldev1205x64.msi

3. 安装oracle 远程访问工具：instantclient-basic-windows.x64-19.6.0.0.0dbru.zip

4. 添加文件以及文件路径到访问工具：`..\instantclient_19_6\network\admin\tnsnames.ora`

5. 配置tnsnames.ora文件，以下代码的4个配置点：
  ```
      myConnectionName[自定义本地连接名] =
      (DESCRIPTION =
          (ADDRESS_LIST =
            (ADDRESS = (PROTOCOL = TCP)(HOST = 192.168.6.11[远程oracle ip地址] )(PORT = 1521[端口号]))
          )
          (CONNECT_DATA =
            (SERVICE_NAME = ORCL[远程访问服务名] )
          )
      )
  ```

6. 配置环境变量
  + TNS_ADMIN：`..\instantclient_19_6\network\admin` (远程访问工具目录下)
  + NLS_LANG：`SIMPLIFIED CHINESE_CHINA.ZHS16GBK`

7. 在PLSQL中配置connection：![image-20200413133814775](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200413133814775.png)