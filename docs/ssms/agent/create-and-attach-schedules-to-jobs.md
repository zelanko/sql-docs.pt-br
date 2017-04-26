---
title: Criar e anexar agendas a trabalhos | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server]
- scheduling jobs [SQL Server]
- jobs [SQL Server], scheduling
- CPU [SQL Server], idle conditions
- automatic job processing
- SQL Server Agent jobs, scheduling
- idle time [SQL Server]
ms.assetid: 079c2984-0052-4a37-a2b8-4ece56e6b6b5
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5c104e70fc7b2e7065f9aa43a16aac88707391ea
ms.lasthandoff: 04/11/2017

---
# <a name="create-and-attach-schedules-to-jobs"></a>Criar e anexar agendas para trabalhos
Agendar trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent significa definir as condições que fazem com que o trabalho comece a ser executado sem interação com o usuário. Você pode agendar um trabalho para execução automática criando uma nova agenda para ele ou anexando uma agenda existente para o trabalho.  
  
Há dois modos de criar um agenda:  
  
-   Crie a agenda enquanto estiver criando um trabalho.  
  
-   Crie a agenda no Pesquisador de Objetos.  
  
Após a criação de uma agenda, você pode anexá-la a vários objetos, mesmo que tenha sido criada para um determinado trabalho. Você também pode desanexar agendas de trabalhos.  
  
Uma agenda pode se basear na hora ou em um evento. Por exemplo, você pode agendar um trabalho para execução nos seguintes horários:  
  
-   Sempre que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent for iniciado.  
  
-   Sempre que a utilização de CPU do computador estiver em um nível definido como ocioso.  
  
-   Apenas uma vez, em data e horário específicos.  
  
-   Em uma agenda recorrente.  
  
Como alternativa às agendas de trabalho, também é possível criar um alerta que responda a um evento executando um trabalho.  
  
> [!NOTE]  
> Só uma instância do trabalho pode ser executada de cada vez. Se você tentar executar um trabalho manualmente enquanto ele estiver sendo executado como agendado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent recusará a solicitação.  
  
Para impedir a execução de um trabalho agendado, siga um destes procedimentos:  
  
-   Desabilite a agenda.  
  
-   Desabilite o trabalho.  
  
-   Desanexe a agenda do trabalho.  
  
-   Pare o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
-   Exclua a agenda.  
  
Se a agenda não estiver habilitada, o trabalho poderá ser executado em resposta a um alerta ou manualmente, por um usuário. Quando uma agenda de trabalho não é habilitada, todos os trabalhos agendados também ficam desabilitados.  
  
É necessário habilitar novamente explicitamente uma agenda que tenha sido desabilitada. Editar a agenda não a habilita novamente automaticamente.  
  
## <a name="scheduling-start-dates"></a>Agendando datas de início  
A data de início de uma agenda deve ser maior ou igual a 19900101.  
  
Quando você está anexando uma agenda a um trabalho, deve examinar a data de início que a agenda usa para executar o trabalho pela primeira vez. A data de início depende do dia e da hora em que você anexa a agenda ao trabalho. Por exemplo, você cria uma agenda executada de 15 em 15 dias, às segundas-feiras às 8:00. Se você criar um trabalho às 10h na segunda-feira, 3 de março de 2008, a data de início da agenda será Segunda-feira, 17 de março de 2008. Se você criar outro trabalho na terça-feira, 4 de março de 2008, a data de início da agenda será segunda-feira,10 de março de 2008.  
  
Você pode alterar a data de início de agenda após anexá-la a um trabalho.  
  
## <a name="cpu-idle-schedules"></a>Agendas de ociosidade de CPU  
Para maximizar os recursos da CPU, você pode definir uma condição de ociosidade de CPU para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent usa a configuração de condição de ociosidade de CPU para determinar o melhor momento para executar trabalhos. Por exemplo, você pode agendar um trabalho para recriar índices durante o tempo ocioso de CPU e períodos de produção lentos.  
  
Antes de definir trabalhos para execução durante o tempo ocioso de CPU, determine a carga na CPU durante o processamento normal. Para tanto, use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler_md.md)] ou o Monitor de Desempenho para monitorar o tráfego de servidor e coletar estatísticas. Assim, você poderá usar as informações recolhidas para definir a porcentagem e a duração do tempo ocioso de CPU.  
  
Defina a condição de ociosidade de CPU na forma de uma porcentagem abaixo da qual deve permanecer o uso de CPU por um tempo especificado. Em seguida, defina o intervalo de tempo. Quando o uso de CPU se encontrar abaixo da porcentagem especificada pelo intervalo de tempo especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent iniciará todos os trabalhos que têm uma agenda de tempo ocioso de CPU. Para obter mais informações sobre como usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler_md.md)] ou o Monitor de Desempenho para monitorar o uso de CPU, consulte [Monitoramento do uso de CPU](http://msdn.microsoft.com/en-us/2a02a3b6-07b2-4ad0-8a24-670414d19812).  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|||  
|-|-|  
|**Description**|**Tópico**|  
|Descreve como criar uma agenda para um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.|[Create a Schedule](../../ssms/agent/create-a-schedule.md)|  
|Descreve como agendar um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.|[Agendar um trabalho](../../ssms/agent/schedule-a-job.md)|  
|Explica como definir a condição de ociosidade de CPU para seu servidor.|[Definir o momento e a duração de ociosidade da CPU &amp;#40;SQL Server Management Studio&amp;#41;](../../ssms/agent/set-cpu-idle-time-and-duration-sql-server-management-studio.md)|  
  
## <a name="see-also"></a>Consulte também  
[sp_help_jobschedule](http://msdn.microsoft.com/en-us/2cded902-9272-4667-ac4b-a4f95a9f008e)  
[sysjobschedules](http://msdn.microsoft.com/en-us/ccdafec7-2a9b-4356-bffb-1caa3a12db59)  
  

