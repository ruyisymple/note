# Control-M Services api

https://172.253.32.101:8443/automation-api/swagger-ui.htm

## session(创建和销毁用户会话)



### (post)/session/login（登录ctm）

传参：账号密码

作用：验证身份，并会生成一个token字符串，在后续请求中会用到此token

### (post)/session/logout（登出ctm）

传参：无

作用：断开由请求身份验证token指定的用户会话，并从服务器内存中删除它

### (post)/session/user/password/update（修改密码）

传参：账号，当前密码，新密码

作用：更改密码

## authentication（创造和管理身份令牌token）

### (post)/authentication/token（创建token）

传参：样例所示的json文件

作用：创建身份令牌token

### (put)/authentication/token(更新token数据)

传参：样例所示的json文件

作用：更新身份令牌token数据

### (get/authentication/token/{tokenName}(返回token数据)

传参：token name（必须）

​			forAgent（非必须）用于代理，默认false			

作用：接收token数据

### (delete)/authentication/token/{tokenName}(删除token数据)

传参：token name（必须）

​			forAgent（非必须）用于代理，默认false

作用：删除token数据

### (get)/authentication/tokens(返回授权用户的token列表)

传参：forAgent（非必须）用于代理，默认false

作用：返回授权用户的token列表

## bulid(编译json文件)

### (post)/build(编译验证json文件是否有效)

传参：definitionsFile（必须）：要编译的json文件

​			deployDescriptorFile（非必须）：部署描述文件

作用：编译提供的定义文件(JSON或zip)，以验证它对Control-M有效

## deploy(部署)

### (post)/deploy(部署定义的文件)

传参：definitionsFile（必须），部署到服务器上的文件

​			deployDescriptorFile（非必须），部署描述性文件

​			additionalConfiguration（非必须），附加配置以启用本地连接配置文件的跳过测试

作用：将本地文件部署到服务器上

### (post)/deploy/ai/jobtype(部署到代理)

传参：ctm （必须）

​			agent （必须）		

​			jobTypeId （必须）

作用：将现有的作业类型部署到代理上进行

### (get)/deploy/ai/jobtypes（获取作业类型）

传参：jobTypeName（非必须），用于查询作业类型的名称

​			jobTypeId（非必须），用户查询作业类型的id

作用：用于获取与搜索条件匹配的，已经被部署的作业类型

### (delete)/deploy/calendar/{calendarName}(删除日历)

传参：calendarName（必须）

​			server（非必须）

作用：删除日历

### (get)/deploy/calendars（定义日历）

作用：将日历定义为与请求的搜索条件匹配的 json 代码。

### (delete)/deploy/connectionprofile/{server}/{agent}/{type}/{name}(删除配置文件)

作用：删除本地连接的配置文件

### (delete)/deploy/connectionprofile/centralized/{type}/{name}（删除统一配置文件）

作用：删除统一配置文件

### (get)/deploy/connectionprofile/centralized/deploymentstatus/{type}/{name}（查询部署状态）

作用：根据 JSON 格式的搜索查询获取当前部署的连接配置文件部署状态。

### (delete)/deploy/connectionprofile/local/{server}/{agent}/{type}/{name}(删除本地配置文件)

作用：删除本地连接的配置文件

### (post)/deploy/connectionprofile/test(测试配置文件)

作用：在代理上测试配置文件

### (get)/deploy/connectionprofiles(获取配置文件)

作用：根据 JSON 格式的搜索查询获取当前本地部署的连接配置文件。

### (get)/deploy/connectionprofiles/centralized(获取统一配置文件)

作用：搜索查询获取当前集中部署的连接配置文件。

### (get)/deploy/connectionprofiles/centralized/status（获取配置文件状态）

作用：搜索查询获取当前部署的连接配置文件状态。

### (get)/deploy/connectionprofiles/local（获取本地配置文件）

作用：搜索查询获取当前本地部署的连接配置文件

### (delete)/deploy/folder/{server}/{folderName}(删除一个文件夹)

传参：server（必须），服务器名称

​			folderName（必须），文件夹名称

作用：删除文件夹

