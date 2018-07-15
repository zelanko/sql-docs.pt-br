---
title: Agendando tarefas administrativas automáticas no SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- scheduling administrative tasks [SMO]
- SQL Server Agent [SMO]
- automatic administrative SMO tasks
ms.assetid: 900242ad-d6a2-48e9-8a1b-f0eea4413c16
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ad4b0fa53b7a15d9ff8118336d0ec0b9d31a4b56
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256048"
---
# <a name="scheduling-automatic-administrative-tasks-in-sql-server-agent"></a>Agendando tarefas administrativas automáticas no SQL Server Agent
  No SMO, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent é representado pelos seguintes objetos:  
  
-   O objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobServer> tem três coleções de trabalhos, alertas e operadores.  
  
-   O objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.OperatorCollection> representa uma lista de pagers, endereços de email e operadores net send que podem ser notificados sobre eventos automaticamente pelo Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent.  
  
-   O objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.AlertCollection> representa uma lista de circunstâncias, tais como eventos do sistema ou condições de desempenho que são monitoradas pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   O objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobCollection> é um pouco mais complexo. Ele representa uma lista de tarefas com várias etapas que são executadas em agendas especificadas. As etapas e as informações da agenda são armazenadas nos objetos <xref:Microsoft.SqlServer.Management.Smo.Agent.JobStep> e <xref:Microsoft.SqlServer.Management.Smo.Agent.JobSchedule>.  
  
 Os objetos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent estão no namespace <xref:Microsoft.SqlServer.Management.Smo.Agent>.  
  
## <a name="examples"></a>Exemplos  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto do Visual Basic SMO no Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) ou [criar um Visual C&#35; projeto de SMO no Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
1.  Para programas que usam o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent, inclua a instrução `Imports` para qualificar o namespace do Agent. Insira a instrução após outras instruções `Imports`, antes de qualquer declaração no aplicativo, como:  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Agent`  
  
## <a name="creating-a-job-with-steps-and-a-schedule-in-visual-basic"></a>Criando um trabalho com etapas e uma agenda no Visual Basic  
 Este exemplo de código cria um trabalho com etapas e uma agenda e informa um operador.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBAgent1](SMO How to#SMO_VBAgent1)]  -->  
  
## <a name="creating-a-job-with-steps-and-a-schedule-in-visual-c"></a>Criando um trabalho com etapas e uma agenda no Visual C#  
 Este exemplo de código cria um trabalho com etapas e uma agenda e informa um operador.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.  
            Server srv = new Server();  
  
            //Define an Operator object variable by supplying the Agent (parent JobServer object) and the name in the constructor.   
            Operator op = new Operator(srv.JobServer, "Test_Operator");  
  
            //Set the Net send address.   
            op.NetSendAddress = "Network1_PC";  
  
            //Create the operator on the instance of SQL Server Agent.   
            op.Create();  
  
            //Define a Job object variable by supplying the Agent and the name arguments in the constructor and setting properties.   
            Job jb = new Job(srv.JobServer, "Test_Job");  
  
            //Specify which operator to inform and the completion action.   
            jb.OperatorToNetSend = "Test_Operator";  
            jb.NetSendLevel = CompletionAction.Always;  
  
            //Create the job on the instance of SQL Server Agent.   
            jb.Create();  
  
            //Define a JobStep object variable by supplying the parent job and name arguments in the constructor.   
            JobStep jbstp = new JobStep(jb, "Test_Job_Step");  
            jbstp.Command = "Test_StoredProc";  
            jbstp.OnSuccessAction = StepCompletionAction.QuitWithSuccess;  
            jbstp.OnFailAction = StepCompletionAction.QuitWithFailure;  
  
            //Create the job step on the instance of SQL Agent.   
            jbstp.Create();  
  
            //Define a JobSchedule object variable by supplying the parent job and name arguments in the constructor.   
  
            JobSchedule jbsch = new JobSchedule(jb, "Test_Job_Schedule");  
  
            //Set properties to define the schedule frequency, and duration.   
            jbsch.FrequencyTypes = FrequencyTypes.Daily;  
            jbsch.FrequencySubDayTypes = FrequencySubDayTypes.Minute;  
            jbsch.FrequencySubDayInterval = 30;  
            TimeSpan ts1 = new TimeSpan(9, 0, 0);  
            jbsch.ActiveStartTimeOfDay = ts1;  
  
            TimeSpan ts2 = new TimeSpan(17, 0, 0);  
            jbsch.ActiveEndTimeOfDay = ts2;  
            jbsch.FrequencyInterval = 1;  
  
            System.DateTime d = new System.DateTime(2003, 1, 1);  
            jbsch.ActiveStartDate = d;  
  
            //Create the job schedule on the instance of SQL Agent.   
            jbsch.Create();  
        }  
```  
  
