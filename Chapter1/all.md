# 第 1 节 表单组&表单配置



### 1 表单组配置流程

1. 增加表单

   表单可以理解为,同类,例如“客户信息”设计成一个表单.

   多个表单可以组成一个表单组.

2. 增加表单组

   表单组,必须有1个主表单,0或n个子表单.

   表单组可以理解为,关联关系,1对1,1对多,前面的1是主表单,后面的n是子表单.

3. 发布表单组

   发布的表单组,一个表单组‘对应’一个父文件夹,父文件夹下每一个文件夹都对应一个表单.

4. 配置表单组菜单

   参考[第 5 节 还在傻傻的配菜单?-配置](Chapter2/menu.md),多个表单组菜单可以用“父菜单”组织起来.

   - 类型选“菜单”才能作为“菜单”被显示
   - 超级管理员(root)默认能够看到全部菜单

5. 确认表单组菜单

   配好菜单后,**重新登录**就可看到页面.

   如果有问题,参考[表单组生成常见问题](Chapter1/faq.md)

6. 修改表单配置

   参考[第 6 节 已同步数据库,修改表单数据库字段-配置](Chapter2/db_field.md)

### 2 表单管理

以下内容来自redmine,没细究

1. 级联【控件】：配置属性：扩展信息字段中，controlAttributes属性配置为空，则默认必须选择最后一层；若controlAttributes属性值为"change-on-select"，则可以选择任意一级。

2. 按钮【控件】：配置属性：扩展信息字段中，controlChangeEvent：配置调用接口；buttonFunctionBody：调用接口后执行的函数体。

3. 多选下拉、单选下拉、文本框、多行文本、密码框、金额框【控件】：配置属性：扩展信息字段中，placeholder若有值，提示信息默认为该值，否则根据字段备注自动生成。

4. 文档生成【控件】：配置属性：扩展信息字段中，buttonFunctionBody：文档生成成功后执行的函数体。