### (delete)/deploy/job/{jobPath}/{server}/{library}（删除作业）

传参：jobPath（必须），作业路径，使用冒号将父文件夹与子文件夹分开

​			server（非必须），服务器，除非系统中只有一个 Control-M/Server，否则是必需的。

​			library（非必须），资源库

作用：删除作业

### (get)/deploy/jobs(获取定义的文件夹和作业)

传参：format（非必须），输出格式json（默认）或者xml

​			folder

​			ctm

​			server

作用：获取与请求的搜索条件匹配的作业和文件夹（以所需的格式 - JSON 或 XML）。

### (post)/deploy/jobtype(将作业类型部署到服务器)

作用：将提供的作业类型部署到 AI 服务器、EM 服务器和代理。

### (get)/deploy/poll(获取部署结果)

传参：pollid(必须)，获取请求标识

作用：获取部署结果

### (delete)/deploy/sitestandard/{siteStandardName}(删除站点标准)

传参：siteStandardName（必须）

作用：删除一个站点标准

### (post)/deploy/sitestandard/{siteStandardName}(重命名站点标准)

传参：siteStandardName  （必须），当前名字

​			siteStandardNewName （必须），新名称

作用：站点重命名

### (get)/deploy/sitestandard/{standardName}/fieldRestriction/{fieldName}(获取字段允许值)

作用：获取指定站点标准中指定字段的允许值

### (post)/deploy/sitestandard/{standardName}/fieldRestriction/{fieldName}(替换字段的允许值)

作用：替换指定站点标准中指定字段的允许值。

### (get)/deploy/sitestandardpolicies(获取站点标准策略定义)

作用：获取与搜索条件匹配的已部署站点标准策略的定义。

### (post)/deploy/sitestandardpolicies(部署站点标准策略)

传参：siteStandardPoliciesFile （必须）

作用：部署站点标准策略。

### (get)/deploy/sitestandardpolicies/details(获取站点标准策略详情)

作用：获取与请求的搜索条件匹配的已部署站点标准策略的详细信息。

### (delete)/deploy/sitestandardpolicy/{siteStandardPolicyName}(删除站点标准策略)

作用：删除站点标准策略

### (post)/deploy/sitestandardpolicy/{siteStandardPolicyName}(重命名站点标准策略)

作用：重命名站点标准策略

### (get)/deploy/sitestandards(获取站点标准定义)

作用：获取与搜索条件匹配的已部署站点标准的定义。

### (get)/deploy/sitestandards/details(获取站点标准详情)

作用：获取与请求的搜索条件匹配的已部署站点标准的详细信息

### (delete)/deploy/subfolder/{subFolderPath}/{server}/{library}（删除子文件夹）

传参：subFolderPath（必须），子文件夹地址

​			server(非必须)，服务器

​			library(非必须)，资源库

作用：删除子文件夹

### (post)/deploy/transform(转换文件)

作用：根据提供的部署描述符文件 (JSON) 转换提供的定义文件 (JSON)。

## run(运行和跟踪作业)

### (post)/run(运行作业)

传参：jobDefinitionsFile（必须），运行的作业

​			 deployDescriptorFile（非必须），部署描述文件

​			additionalConfiguration（非必须），附加配置以启用本地连接配置文件的跳过测试

作用：运行作业

### (post)/run/alerts(更新告警)

传参：alertModifyValue （必须），包含要更新的警报属性的文件

作用：更新告警

### (post)/run/alerts/status(更新告警状态)

传参：alertModifyStatusValue （必须）

作用：更新告警状态

### (post)/run/event/{server}(添加一个新事件)

传参：server（必须），服务器

​			event（必须），事件

作用：添加一个新事件。 日期可以是 MMDD 格式，ODAT 设置当前控制日期，STAT 设置无日期。 默认值为 ODAT。

### (delete)/run/event/{server}/{name}/{date}(删除一个事件)

传参：server （必须），服务器

​			name （必须），事件名

​			date （必须），事件日期

作用：删除事件

### (get)/run/events(获取事件记录)

传参：详见api

作用：获取特定搜索的所有事件记录

### (post)/run/job/{jobId}/confirm(确认等待确认的作业)