## <a name="creating-a-job-with-steps-and-a-schedule-in-powershell"></a>Criando um trabalho com etapas e uma agenda no PowerShell  
 Este exemplo de código cria um trabalho com etapas e uma agenda e informa um operador.  
  
```  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define an Operator object variable by supplying the Agent (parent JobServer object) and the name in the constructor.  
$op = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Agent.Operator -argumentlist $srv.JobServer, "Test_Operator"  
  
#Set the Net send address.  
$op.NetSendAddress = "Network1_PC"  
  
#Create the operator on the instance of SQL Agent.  
$op.Create()  
  
#Define a Job object variable by supplying the Agent and the name arguments in the constructor and setting properties.   
$jb = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Agent.Job -argumentlist $srv.JobServer, "Test_Job"   
  
#Specify which operator to inform and the completion action.   
$jb.OperatorToNetSend = "Test_Operator";   
$jb.NetSendLevel = [Microsoft.SqlServer.Management.SMO.Agent.CompletionAction]::Always  
  
#Create the job on the instance of SQL Server Agent.   
$jb.Create()  
  
#Define a JobStep object variable by supplying the parent job and name arguments in the constructor.   
$jbstp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Agent.JobStep -argumentlist $jb, "Test_Job_Step"   
$jbstp.Command = "Test_StoredProc";   
$jbstp.OnSuccessAction = [Microsoft.SqlServer.Management.SMO.Agent.StepCompletionAction]::QuitWithSuccess;   
$jbstp.OnFailAction =[Microsoft.SqlServer.Management.SMO.Agent.StepCompletionAction]::QuitWithFailure;   
  
#Create the job step on the instance of SQL Agent.   
$jbstp.Create();   
  
#Define a JobSchedule object variable by supplying the parent job and name arguments in the constructor.   
$jbsch =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Agent.JobSchedule -argumentlist $jb, "Test_Job_Schedule"   
  
#Set properties to define the schedule frequency, and duration.   
$jbsch.FrequencyTypes =  [Microsoft.SqlServer.Management.SMO.Agent.FrequencyTypes]::Daily  
  
$jbsch.FrequencySubDayTypes = [Microsoft.SqlServer.Management.SMO.Agent.FrequencySubDayTypes]::Minute  
$jbsch.FrequencySubDayInterval = 30  
$ts1 =  New-Object -TypeName TimeSpan -argumentlist 9, 0, 0  
$jbsch.ActiveStartTimeOfDay = $ts1  
$ts2 = New-Object -TypeName TimeSpan -argumentlist 17, 0, 0  
$jbsch.ActiveEndTimeOfDay = $ts2  
$jbsch.FrequencyInterval = 1  
$jbsch.ActiveStartDate = "01/01/2003"  
  
#Create the job schedule on the instance of SQL Agent.   
$jbsch.Create();  
```  
  
