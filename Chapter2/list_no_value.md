# 第 13 节 页面列表没有值,点查询才有

###### 问: 核保结束,首保列表页面没有值,点查询才有

答: 

因为一句判断,activated没有调用this.search().created才调用了this.search().vue生命周期,你懂的,所以列表不刷新



<img src="./img/list_no_value_1.png" alt="list_no_value_1" style="zoom:50%;" />

<img src="./img/list_no_value_2.png" alt="list_no_value_2" style="zoom:50%;" />

<img src="./img/list_no_value_3.png" alt="list_no_value_3" style="zoom:50%;" />

<img src="./img/list_no_value_4.png" alt="list_no_value_4" style="zoom:50%;" />