传参：jobId(必须)

作用：确认一个等待确认的作业

### (post)/run/job/{jobId}/delete(标记删除一个作业)

传参：jobId(必须)

作用：删除作业的实例

### (post)/run/job/{jobId}/free(释放一个已经被抓取的作业)

传参：jobId(必须)

作用：释放一个已经被抓取的作业

### (get)/run/job/{jobId}/get(获取正在活动的作业数据)

传参：jobId(必须)

作用：通过作业的 ID 获取活动作业的数据

### (post)/run/job/{jobId}/hold(抓取一个作业)

传参：jobId(必须)

作用：保留该作业，使其在被释放之前不会启动

### (post)/run/job/{jobId}/kill(取消一个正在运行的作业)

传参：jobId(必须)

作用：中止作业执行。

### (get)/run/job/{jobId}/log(获取作业执行日志)

传参：jobId(必须)

作用：获取作业执行日志。

### (post)/run/job/{jobId}/modify(修改作业实例)

传参：jobDefinitionsFile (必须)，修改json

​			jobId (必须)			

作用：根据给定的定义文件 (JSON) 修改由ID 指定的活动作业。当天运行作业的实例，非定义

### (get)/run/job/{jobId}/output(获取作业的输出)

传参：jobId （必须）

​			runNo（非必须），默认为0，多次执行时的执行次数（0 将获得最后一次执行的输出）

作用：获取作业返回的输出。

### (post)/run/job/{jobId}/rerun(重新运行作业)

传参：jobId （必须）

​			rerunParameters（非必须），包含重启配置和参数的 JSON 文件

作用：运行一个已经执行过的作业

### (post)/run/job/{jobId}/runNow(立即执行一个作业)

传参：jobId （必须）

作用：绕过调度条件并开始作业

### (post)/run/job/{jobId}/setToOk(将作业的结束状态设置为ok)

传参：jobId （必须）

作用：将作业的状态设置为OK

### (get)/run/job/{jobId}/statistics(获取作业的统计信息)

传参：jobId （必须）

作用：获取作业的统计信息，如开始时间之类

### (get)/run/job/{jobId}/status(获取作业的状态)

传参：jobId （必须）

作用：获取作业的状态

### (post)/run/job/{jobId}/undelete(恢复删除作业的标记)

传参：jobId （必须）

作用：恢复删除作业的标记

### (get)/run/job/{jobId}/waitingInfo(获取作业等待信息)

传参：jobId （必须）

作用：获取作业处于等待状态的原因

### (get)/run/jobs/status(获取作业状态)

传参：详见api

作用：获取与请求的搜索条件匹配的工作状态。

### (post)/run/order(筛选文件夹运行作业)

传参：data（非必须），json文件

作用：根据给定的过滤器从选定的文件夹运行作业

### (post)/run/resource/{server}(添加一个新的资源池)

传参：server （必须）

​			resource （必须）

作用：添加一个新的资源池

### (post)/run/resource/{server}/{name}(更新资源池)

传参：详见api

作用：更新资源池

### (delete)/run/resource/{server}/{name}(删除资源池)

传参：详见api

作用：删除资源池

### (get)/run/resources(获取资源记录)

传参：详见api

作用：获取匹配搜索的所有资源记录。

### (get)/run/services/sla(获取所有 SLA 活动服务)

传参：无

作用：获取所有 SLA 活动服务

### (get)/run/status/{runId}(获取正在运行的作业的状态)

传参：runId （必须）

​			startIndex（非必须），从其开始的作业状态的索引。 返回结果

作用：获取使用 Run 服务启动的作业的运行状态。如jobid

### (get)/run/variables(返回变量值)

传参：详见api

作用：根据指定的搜索条件返回变量值。

### (post)/run/variables/{server}(创建变量或更新变量)

传参：详见api

作用：设置 json 输入中定义的变量值。 使用此 API 创建新变量或更新现有变量。

### (delete)/run/variables/{server}(删除变量)

传参：详见api

作用：从服务器中删除变量

### (get)/run/workloadpolicies(获取所有工作负载策略)

传参：state(非必须)