## <a name="creating-an-alert-in-visual-basic"></a>Criando um alerta no Visual Basic  
 Este exemplo de código cria um alerta que é disparado por uma condição de desempenho. A condição deve ser fornecida em um formato específico:  
  
 **ObjectName | CounterName | Instância | ComparisionOp | CompValue**  
  
 É necessário um operador para a notificação de alerta. O tipo <xref:Microsoft.SqlServer.Management.Smo.Agent.Operator> exige colchetes porque o `operator` é uma palavra-chave do Visual Basic.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBAgent3](SMO How to#SMO_VBAgent3)]  -->  
  
## <a name="creating-an-alert-in-visual-c"></a>Criando um alerta no Visual C#  
 Este exemplo de código cria um alerta que é disparado por uma condição de desempenho. A condição deve ser fornecida em um formato específico:  
  
 **ObjectName | CounterName | Instância | ComparisionOp | CompValue**  
  
 É necessário um operador para a notificação de alerta. O tipo <xref:Microsoft.SqlServer.Management.Smo.Agent.Operator> exige colchetes porque o `operator` é uma palavra-chave do [!INCLUDE[csprcs](../../../includes/csprcs-md.md)].  
  
```  
{  
             //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
  
            //Define an Alert object variable by supplying the SQL Server Agent and the name arguments in the constructor.   
            Alert al = new Alert(srv.JobServer, "Test_Alert");  
  
            //Specify the performance condition string to define the alert.   
            al.PerformanceCondition = "SQLServer:General Statistics|User Connections||>|3";  
  
            //Create the alert on the SQL Agent.   
            al.Create();  
  
            //Define an Operator object variable by supplying the SQL Server Agent and the name arguments in the constructor.   
  
            Operator op = new Operator(srv.JobServer, "Test_Operator");  
            //Set the net send address.   
            op.NetSendAddress = "NetworkPC";  
            //Create the operator on the SQL Agent.   
            op.Create();  
            //Run the AddNotification method to specify the operator is notified when the alert is raised.   
            al.AddNotification("Test_Operator", NotifyMethods.NetSend);  
        }  
```  
  
## <a name="creating-an-alert-in-powershell"></a>Criando um alerta no PowerShell  
 Este exemplo de código cria um alerta que é disparado por uma condição de desempenho. A condição deve ser fornecida em um formato específico:  
  
 **ObjectName | CounterName | Instância | ComparisionOp | CompValue**  
  
 É necessário um operador para a notificação de alerta. O tipo <xref:Microsoft.SqlServer.Management.Smo.Agent.Operator> exige colchetes porque o `operator` é uma palavra-chave do [!INCLUDE[csprcs](../../../includes/csprcs-md.md)].  
  
```  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define an Alert object variable by supplying the SQL Agent and the name arguments in the constructor.  
$al = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Agent.Alert -argumentlist $srv.JobServer, "Test_Alert"  
  
#Specify the performance condition string to define the alert.  
$al.PerformanceCondition = "SQLServer:General Statistics|User Connections||>|3"  
  
#Create the alert on the SQL Agent.  
$al.Create()  
  
#Define an Operator object variable by supplying the Agent (parent JobServer object) and the name in the constructor.  
$op = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Agent.Operator -argumentlist $srv.JobServer, "Test_Operator"  
  
#Set the Net send address.  
$op.NetSendAddress = "Network1_PC"  
  
#Create the operator on the instance of SQL Agent.  
$op.Create()  
  
#Run the AddNotification method to specify the operator is notified when the alert is raised.  
$ns = [Microsoft.SqlServer.Management.SMO.Agent.NotifyMethods]::NetSend  
$al.AddNotification("Test_Operator", $ns)  
  
#Drop the alert and the operator  
$al.Drop()  
$op.Drop()  
```  
  
## <a name="allowing-user-access-to-subsystem-by-using-a-proxy-account-in-visual-basic"></a>Permitindo o acesso de usuários ao subsistema usando uma conta proxy no Visual Basic  
 Este exemplo de código mostra como permitir o acesso de um usuário a um subsistema especificado usando o método <xref:Microsoft.SqlServer.Management.Smo.Agent.ProxyAccount.AddSubSystem%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.ProxyAccount>.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBAgent2](SMO How to#SMO_VBAgent2)]  -->  
  
## <a name="allowing-user-access-to-subsystem-by-using-a-proxy-account-in-visual-c"></a>Permitindo o acesso de usuários ao subsistema usando uma conta proxy no Visual C#  
 Este exemplo de código mostra como permitir o acesso de um usuário a um subsistema especificado usando o método <xref:Microsoft.SqlServer.Management.Smo.Agent.ProxyAccount.AddSubSystem%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.ProxyAccount>.  
  
```  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
//Declare a JobServer object variable and reference the SQL Server Agent.   
JobServer js = default(JobServer);   
js = srv.JobServer;   
//Define a Credential object variable by supplying the parent server and name arguments in the constructor.   
Credential c = default(Credential);   
c = new Credential(srv, "Proxy_accnt");   
//Set the identity to a valid login represented by the vIdentity string variable.   
//The sub system will run under this login.   
c.Identity = vIdentity;   
//Create the credential on the instance of SQL Server.   
c.Create();   
//Define a ProxyAccount object variable by supplying the SQL Server Agent, the name, the credential, the description arguments in the constructor.   
ProxyAccount pa = default(ProxyAccount);   
pa = new ProxyAccount(js, "Test_proxy", "Proxy_accnt", true, "Proxy account for users to run job steps in command shell.");   
//Create the proxy account on the SQL Agent.   
pa.Create();   
//Add the login, represented by the vLogin string variable, to the proxy account.   
pa.AddLogin(vLogin);   
//Add the CmdExec subsytem to the proxy account.   
pa.AddSubSystem(AgentSubSystem.CmdExec);   
}   
//Now users logged on as vLogin can run CmdExec job steps with the specified credentials.   
```  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Agent](../../../ssms/agent/sql-server-agent.md)   
 [Implementar trabalhos](../../../ssms/agent/implement-jobs.md)  
  
  
