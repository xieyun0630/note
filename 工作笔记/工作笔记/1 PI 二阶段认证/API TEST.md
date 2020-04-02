# 二阶段认证的测试URL

### auth AIP的测试数据

测试之前创建如下SQL

```SQL
#查询
SELECT * FROM F_TWO_STEP_AUTH_CODE
#插入
insert into F_TWO_STEP_AUTH_CODE (MEMBER_NO, USE_SERVICE_NO, CALL_IDENTIFIER, AUTH_CODE, VALID_DT)
values (219, 1000, 'com', '2353233', to_date('19-09-2019 15:16:04', 'dd-mm-yyyy hh24:mi:ss'));

delete from F_TWO_STEP_AUTH_CODE
where MEMBER_NO=219

SELECT
    MEMBER_NO,
    USE_SERVICE_NO,
    CALL_IDENTIFIER,
    AUTH_CODE,
    VALID_DT
FROM
    F_TWO_STEP_AUTH_CODE
WHERE
    MEMBER_NO = 219
    AND USE_SERVICE_NO = 1000
    AND CALL_IDENTIFIER = 'com'

```



https://localhost:8443/a/api/v1/twostep/auth.do?apiKey=b2b22d1e736ef3bdaf29f7fc2594a828ae203797&memberId=ELGR2409&useServiceNo=1000&callIdentifier=com&authCode=2353233&ipAddress=192.168.1.1

### createAuthCode AIP的测试URL

https://localhost:8443/a/api/v1/twostep/createAuthCode.do?apiKey=11sdfsadfasdfsadfsdfa&memberID=11&useServiceNo=11&callIdentifier=11&codeLength=11&codeType=2&mlTemplateNo=333&validDt=444&ipAddress=555

### register api的测试数据

#### url:

https://localhost:8443/a/api/v1/twostep/register.do?apiKey=b2b22d1e736ef3bdaf29f7fc2594a828ae203797&memberId=ELGR2461&useServiceNo=1000&callIdentifier=com



以上URL测试结果会向数据表中添加一条以下数据

```sql
insert into M_TWO_STEP_AUTH_CONFIG (MEMBER_NO, USE_SERVICE_NO, CALL_IDENTIFIER)
values (221, 1000, 'com');

#查询 利用M两阶段认证设定  M_TWO_STEP_AUTH_CONFIG M二段階認証利用設定
SELECT * FROM M_TWO_STEP_AUTH_CONFIG where USE_SERVICE_NO =1000
```



### unregister api的测试数据

https://localhost:8443/a/api/v1/twostep/unRegister.do?apiKey=b2b22d1e736ef3bdaf29f7fc2594a828ae203797&memberId=ELGR2461&useServiceNo=1000&callIdentifier=com

### Usechk api

https://localhost:8443/a/api/v1/twostep/usechk.do?apiKey=b2b22d1e736ef3bdaf29f7fc2594a828ae203797&memberId=ELGR2461&useServiceNo=1000&callIdentifier=com