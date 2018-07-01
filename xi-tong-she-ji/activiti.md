
activi 学习网站
流程概览了解：https://www.jianshu.com/p/bdc9c9fa719d
https://my.oschina.net/u/1764868/blog/401975
https://www.jianshu.com/p/701056e672a4


# 工作流
工作流（workflow）就是工作流程的计算模型，即将工作流程中的工作如何前后组织在一起的逻辑和规则在计算机中以恰当的模型进行表示并对其实施计算

> 工作流：以恰当的模型进行表示并对其实施计算
  模型：xml形式定义、或模型工具

将部分或者全部的工作流程、逻辑让计算机帮你来处理，实现自动化

![](/assets/10135025-afeff18c785c7345.png)

#### 以上控件为：
StartEvent，UserTask，ExlusiveGateway，UserTask，EndEvent
连线都是SequenceFlow
ExlusiveGateway:排他，并行； 排他，几个人谁先签谁执行控件


1.编辑流程xml，或用工具设计bpm
2.部署流程
3.前端请假信息表单提交
4.后台一个Leave对象用于保存请假信息（表单），保存相应的数据库表为 leave
5.启动流程：runtimeService.startProcessInstanceByKey
6.查看提交的任务，在请假申请的办理人assignee
List<Task> taskList = taskService.createTaskQuery().taskAssignee(assignee).list();
7.流程审批：通过 taskId 就可以对当前执行的任务进行审批
TaskService taskService = processEngine.getTaskService();
taskService.complete(taskid, map);