作用：获取所有工作负载策略。

### (post)/run/workloadpolicies(天剑工作负载策略)

传参：workloadpoliciesfile （必须）

作用：将工作负载策略从 json 定义文件添加到 Control-M

### (get)/run/workloadpolicies/detailed(获取工作负载详情)

传参：name（非必须）

作用：获取与请求的搜索条件匹配的完整工作负载策略数据

### (post)/run/workloadpolicy/{policy}/activate(激活工作负载策略)

传参：详见api

作用：激活工作负载策略

### (post)/run/workloadpolicy/{policy}/deactivate(停用工作负载策略)

传参：详见api

作用：停用工作负载策略

### (delete)/run/workloadpolicy/{workloadpolicyName}(删除工作负载策略)

传参：详见api

作用：删除工作负载策略



## config(管理 Control-M 配置和环境权限)

## archive(Control-M 归档操作)

### (get)/archive/{jobId}/log（获取作业日志）

传参：jobId （必须）

​			runNo （必须），多次执行的执行次数

作用：通过唯一的作业键获取作业日志

### (get)/archive/{jobId}/output（获取作业的输出）

传参：jobId （必须）

​			runNo （必须），多次执行的执行次数

作用：通过唯一的作业键获取作业输出

### (get)/archive/search（搜寻作业）

传参：详见api

作用：获取所有符合搜索条件的 Control-M 归档作业

## provision(在当前帐户上安装 大数据 代理)

## reporting(生成 Control-M 报告)

# Control-m github

## 101-create-first-job-flow

创建第一个job案例，json案例

## 101-running-file-transfer-and-database-query-job-flow

运行文件传输和数据库查询作业流程，json和sql案例

## 101-running-hadoop-spark-job-flow

创建第一个Hadoop案例

## 101-running-script-command-job-flow

运行脚本、程序和命令作业，作业类型

## 102-automate-code-deployment

如何自动化代码部署

## 102-build-docker-containers-for-automation-api

如何使用预安装和预配置的自动化 API 构建容器

## 102-build-docker-containers-for-batch-application

用于批处理应用程序的 Docker 容器

## 102-on-boarding-new-application-group

加入新的应用程序组

## 103-test-automation-JUnit-workflow-examples

如何使用 JUnit 验证 control-m 工作流运行

## 104-push-jobs-script-from-DEV-to-PROD

使用自动化 API 将作业从 DEV 推送到 PROD

## 201-automate-corrective-flow

自动运行不同的作业来修复当前作业失败导致的问题

## 201-call-rest-api-using-curl

如何在 linux bash 脚本中使用 curl 调用自动化 api REST 调用,包含不同 api 调用的示例

## 201-call-rest-api-using-node-axios

使用node-axios调用rest api

## 201-call-rest-api-using-powershell

使用 Power Shell Invoke-RestMethod 调用 Control-M 自动化 API 的示例

## 201-call-rest-api-using-python

如何在 Python 中对自动化 API 进行 REST 调用

# bmc官方文档

https://docs.bmc.com/docs/automation-api/monthly/

## What's new in this version（版本新功能）

​	简介：介绍了此版本的新功能，如api的变化。

​				介绍了版本的变化

​				介绍了更正的问题

## Installation（安装CTM）

简介：讨论安装和设置 Control-M 自动化 API 必须执行的任务

​			包括： Control-M 自动化 API 组件及其要求、下载和安装或升级 Control-M REST API、安装 Control-M 自动化 						CLI等

## Tutorials（教程）



### Tutorials - Setting up the prerequisites（设置条件，如环境，登录验证）

简介：获得对 Control-M 自动化 API 的访问权限

​			安装 Control-M 自动化 CLI

​			设置 Control-M 环境

​			 通过登录会话验证设置

### Tutorial - Creating your first job flow（创建第一个作业流程）

简介：bulid验证Control-M 的代码

​			run运行源代码

​			*使用runId*检查作业状态

### Tutorial - Automating code deployment（自动化代码部署及检索作业）

简介：设置 Control-M 环境

​			部署到 ciEnvironment

​			使用部署描述符将作业从 ciEnvironment 检索回开发环境

