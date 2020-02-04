# 第 1.9 节 导入配置

### 1 坑

json容易写错,边配边校验吧.丢个链接[在线校验json格式](https://www.sojson.com/)

### 2 简述

菜单入口:表单组管理 > 更多操作 > 匹配导入配置

页面列名如下,需要配置的主要有三列

| 序号 | 字段名称 | 字段备注 | 模板列 | 匹配列 | 更新列 | 插入列 | 更新表达式 | 插入表达式 | 校验表达式 | 校验规则 |
| :--- | :------- | :------- | :----- | :----- | :----- | :----- | :--------- | :--------- | :--------- | :------- |
| -    | -        | -        | 需要   | -      | -      | 需要   |            |            | 需要       | -        |

### 3 常用校验表达式配置

- 客户性质

```json
[{"express": "cfbizBusinessinfo.CUSTOMER_TYPE != null && cfbizBusinessinfo.CUSTOMER_TYPE !=''","msg": "客户性质不能为空"}, {"express": "['GR','QY'].indexOf(cfbizBusinessinfo.CUSTOMER_TYPE)>=0","msg": "客户性质必须填写个人或企业"}]
```

- 证件号码

```json
[{ "express": "cfbizBusinessinfo.CREDENTIAL_NO !=null && cfbizBusinessinfo.CREDENTIAL_NO !=''", "msg": "身份证号/统一社会信用代码不能为空" }, { "express": "((cfbizBusinessinfo.CUSTOMER_TYPE=='QY')&&(/^[1-9A-GY]{1}[1239]{1}[1-5]{1}[0-9]{5}[0-9A-Z]{10}$|^[0-9]{15}$/.test(cfbizBusinessinfo.CREDENTIAL_NO)))||(cfbizBusinessinfo.CUSTOMER_TYPE=='GR')", "message": "客户性质为企业时应输入正确的统一社会信用代码" }, { "express": "((cfbizBusinessinfo.CUSTOMER_TYPE=='GR')&&(/^[1-9]\\d{5}(18|19|([23]\\d))\\d{2}((0[1-9])|(10|11|12))(([0-2][1-9])|10|20|30|31)\\d{3}[0-9Xx]$/.test(cfbizBusinessinfo.CREDENTIAL_NO)))||(cfbizBusinessinfo.CUSTOMER_TYPE=='QY')", "message": "客户性质为自然人时应输入正确的身份证号" }]
```

- 客户名称

```json
[{"express": "cfbizBusinessinfo.CUSTOMER_NAME !=null && cfbizBusinessinfo.CUSTOMER_NAME !=''","msg": "客户名称不能为空"}]
```

- 银行贷款金额

```json
[{"express": "cfbizBusinessinfo.BANK_LOAN_AMOUNT !=null && cfbizBusinessinfo.BANK_LOAN_AMOUNT !=''",   "msg": "银行贷款金额（万元）不能为空"  },{"express":"Number(cfbizBusinessinfo.BANK_LOAN_AMOUNT) >= 10 && Number(cfbizBusinessinfo.BANK_LOAN_AMOUNT) <= 1000","msg": "银行贷款金额（万元）必须大于或等于10万元且小于或等于1000万元"}]
```

​	他行担保金额(不校验)

```json
[{"express":"(cfbizBusinessinfo.OTHER_BANK_GUARANTEE_AMOUNT ==null || cfbizBusinessinfo.OTHER_BANK_GUARANTEE_AMOUNT =='') || (Number(cfbizBusinessinfo.OTHER_BANK_GUARANTEE_AMOUNT) >= 10 && Number(cfbizBusinessinfo.OTHER_BANK_GUARANTEE_AMOUNT) <= 1000)","msg": "银行贷款金额（万元）必须大于或等于10万元且小于或等于1000万元"}]
```



- 贷款期限

```json
[{"express": "cfbizBusinessinfo.LOAN_MONTH !=null && cfbizBusinessinfo.LOAN_MONTH !=''","msg": "贷款期限（月）不能为空"}, {"express": "/^[1-9]\\d*|0$/.test(cfbizBusinessinfo.LOAN_MONTH)","msg": "贷款期限（月）必须为非负整数"}, {"express": "Number(cfbizBusinessinfo.LOAN_MONTH) <= 36","msg": "贷款期限（月）必须小于或等于36"}]
```

- 贷款利率

```json
[  {   "express": "cfbizBusinessinfo.LOAN_RATE !=null && cfbizBusinessinfo.LOAN_RATE !=''",   "msg": "贷款年利率（%）不能为空"  },  {   "express": "Number(cfbizBusinessinfo.LOAN_RATE) > 0 && Number(cfbizBusinessinfo.LOAN_RATE) <= 20",   "msg": "贷款年利率（%）必须大于0且小于或等于20"  } ]
```

- 联系电话

```json
[  {   "express": "cfbizBusinessinfo.MANAGER_TELL != null && cfbizBusinessinfo.MANAGER_TELL !=''",   "msg": "联系电话不能为空"  },  {   "express": "/(^(0[0-9]{2,3}\\-)([0-9]{7,8})$)|(^0?[1][358][0-9]{9}$)/.test(cfbizBusinessinfo.MANAGER_TELL)",   "msg": "必须填写有效的联系电话或手机号码"  } ]
```

- 是否他行担保

```json
[  {   "express": "cfbizBusinessinfo.IS_OTHER_BANK_GUARANTEE !=null && cfbizBusinessinfo.IS_OTHER_BANK_GUARANTEE !=''",   "msg": "是否他行担保不能为空"  },  {   "express": "['Y','N'].indexOf(cfbizBusinessinfo.IS_OTHER_BANK_GUARANTEE)>=0",   "msg": "是否他行担保只能填写【是】或【否】"  } ]
```

- 产品名称

```json
[{"express": "cfbizBusinessinfo.PRODUCT_NAME != null && cfbizBusinessinfo.PRODUCT_NAME !=''","msg": "产品名称不能为空"}, {"express": "['CGCP','SND_FSD','HA_FSD','HA_ZCD','SND_FMD','ZD_CMSCD','ZL_WGFDD','NK_LSZZDHD','YK_SND_JQ','YC_LPD','NJ33DSGYL','CZ_HND','LJT_PLCP','NT_YCD','ZJ_JTNCPL','SND_MLXCD','NTD','XNJYD','JGNDD'].indexOf(cfbizBusinessinfo.PRODUCT_NAME)>=0","msg": "产品名称必须存在"}]
```



