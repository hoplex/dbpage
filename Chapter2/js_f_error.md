# 第 7 节 插播一条JS广告

JS易错点广而告之!!!

- 类型是字符串的[数字]乘以数字结果是数字.[真的字符串]乘以数字结果是NaN,NaN（Not A Number）通过typeof判断是个数字

  这句很绕,但请记住,不要试图通过运算结果去判断原始字符串是否是数字.

- 判断null或者undefined时**——代码截图**
  - 如果使用X==null,X是null或者undefined,等式都能成立
  - 如果使用X===null,等式不成立

- 判断空字符串时,不能用X==‘’,需要使用X===‘’**——代码截图**

  因为0==‘’,js认为相等

- 最重要的,1273.86*10000=12738600,看看JS计算的结果

  <img src="./img/js_f_error_2.png" alt="js_f_error_2" style="zoom: 50%;" />

###### 代码截图

bug给圈上.还有,第一个条件被包含在第二个条件中了!

<img src="./img/js_f_error_1.png" alt="js_f_error_1" style="zoom:67%;" />