​			(ctm deploy jobs::get -s "server=*&folder=*" -e ciEnvironment > ciEnvironmentJobs.json)

​			自动化部署

### Tutorial - Running applications and programs in your environment（运行不同的作业）

简介：运行脚本和命令作业流

​			运行文件传输和数据库查询作业流程		

​			运行 Hadoop-Spark 作业流	

### Tutorial - Building a docker container for batch applications（为批处理应用程序构建 docker 容器）

简介： 构建容器映像

​			 运行容器实例 

​			在 docker 容器中运行一个简单的作业流程

### Tutorial - Defining authorizations for Control-M roles and users（为 Control-M 角色和用户定义授权）

简介：完成为 Control-M 定义新角色和用户以及控制他们对 Control-M 资源的授权的过程。

​			在本例中，我们将创建一个将 Hadoop 开发人员分组在一起的角色，并将用户分配给该角色。

## Code Reference（代码参考）



### Folder（文件夹的相关参数及操作）

简介：普通文件夹：

​						**文件夹的默认类型**（与简单文件夹相反）使您能够配置各种设置，例如**日程安排、事件管理、添加资源或					在文件夹级别添加通知**。

​						文件夹级定义由文件夹内的作业或子文件夹**继承**。

​						例如，您可以在文件夹级别指定计划标准，而不是在文件夹中定义每个作业的标准。文件夹中的所有作业都									将采用文件夹的规则。这减少了代码中的作业定义。

​			子文件夹：

​					子文件夹是包含在另一个（父）文件夹或子**文件夹中的文件夹**。子文件夹可以包含一组作业或下一级子文件					夹，也**可以包含一个流**。子文件夹提供了常规文件夹提供的许多（但不是全部）功能。				

​			简单文件夹：

​							简单文件夹是**作业的容器**。简单文件夹不启用文件夹级别的作业定义配置。

​			FLOW：

​							*Flow*对象类型允许您定义文件夹和子文件夹中作业之间的**顺序依赖**关系。作业必须成功结束，流程中的下					一个作业才能运行。

### Job Properties（作业的属性及相关操作）

简介：type:作业类型

​			Application, SubApplication ：为一组相关的作业、文件夹或子文件夹提供一个通用的描述性称

​			Comment：允许您在对象上写评论。评论不会上传到 Control-M。

​			When：使您能够定义作业、文件夹和子文件夹的计划参数，包括使用日历的选项。

​			Events：事件可以由 Control-M 生成，也可以触发作业。事件由名称和日期定义。您可以通过 API 调用在 Control-							M 中添加或删除事件

​			If：当满足与作业相关的条件（例如，作业以特定状态结束或作业多次失败）时，*if语句会触发一个或多个操作。*

​			If Actions：*响应满足的If*语句，可以触发以下操作

​			Action:CaptureOutput：CaptureOutput 操作使您能够搜索作业输出并将作业输出中的文本捕获到变量中

​			...作业通知、运行等一系列操作

​		Resources：允许您在作业上设置池（以前称为*定量资源*或*信号量*），以控制对其他作业同时共享的资源的访问						

### Job types（作业类型）

简介：提供有关您可以定义的可用作业类型以及用于定义每种作业类型的参数的详细信息

### Calendars（日历）

简介：日历是一组计划标准，您可以将其应用于多个作业，而不必在每个单独的作业中定义计划标准。

​			提供有关您可以定义的可用日历类型以及您在日历定义中使用的参数的详细信息

### Connection Profiles（连接配置文件）

简介：连接配置文件用于定义特定应用程序的访问方法和安全凭证。它们可以被多个作业引用。为此，您必须在运行相关			作业之前部署连接配置文件定义

### Site Standards（站点标准）

简介：站点标准是使您能够通过对特定作业参数实施限制来控制 Control-M 中的作业定义的规则。站点标准应用于文件夹			级别，并应用于文件夹中的子文件夹和作业。 

### Site Standard Policies（站点标准策略）

简介：站点标准策略使您能够对多个文件夹实施站点标准。您可以按文件夹名称和服务器过滤策略的应用位置

### Secrets in Code（隐藏密码字段）

