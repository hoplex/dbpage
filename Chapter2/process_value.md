# 第 12 节 流程配置始终取不到值&流程配置

记住:

- 要么是loginUser中的值

- 要么是数据库中的值

前端的值没有传到后台,取不到!!!

### 配置参考

我没有配过流程.贴段配置以供参考,靠悟性了

1. 网关:是否二级分公司

```js
${startUser.companyIdList.size() == 2}
```

2. 网关:一级分公司是否授权

```js
${startUser.companyIdList != null && startUser.companyIdList.size() == 1 && CFBIZ_BUSINESSINFO.hjdRiskAdmit1 == '1' }
```

3. 网关:二级分公司是否授权

```js
${startUser.companyIdList != null && startUser.companyIdList.size() == 2 && CFBIZ_BUSINESSINFO.hjdRiskAdmit2 == '1' }
```

4. 候选人:一级有授权的初审人员审核环节

```js
${CFBIZ_BUSINESSINFO.hjdRiskAdmitPersonList}
```

5. 候选人：二级有授权的初审人员审核环节

```js
${CFBIZ_BUSINESSINFO.hjdRiskAdmitPersonList2}
```

6. 网关:是否区域内

```js
${CFBIZ_BUSINESSINFO.isInArea == '1'}
```

