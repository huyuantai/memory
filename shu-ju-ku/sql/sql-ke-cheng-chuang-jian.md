create table student(sid int primary key auto_increment, 
sname varchar(20), 
sage date, 
ssex enum('男','女'));

insert into student values(1,'赵雷','1990-01-01','男'),
    (2,'钱电','1990-12-21','男'),
    (3,'孙风','1990-05-20','男'),
    (4,'李云','1990-08-06','男'),
    (5,'周梅','1991-12-01','女'),
    (6,'吴兰','1992-03-01','女'),
    (7,'郑竹','1989-07-01','女'),
    (8,'王菊','1990-01-20','女');


create table course(cid int primary key auto_increment, 
cname varchar(20), 
tid int);


insert into course values(1,'语文',2),
            (2,'数学',1),
            (3,'数学',3);
						
						
						
create table teacher(tid int primary key auto_increment, 
tname varchar(20));


insert into teacher values(1,'张三'),
        (2,'李四'),
        (3,'王五');
				
				
create table sc(sid int, 
cid int, 
score int);
						
				
insert into sc values(1,1,90),
            (1,2,80),
            (1,3,90),
            (2,1,70),
            (2,2,60),
            (2,3,80),
            (3,1,80),
            (3,2,80),
            (3,3,80),
            (4,1,50),
            (4,2,30),
            (4,3,20),
            (5,1,76),
            (5,2,87),
            (6,1,31),
            (6,3,34),
            (7,2,89),
            (7,3,98);