简介： 当您不想在源中公开机密信息（例如，连接配置文件中的密码字段）时，可以在 JSON 代码中使用 *Secret对象。*

### Defaults（json代码中设置默认值）

简介：JSON 代码中的 Defaults 对象允许您一次为所有对象定义默认参数值。

​			使用 *When* 参数定义调度条件。这会将*所有*作业配置为根据相同的调度标准运行。请注意，如果您还在作业级别设

​			置了特定值，则作业级别值将覆盖全局级别*默认值* 部分中的值



## Services（接口服务）



### Build service（编译文件，验证是否有效）

简介：允许您编译作业、文件夹或日历的定义，并验证它们对您的 Control-M 环境是否有效。Control-M 验证包括基本的 			Control-M 规则，例如字段长度、允许的字符和必填字段。Build 还将检查 JSON 是否有效。

### Deploy service(部署服务，文件管理)

简介：部署服务允许您将作业和配置定义传输到 Control-M。部署作业后，Control-M 将根据其调度标准和依赖关系对其			进行调度。部署会覆盖任何现有的同名定义。

​			文件夹、作业、日历、配置文件、站点标准的获取和删除。	

### Run service（运行服务，作业管理）

简介：*运行服务*使您 能够**运行作业并跟踪其状态**，以及管理作业使用的几种其他类型的对象。

​			作业运行状态的获取、统计、输出。

​			作业挂起、删除（实例）、立即执行、获取、修改、运行、释放等。

​			资源管理、事件管理、工作负载管理、服务管理、变量管理、告警管理等

### Package service(返回zip存档)

简介：从 .json 和 .xml定义文件的目录创建一个包。它返回一个 .zip 存档。这个包可以由这些各自的服务部署、运行或构			建。

​			注意：此功能仅通过 CLI 支持，不能通过 REST API 命令调用。

### Config service（配置服务权限管理）

简介：配置服务允许您配置 Control-M 环境

​			配置服务器、配置授权、配置作业归档、配置文件传输、配置安全

### Provision service（访问代理）

简介：Provision 服务允许您访问代理和服务器的以下设置过程的完整周期

​			向代理部署应用程序插件或集成插件、将某些插件部署到现有的 Agent、作为新服务器或通过将现有 Control-			M/Server 从一台机器转移到另一台机器

### Reporting service（生成报告）

简介：报告服务使您能够生成通过 Control-M 报告设置的报告。您可以同步或异步生成报告。

### Archive service（存档服务）

简介：归档服务使您能够搜索通过 Control-M 工作负载归档插件归档在工作负载归档服务器中的工作数据，以及获取单个			工作的工作输出和工作日志。此功能在具有 Control-M 9.0.20 或更高版本的环境中提供。

### Environment service（环境管理，账号密码等）

简介：*Environment*服务使您能够管理环境，包括定义和选择要使用的 Control-M 环境。环境是 *端点*、 *用户名*和 *密码*的组			合

​			环境保存在*env.json*文件中，该文件位于主用户的 .ctm 文件夹下，仅对登录用户具有读/写权限。

​			不得加密*env.json*文件中的敏感信息，例如密码和令牌。加载文件时，此敏感信息会自动加密。

### Session service（会话服务，登录登出，密码更新）

简介：Session 服务允许您登录和注销 Control-M 并接收可以在后续请求中重复使用的令牌。此外，会话服务允许用户更			改自己的密码。

### Authentication service（认证服务，token令牌）

简介：身份验证服务使您能够管理用于运行 API 命令的身份验证令牌。创建、更新、删除、获取token

## Deploy Descriptor（部署描述符，测试生产环境的迁移）

简介：Control-M 自动化 API 使您能够在构建、部署或**运行 JSON 文件之前**使用 Deploy Descriptor 以 JSON 格式**更改作业			定义属性**。支持的更改包括在 JSON 文件中添加、删除或修改属性或对象。

​			使用部署描述符使您能够**跨不同环境**（例如，在开发、测试或生产之间）**简化代码**。由于每个 Control-M 环境都			有不同的属性，部署描述符使您能够以编程方式操作这些属性。