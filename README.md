# Udacity_ML

已完成项目有：

   1)Titanic_Survival_Exploration
   
   2)Predicting Boston Housing Prices
   
   3)Building a Student Intervention System
   
   4)use unsupervised learning techniques to see if any similarities exist between customers, and how to best segment customers into distinct categories
   
   
 Kickoff是服务器的禁播功能，支持用户踢正在直播的流，并将这个流禁播（禁止推流）一定时间。

### Workflow

下面说明禁播的主要工作流程：

1. BMS中配置后端API的地址，vhost中配置是否开启禁播功能。
1. 推流到BMS时，将流的信息送到API验证。若验证失败，则拒绝推流。
1. BMS提供API，后端可以调用接口踢已经在推的流。

> 备注：提供给客户用的禁播接口，除了鉴权（即只允许合法的客户调用禁播API）之外，还需要从BOCAR中查询流所在的服务器，然后调用BMS的API。

### Kickoff API

Kickoff API是BMS提供给后端调用的，可以用来踢已经在推的流。

```
req: GET http://ip:port/api/v1/control/kick?domain={domain}&app={app}&stream={stream}
res: {"code": 0}

错误码：
    0     --- 请求成功，流已剔出
    100   --- 输入参数domain/app/stream为空
```

