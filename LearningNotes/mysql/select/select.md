1. **select 语法结构**

   ```sql
   select ... from ...;
   ```

   > Select 语法结构为select  列名、函数名、常量  from 表名、dual



2. ------

   **列的别名**

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

   ------

   

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

   ------

   

4. **空值参与运算**