5. 编号控件： 配置信息参考 [#9405](http://longersoftdb.vicp.cc:8088/issues/9405)

6. 超链接【控件】：配置属性：

   linkName：超链接名称

   linkType：超链接类型，file(文件下载)、route(路由跳转)、http(外部链接)

   linkPathV：超链接地址，例：'/path?field=${tableName.fieldName}&field2='+loginUser.username

   【注】：表单组列表字段若显示为超链接，也需配置上述三个属性，且linkType只能为"route"

   ```
   {"sign": "", "linkName": "放款登记", "linkType": "route", "linkPathV": "'/LoanReg_edit?masterId=${cfbizGuarantee.ID}'", "selectData": {"columnAs": {}, "dataSource": ""}, "slotAppend": "", "slotPrefix": "", "slotSuffix": "", "placeholder": "", "slotPrepend": "", "jsExpression": "", "textareaRows": "2", "valueDefault": "", "codeGenerator": {"sn": "", "pSn": "", "formatCode": ""}, "sqlExpression": "", "conversionRate": 1, "controlInputHide": "N", "controlLabelHide": "N", "controlAttributes": "", "controlPagination": "Y", "buttonFunctionBody": "", "controlChangeEvent": "", "documentTemplateCodeV": "", "controlAllowCreateItem": "N"}
   ```

7. 文档生成【控件】：配置属性：
   linkName：文档生成组件显示名称
   documentTemplateCodeV：文档模板编码（变量）
   sign：为空则不签名，只生成文档。
   安心签 =》配置变量：
   1.根据关键字：{'type':'anxinsign','keyword':{'content':'开立时间','offsetCoordX':'30','offsetCoordY':'0','imageWidth':'150','imageHeight':'150'}}
   2.根据指定位置：{'type':'anxinsign','location':{'leftBottomX':'', 'leftBottomY':'', 'rightTopX':'', 'rightTopY':'', 'pageNumber':'1'}}
   自定义图片签章（暂未开放）=》配置变量：
   1.{'type':'image','imageId':'','keyword':{}}
   2.{'type':'image','imageId':'','location':{}}

8. [本条合并到 =》第 1.4 节 字典-正则校验](Chapter1/dict_regular.md)

   校验规则的定义如果变更(通过字典管理中的校验)，则需要重新登录后才生效
   原因：校验规则在登录时重新加载到缓存中

### 3 表单组管理

以下内容来自redmine,没细究

1. 表单组的添加

2. 表单组的删除按钮
   扩展信息中的enable控件的是是否有权限删除该数据，而不是控件删除按钮的是否显示

3. 表单组的编辑

   - 流程标题的设置
     支持以下变量
     流程信息（processInfo.name）
     环节信息（taskInfo.name）
     表单信息（${物理表名.字段名}）

4. 页签配置
   子组件传参配置说明:
   一、关联关系组件:
   (1)属性名:customerTableName,属性值:(客户表物理表名)
   (2)属性名:relationOperateType,属性值:客户表不为主表时business;
   二、签收材料：
   (1)属性名:attachmentDict,属性值:(支持三元表达式，字典分类值,例:$$DEMO)
   三、懒加载配置：
   主表、子表一对一不支持组件懒加载，子表一对多以及自定义组件支持懒加载。
   四、组件必填校验
   自定义组件以及子表一对多支持配置，支持条件表达式配置（暂支持登录信息），当组件设为懒加载时，该功能无效。
   五、数据源配置
   路径支持传参格式：@views/generatedForm/statisticsForm/BusinessStatusSV.vue?param1='aaa'&param2='bbb'
   =>解析参数为： AND param1='aaa' AND param2='bbb'
   统计配置中的sql添加${routeParams}【注意sql语句的正确性】

5. 全局校验JS
   可以在每个【主表】以及【子表一对一】表单中配置，页面保存时优先校验，提示信息在该表单页签的最上方。

6. 外键表单配置（即可添加也可选择表单）

   配置要点如下：

   - 【表单组编辑页面】表单组关联表单的外键设为ID

   - 【页签配置页面】子组件传参

     属性名（固定）：customizeFid
     属性值格式：子表名${主表名.字段名} | 是否可新增（true / false）（示例：CFBIZ_Customer${CFBIZ_Guarantee.customer_id} | true）

     批次附件上传（压缩文件）的配置

     ```json
     "upload": {
       "dictCode": "ATTACHMENTS_FPXD",   // 指定附件字典项编码
       "enabled": "true",   // 是否生成上传按钮
       "name": ""  // 指定按钮名称
     },
     ```

### 3 动态表单使用

以下内容来自redmine,没细究

1. 单使用内嵌组件合计行的值：this.${tableName}.${fieldName}[${lastLength}].${componentFieldName}
   ${tableName}：表名
   ${fieldName} ：内嵌组件字段名
   ${lastLength} ：内嵌组件列表最后一行index
   ${componentFieldName} ：内嵌组件列表的字段名
2. 动态表单列表页面查询条件支持路由传参：routePath："/test_list?fieldA=xx&fieldB=yy"
3. 动态表单【主表】、【子表一对一】新增页面支持路由传参：routePath："/test_add?tableName.fieldName=xx&tableName.fieldName=yy"
4. 动态表单列表页面导出功能支持动态选择条目导出。不选则默认导出所有。
5. 统计表在动态表单中的使用
   通用配置：
   1.页签配置中，新建自定义组件。组件地址填入改统计页面的物理路径。查询设置按钮点击填入统计过滤条件(配置示例：fieldName=${tableName.fieldName}&fieldName……)
   嵌入样式：
   1.tab页签形式：
   表单组列表页面，页面配置中，选中【tab切换加载】=>点击页签时，刷新统计。
   2.内嵌形式：
   1.表单组页面配置找到改内嵌字段，填写组件地址。注意：表名为必填，填写内容为在统计在表单组页面配置中，填写的表名。若不保持一致，则查询条件无法获取。
   2.作为内嵌时，不主动触发查询。需要人工写代码触发。示例：
   this.$refs["statistics_ref"].tabInit();
   statistics_ref为该统计组件在页面的实例。
   注意：【查询条件变更】或者【tab切换加载变更】时，不需要重新生成页面，配置即生效。
6. 动态表单字段、分组权限执行顺序以及隐藏配置：
   1.表单组编辑页面，扩展信息字段："commonConfig": {"pageInitItemEnabled": "Y"}。pageInitItemEnabled为Y时，默认页面加载字段以及分组均显示，为N时，与之相反，全部隐藏。
   2.页面监听JS中(pageWatchJs),执行顺序为：
   1）表单组字段权限配置脚本（模板固定），
   2）表单编辑页面配置的监听脚本（配置内容），
   3）表单组页面配置中，该表单设置的监听脚本（配置内容）
   4）分组默认权限：该分组中的字段有一个显示，则分组显示，若全部隐藏，则分组隐藏（模板固定）。
   提示(2.0中)：
   原先隐藏分组的脚本：this.fieldGroupHide.tableName.fieldGroupCode = true;已失效，最新的隐藏脚本为：this.hideFieldGroup("fieldGroupCode");

### 4 注意事项

1. 定制表单的表单文件规范统一设为（*Customized.vue）格式（例如：editCustomized.vue）
   目的：自动生成后提交代码时只需比较后缀为（*Customized.vue）的文件，确定定制内容后再提交
2. 【表单管理】数据字段》允许空值 默认设置为允许，通过表单组的必填项控制
   如果该处设为不允许，通过表单组设置为非必填项时会异常
3. 多选文本框的宽度需要设置为24栅格（因固定高度问题，校验提示消息会被覆盖）
4. 当表单中的元素或表单有增删时，需要重新打开表单组的页面配置并保存（目前不能自动更新到表单组中）
5. 通过表单或表单组的WatchJS对于页面元素赋值时如果每次都赋值，则该元素通过页面是无法操作的，建议设置为只读

### 5 文档模板

- 文档模板的表单域支持表达式配置：
  （1）简单表单数据替换：${tableName.fieldName}
  （2）金额计算：Number(${tableName.fieldName})*100+200
  （3）金额转大写：ArabiaToChinese(${tableName.fieldName})
  （4）三元表达式：${tableName.fieldName}=="abc" ? "123" : ${tableName.fieldName}

- 表格循环行配置

  注意：doc文档格式需要预留多余的空行（因不能根据条数自动生成行），否则生成不全。.docx无需

  | ${foreachTableRow}     | tableName              |                        |
  | ---------------------- | ---------------------- | ---------------------- |
  | 标题1                  | 标题2                  | 标题3                  |
  | ${foreachRows}         |                        |                        |
  | ${tableName.fieldName} | ${tableName.fieldName} | ${tableName.fieldName} |

- 注意事项
  【.doc】格式
  \1. 表格以及图片不可设置特殊格式，否则会生成异常。
  \2. 表格列最多不超过9列
  【.docx】格式
  \1. 生成word样式会丢失，但没有以上【.doc】的限制。