From A 
Left Join B ON A.t_id = B.t_id 
Left Join C ON A.p_id = C.p_id 

首先A 与 B 连接得到 AB的连接后结果集【AB集】，
然后【AB集】在与C连接得到【AB集】C集

连接可以=，>,< 等等，如
> ON A.t_id = B.t_id 
> ON A.t_id > B.t_id 
> ON A.t_id < B.t_id 



a:  From A  Left Join B ON A.t_id = B.t_id AND B.status = 1
与
b:  From A  Left Join B ON A.t_id = B.t_id Where B.status = 1
的区别
















