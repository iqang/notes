1. **select 语法结构**

   ```sql
   select ... from ...;
   ```

   > Select 语法结构为select  列名、函数名、常量  from 表名、dual



2. **列的别名**

   select语句支持给列起别名，别名包含空格等字符时可以使用一对“”将列名括起来

   ```sql
   # 通过as关键字进行别名命名
   select last_name as lname from dual;
   # 省略关键字
   select last_name lname from dual;
   
   #使用双引号，省略关键字
   select last_name "lname" from dual;
   
   select first_name as fname,last_name lname,salary "sal",commission_pct "cp this year" from employees order by commission_pct desc limit 5;
   ```

   

3. **去除重复行**

   > DISTINCT 关键字去重，语法为 select distinct 列名 from dual；

   ```sql
   # 正确用法
   select distinct department_id from employees;
   
   # 错误用法
   select department_id，distinct salary from employees;
   
   # 其他场景-多列组合去重
   select distinct department_id，salary from employees;
   
   ```

   

4. **空值参与运算**

   > null 空值不等于0、''、空对象; 空值参与的任何运算值也为空值，可以使用ifnull(column,vaule)函数进行替代计算

   ```sql
   select salary,salary*(1+cp)*12 from employees;
   ```



5.  **着重号``**

   > 如果字段或者表名使用了数据库的关键字，则使用着重号进行处理

   ```sql
   select * from `order` #order 为关键字，作为表名使用时候必须添加着重号（``）修饰否则报语法错误
   ```

   

6.  **查询常数**

   > 当查询结果需要返回某一常量固定列时候，直接写到查询列名处即可
   ```sql
   select '尚硅谷',123,name,salary from `order` #order 为关键字，作为表名使用时候必须添加着重号（``）修饰否则报语法错误
   ```
   
   

7. **显示表结构**

   > 显示表中的字段信息，使用describe、desc 表名进行查看。

   ```sql
   describe table;
   desc table;
   ```

   

8. **数据过滤**

   > 使用WHERE关键字进行数据的过滤，语法结构为select 列名 from 表名 where 条件

   ```sql 
   select name,age from employee where age >30;
   # SQL标准规定mysql的关键字大小写不敏感，对数据部分大小写敏感（MySQL没有严格遵守规范，因此mysql大小写不敏感）
   ```

   

   