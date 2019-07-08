#  DML

- ### insert

  - 语法

    ```sql
    insert into 表名 values （建表时的顺序）
    insert into 表名(列名) values(列名类型)
    ```

  - 备份表——备份2表 

    ```sql
    insert into 表名 
    	select * from 表名2
    ```

    

- ### update

  - 语法

    ```sql
    update 表名 set 列名1 = 值1, 列名n = 值n where 条件 -- 一定要加条件，避免全部修改
    ```

    

- ### delete

  - 删除表的数据，如果不提交数据是能找出的

  - 语法

    ```sql
    delete from 表名 where 条件 -- 一定要加条件，避免全部修改
    ```

  - 用到delete很少

# DDL

- ### create 创建表

  - 语法

    ```sql
    create table 表名(
    	字段名 类型 默认值 是否非空
      
      Constraint 约束
    )
    ```

  - 拷贝数据

    ```sql
    create table 备份表名 as
    SELECT * 
    FROM 原数据表; -- 只能拷贝数据、字段
    ```

- ### alert

  - 修改表结构，如增加、删除、修改字段等操作

  - 语法

    ```sql
    -- 添加列
    alert table 表名
    add (
      列名 类型 默认值 约束
    )
    	
    
    -- 修改列
    modify(
    )
    
    -- 删除列
    drop column 列名
    
    -- 删除约束
    
    -- 让约束失效
    
    -- 让约束生效
    
    
    ```

  - **注意事项** ：最好不要随便创建表


# 删除的特点

- ### drop

  - 删除表、表结构、表空间、彻底删除——不能找回数据

- ### truncate

  - 删除表中的、数据、表空间 
  
- ### delete

  -  Object obj =null;

  -  相当于不带条件的delete操作

# 视图

# 索引

- ### 特点

  - 优势：大大加快了查询的速度
  - 劣势：索引会占据物理空间
    - 如果对数据进行添加，删除，修改的时候，索引也会自动的动态维护，这样会降低维护的速度。
  - 主键自带索引
  - 

- ### 语法

  ```sql
  create index 索引名 on 表名(列名) -- 创建索引
  drop index 索引名 -- 删除索引
  create index  -- 联合索引
  ```

# 触发器-trigger

- ### 说明：

  - 触发器的定义就是说某个条件成立的时候，触发器里面所定义的语句就会被自动的执行。
  - 触发器不需要人为的去调用，也不能调用。
  - 

- ### 功能：— （行级触发器、语句级触发器）

  - 行级触发器 — 行级触发器则是在定义的了触发的表中的行数据改变时就会被触发一次
  - 语句级触发器 — 语句级的触发器可以在某些语句执行前或执行后被触发

  1. 允许/限制对表的修改
  2. 自动生成派生列，比如自增字段
  3.  强制数据一致性
  4.  提供审计和日志记录
  5.  防止无效的事务处理
  6.  启用复杂的业务逻辑

- ### 语法：

  ```sql
  create [or replace] tigger 触发器名 触发时间 触发事件
  on 表名
  [for each row]
  begin
   pl/sql语句
  end
  ```

  其中：
  
  触发器名：触发器对象的名称。由于触发器是数据库自动执行的，因此该名称只是一个名称，没有实质的用途。
  触发时间：指明触发器何时执行，该值可取：
  before：表示在数据库动作之前触发器执行;
  after：表示在数据库动作之后触发器执行。
  触发事件：指明哪些数据库动作会触发此触发器：
  insert：数据库插入会触发此触发器;
  update：数据库修改会触发此触发器;
  delete：数据库删除会触发此触发器。
  表 名：数据库触发器所在的表。
  for each row：对表的每一行触发器执行一次。如果没有这一选项，则只对整个表执行一次。
  
- ### 举例

  1. 允许/限制对表的修改

     ```sql
     /*下面的触发器在更新表tb_emp之前触发，目的是不允许在周末修改表*/
     create or replace trigger auth_secure before insert or update or DELETE
     on tb_emp
     begin
       IF(to_char(sysdate,'DY')='星期日') THEN
         RAISE_APPLICATION_ERROR(-20600,'不能在周末修改表tb_emp');
       END IF;
     END;
     ```

     