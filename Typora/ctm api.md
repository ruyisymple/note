# 1、创建文件

调用接口https://172.253.32.101:8443/automation-api/build

传入json参数

```
{
    "Defaults" : {
        "Application" : "TestApp",
        "SubApplication" : "TestA",
        "RunAs" : "user01",
        "Host" : "HOST",

        "Job": {
            "When" : {
                "Months": ["JAN", "OCT", "DEC"],
                "MonthDays":["22","1","11"],
                "WeekDays":["MON","TUE", "WED", "THU", "FRI"],
                "FromTime":"0300",
                "ToTime":"2100"
            },
            "ActionIfFailure" : {
                "Type": "If",       
                "CompletionStatus": "NOTOK",
                
                "mailToTeam": {
                    "Type": "Mail",
                    "Message": "%%JOBNAME failed",
                    "To": "team@mycomp.com"
                }
            }
        }
    },
        "AutomationAPISampleFlow": {
        "Type": "Folder",
        "Comment" : "Code reviewed by John",

        "CommandJob1": {
            "Type": "Job:Command",
            "Command": "echo my 1st job"
        },

        "ScriptJob": {
            "Type": "Job:Script",
          	"FilePath":"SCRIPT_PATH",
          	"FileName":"SCRIPT_NAME"
        },
        "CommandJob2": {
            "Type": "Job:Command",
            "Command": "echo my 1st job"
        },

        "Flow": {
            "Type": "Flow",
            "Sequence": ["CommandJob1", "ScriptJob"]
        }
    }
}


```

参数描述：        "Defaults"全局默认参数（可以在具体作业中修改，如调度时间）

​								 "Application" : "TestApp",     逻辑层属主
​       				 		"SubApplication" : "TestA",    逻辑层分类
​       						 "RunAs" : "user01",        执行用户
​        						"Host" : "HOST",    运行主机

​					When:定义时间（参数https://docs.bmc.com/docs/automation-api/monthly/job-properties-1116950305.html#JobProperties-When）

​					ActionIfFailure  当作业没有完成时触发事件 （"Type": "If":当作业满足某个状态时触发事件）

​			

​					AutomationAPISampleFlow 文件夹名称（"Type": "Folder"：定义一个文件夹类型）

​					CommandJob1作业名称（"Type": "Job:Command"：定义一个作业类型，可以定义各种作业类型（https://docs.bmc.com/docs/automation-api/monthly/job-types-1116950308.html））

​					Flow 依赖名称（"Type": "Flow"：定义依赖）可定义多个

​				 "Sequence": ["CommandJob1", "ScriptJob"]  按照此队列执行作业



总结：根据"Type"类型的不同产生不同的作业行为（https://docs.bmc.com/docs/automation-api/monthly/job-properties-1116950305.html）

# 2、运行作业

接口https://172.253.32.101:8443/automation-api/run

传入上述json文件

# 3、删除作业

接口https://172.253.32.101:8443/automation-api/run/job/{{jobId}}/delete

只是标记删除（先hold再delete），删除实例

接口https://172.253.32.101:8443/automation-api/deploy/job/{{jobPath}}/{server}/{library}?server=ctrlm1&library=

jobPath代表作业地址，子父文件使用：隔开，server是ctm-server服务器名称(这里是ctrlm1)，只有一个可省略，library可省略



# 4、修改作业

https://172.253.32.101:8443/automation-api/deploy

将更新后的json文件传入即可

