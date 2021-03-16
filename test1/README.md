# 实验1：SQL语句的执行计划分析与优化指导
## 实验目的
```text
分析SQL执行计划，执行SQL语句的优化指导。理解分析SQL语句的执行计划的重要作用。
```
## 实验内容
### 1. 运行和分析下面两个语句并分析判断哪个语句更优。
  #### 1) 语句1
* 代码
```SQL
set autotrace on

SELECT d.department_name,count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
from hr.departments d,hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT','Sales')
GROUP BY d.department_name;
```
* 截图  
![语句1结果](1.png)
#### 2) 语句2:
* 代码：
```SQL
set autotrace on

SELECT d.department_name,count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
FROM hr.departments d,hr.employees e
WHERE d.department_id = e.department_id
GROUP BY d.department_name
HAVING d.department_name in ('IT','Sales');
```
* 截图：  
![语句2结果](2.png)
#### (3)分析和判断
* 语句1运行消耗时长  
![语句1消耗时长](1.1.png)
* 语句2运行消耗时长  
![语句2消耗时长](2.1.png)
```text
由图可知，语句1的运行消耗时长比语句2的运行消耗时长更短，说明语句1比语句2的效率更高
造成这种结果的原因是：
语句1是先筛选出符合条件的数据，再将数据进行分组；而语句2是先将数据进行分组，再去筛选出符合条件的语句。
这样一来，在执行分组操作时，语句1实际操作的数据比语句2的更少，因此花费的时间更少
```
