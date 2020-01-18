# 第 4 节 扩展字段的使用

对,你没看错!扩展字段就是“系统保留字段”(EXTEND_INFO).因为他是JSON,所以用处多多.

我用这个"EXTEND_INFO"做修改留痕

我用这个“ERROR_INFO”做错误记录

我用类似JSON扩展出很多字段

就酱!!!

### 1 坑

虽然很简单,但是,在担保配置系统中,还是有所差别的.

- 对象的时候,传回后台,得JSON.stringify

  ```js
  function convertToSave(param) {
    let data = param.formDataList[0].manipulationData
    
    let ENTERPRISE_INFO = {
      REGISTERED_CAPITAL: 0, // data.REGISTERED_CAPITAL, // 注册资本[万元]
      PAID_CAPITAL: 0, // data.PAID_CAPITAL, // 实收资本[万元]
      SALES_REVENUE: data.SALES_REVENUE, // 销售收入[万元]
      TOTAL_ASSETS: data.TOTAL_ASSETS, // 资产总额[万元]
      EMPLOYED_POPULATION: 0, // data.EMPLOYED_POPULATION, // 从业人数
      ENTERPRISE_SIZE: 'WXQY', // data.ENTERPRISE_SIZE, // 企业规模
      PROMOTE_EMPLOYMENT: data.PROMOTE_EMPLOYMENT, // 带动就业
      DRIVE_REVENUE_GROWTH: data.DRIVE_REVENUE_GROWTH // 带动增收[万元]
    }
    data.ENTERPRISE_INFO = JSON.stringify(ENTERPRISE_INFO, null, 1)
    
    /** 中间省略一大段 */
    return param
  }
  ```

- 数组的时候,不需要任何处理.

  昨天,看到数据库'\\\\[]\\'\一串引号、斜杠的时候.

  我猜想,当然靠猜,天天调试,就没时间做项目了不是?

  大概后台对数组做了处理,JSON对象就没有.

### 2 参考代码

- 可以是对象

  对象的时候, 一个字段可以是千千万万(允许我夸张)个“前端字段”,我得贴段代码

  ```js
  function convertToShow(data) {
    /* JSON字段特殊处理 */
    if (data.jsndHistoryBusinessB.ENTERPRISE_INFO) {
      // data.jsndHistoryBusinessB.ENTERPRISE_INFO = JSON.stringify(data.jsndHistoryBusinessB.ENTERPRISE_INFO);
  
      data.jsndHistoryBusinessB['REGISTERED_CAPITAL'] =
        data.jsndHistoryBusinessB.ENTERPRISE_INFO.REGISTERED_CAPITAL
      data.jsndHistoryBusinessB['PAID_CAPITAL'] =
        data.jsndHistoryBusinessB.ENTERPRISE_INFO.PAID_CAPITAL
      data.jsndHistoryBusinessB['SALES_REVENUE'] =
        data.jsndHistoryBusinessB.ENTERPRISE_INFO.SALES_REVENUE
      data.jsndHistoryBusinessB['TOTAL_ASSETS'] =
        data.jsndHistoryBusinessB.ENTERPRISE_INFO.TOTAL_ASSETS
      data.jsndHistoryBusinessB['EMPLOYED_POPULATION'] =
        data.jsndHistoryBusinessB.ENTERPRISE_INFO.EMPLOYED_POPULATION
      data.jsndHistoryBusinessB['ENTERPRISE_SIZE'] =
        data.jsndHistoryBusinessB.ENTERPRISE_INFO.ENTERPRISE_SIZE
      data.jsndHistoryBusinessB['PROMOTE_EMPLOYMENT'] =
        data.jsndHistoryBusinessB.ENTERPRISE_INFO.PROMOTE_EMPLOYMENT
      data.jsndHistoryBusinessB['DRIVE_REVENUE_GROWTH'] =
        data.jsndHistoryBusinessB.ENTERPRISE_INFO.DRIVE_REVENUE_GROWTH
    }
  
    /** 中间省略一大段 */
    return data
  }
  ```

  

- 可是是数组

  数组的时候,一个字段可以是千千万万行“前端行”,我还是得贴段代码

  ```js
  /* JSON字段特殊处理 */
  if(data.cfbizBusinessinfo.EXTEND_INFO){
    if (!this.isNotEmpty(data.cfbizBusinessinfo.EXTEND_INFO)) {
      data.cfbizBusinessinfo.EXTEND_INFO = []
    }
    // 是个数组
    // data.cfbizBusinessinfo.EXTEND_INFO = JSON.stringify(data.cfbizBusinessinfo.EXTEND_INFO);
  }
  ```

  直接JSON.stringify?那是万万不行的.手工写JSON,太容易错了.

