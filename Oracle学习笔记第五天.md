# 触发器：

- 触发器，是通过系统调用的，
- 只对DML语句才能触发，
- 触发器是有名字的
- create创建
- drop删除

# 存储过程：

- 存储函数，它相当于我们java当中的方法，会把内容块封装到方法当中，便于下一次使用的时候调用。
- 传入的参数 java需要让数据库执行的时候，传入的参数
- 传出的参数 java需要接收到数据库执行完成之后的返回值

```sql
--无参的存储过程
Create or replace procedure 存储过程名
As
    --1、定义游标
     cursor my_stu is select * from student ;
  begin
     --2、加入循环
     for stu in my_stu loop 
        dbms_output.put_line('学号：' || stu.stuid || ' 姓名：' || stu.stuname);
     end loop ;
  end;

--有参的存储过程
Create or replace procedure pro_my_emp
(begin_sal number,end_sal number)
As
    --1、定义游标
     cursor my_emp is select * from emp where sal between begin_sal and end_sal;
  begin
     --2、加入循环
     for emps in my_emp loop 
        dbms_output.put_line( ' 姓名：' || emps.ename || '工资：'|| emps.sal);
     end loop ;
  end;
  
  begin
     pro_my_emp(800,3000);
 end;
  

-- 有参的，并且有返回值得存储过程
--通过传入empno，查找到员工的姓名
Create or replace procedure pro_get_name
(empno in number,ename out varchar2)
As
  begin
    select e.ename into ename from emp e where e.empno = empno and rownum=1;
  end;
  
select * from emp where empno=7369;  

declare
  ename varchar2(20);  
begin
    pro_get_name(7369,ename);
    dbms_output.put_line(ename);
 end; 
```



# 匿名代码块

```sql
declare
声明变量;
begin
	内容块;
end;
```

# 随堂练习

1. 使用Oracle的case when来实现年龄打印	

   ​	如果是10岁 打印未成年

   ​	如果是 20岁 打印青年

   ​	如果是 30岁 打印中年

   ​	如果是 50 岁 打印中老年

   ​	否则  打印老年

   ```sql
   declare
       s_age   number;
       message varchar2(10);
   begin
       case s_age
           when 10 then message := '未成年';
           when 20 then message := '青年';
           when 30 then message := '中年';
           when 50 then message := '中老年';
           else message := '老年';
           end case;
   end;
   ```

2. 循环打印出1—100 的和

   ```sql
   -- while loop 
    declare
     v_num number := 0;
     begin
           while v_num <100  loop
              v_num := v_num+1;
              dbms_output.put_line(v_num);
           end loop;
     end;
    -- for loop
     declare
   
     begin
          for i in 1..100  loop
              dbms_output.put_line(i);
           end loop;
     end;
   ```

3. 通过游标将所有学生的科目和分数，打印出来

   ```sql
   --读取一行游标的方式
    declare
       --s_id number;
       -- s_name varchar2(20);
       s_id student.stuid%type;
       s_name student.stuname%type;
        --1、定义游标
        cursor my_stu is select stuid,stuname from student where stuid=1;
     begin
        --2、打开游标
        open my_stu;
        --3、判断游标是否取到了值
        if my_stu%notfound then
           dbms_output.put_line('数据为空，没有找到记录');
        else
           --4、读取游标的内容
           fetch my_stu into s_id,s_name;
        end if;
        dbms_output.put_line('学号：' || s_id || ' 姓名：' || s_name);
        --5、关闭游标
        close my_stu;
     end;
     
   --读取多行游标的方法
   declare
        s_id number;
        s_name varchar2(20);
        --1、定义游标
        cursor my_stu is select stuid,stuname from student ;
     begin
        --2、打开游标
        open my_stu;
        --3、加入循环
        loop 
          --4、读取游标的内容
           fetch my_stu into s_id,s_name;
           --5、判断游标是否还有值，没有值就退出
           exit when my_stu%notfound;  
           dbms_output.put_line('学号：' || s_id || ' 姓名：' || s_name);
        end loop ;
        --6、关闭游标
        close my_stu;
     end;
     
     --改成 for loop 拿到游标
     declare
        --1、定义游标
        cursor my_stu is select * from student ;
     begin
        --2、加入循环
        for stu in my_stu loop 
           dbms_output.put_line('学号：' || stu.stuid || ' 姓名：' || stu.stuname);
        end loop ;
     end;
   ```

   

<u>程序员当中有一句话：能在数据库中搞定的逻辑，不放在java当中实现。</u>

<u>第一个：java处理的效率没有Oracle快，编译，java先要编译成class，然后执行。</u>

<u>第二个：oracle里面执行效率会优于java</u>

<u>第三个：因为java当中需要处理大量的业务需求，所以处理数据需求的时候，都将其放在我们的Oracle中。</u>