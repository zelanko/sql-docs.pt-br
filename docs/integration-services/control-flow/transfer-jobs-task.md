---
title: Tarefa Transferir Trabalhos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferjobstask.f1
- sql13.dts.designer.transferjobstask.general.f1
- sql13.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e5747cc9fbac122e9bca7fa6a127fd74a4ec47ff
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916102"
---
# <a name="transfer-jobs-task"></a>Tarefa Transferir Trabalhos

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  A tarefa Transferir Trabalhos transfere um ou mais trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A tarefa Transferir Trabalhos pode ser configurada para transferir todos os trabalhos ou só os trabalhos especificados. Você também pode indicar se os trabalhos transferidos são habilitados no destino.  
  
 Os trabalhos a ser transferidos já podem existir no destino. A tarefa Transferir Trabalhos pode ser configurada para manipular os trabalhos existentes dos modos a seguir:  
  
-   Substituir os trabalhos existentes.  
  
-   Interromper a tarefa quando houver trabalhos duplicados.  
  
-   Ignorar trabalhos duplicados.  
  
 No tempo de execução, a tarefa Transferir Trabalhos conecta-se aos servidores de origem e de destino usando um ou dois gerenciadores de conexões SMO. O gerenciador de conexões SMO é configurado separadamente da tarefa Transferir Trabalhos e depois é referenciado na tarefa Transferir Trabalhos. O gerenciador de conexões SMO especifica o servidor e o modo de autenticação a ser usado ao acessar o servidor. Para obter mais informações, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>Transferindo trabalhos entre instâncias do SQL Server  
 A tarefa Transferir Trabalhos dá suporte a uma origem e a um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Não há nenhuma restrição quanto à versão a ser usada como origem ou destino.  
  
## <a name="events"></a>Eventos  
 A tarefa Transferir Trabalhos gera um evento de informação com o número de trabalhos transferidos e um evento de aviso quando um trabalho é substituído. A tarefa não informa o progresso incremental da transferência de trabalhos; informa só 0% e 100% concluídos.  
  
## <a name="execution-value"></a>Valor de execução  
 O valor de execução, definido na propriedade **ExecutionValue** da tarefa retorna o número de trabalhos que são transferidos. Ao atribuir uma variável definida pelo usuário à propriedade **ExecValueVariable** da tarefa Transferir Trabalhos, informações sobre a transferência de trabalhos podem se tornar disponíveis a outros objetos no pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Entradas de log  
 A tarefa Transferir Trabalhos inclui as seguintes entradas de log personalizadas:  
  
-   TransferJobsTaskStarTransferringObjects   Essa entrada de log informa que a transferência foi iniciada. A entrada do log contém a hora de início.  
  
-   TransferJobsTaskFinishedTransferringObjects    Essa entrada de log informa que a transferência foi concluída. A entrada do log contém a hora de término.  
  
 Além disso, uma entrada de log para o evento **OnInformation** informa o número de trabalhos que foram transferidos e uma entrada de log para o evento **OnWarning** é gravada para cada trabalho no destino que for substituído.  
  
## <a name="security-and-permissions"></a>Segurança e permissões  
 Para transferir trabalhos, o usuário deve ser membro da função de servidor fixa sysadmin ou de uma das funções de banco de dados fixas Agent do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados msdb em ambas as instâncias de origem e de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>Configuração da tarefa Transferir Trabalhos  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-jobs-task-editor-general-page"></a>Editor da Tarefa Transferir Trabalhos (página Geral)
  Use a página **Geral** da caixa de diálogo do **Editor da Tarefa Transferir Trabalhos** para nomear e descrever a tarefa Transferir Trabalhos.  
  
> [!NOTE]  
>  Somente os membros da função de servidor fixa **sysadmin** ou uma das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no servidor de destino podem criar trabalhos com êxito. Para acessar trabalhos no servidor de origem, os usuários devem ser membros pelo menos da função de banco de dados fixa **SQLAgentUserRole** . Para obter mais informações sobre as funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e suas permissões, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
### <a name="options"></a>Opções  
 **Nome**  
 Digite um nome exclusivo para a tarefa Transferir Trabalhos. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Transferir Trabalhos.  
  
## <a name="transfer-jobs-task-editor-jobs-page"></a>Editor da Tarefa Transferir Trabalhos (página Trabalhos)
  Use a página **Trabalhos** da caixa de diálogo **Editor da Tarefa de Transferir Trabalhos** para especificar as propriedades para cópia de um ou mais trabalhos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent de uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra.  
  
> [!NOTE]  
>  Para acessar trabalhos no servidor de origem, é necessário que os usuários sejam membros pelo menos da função do banco de dados fixa **SQLAgentUserRole** no servidor. Para criar trabalhos no servidor de destino com êxito, é necessário que o usuário seja um membro da função de servidor fixa **sysadmin** ou uma das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações sobre as funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e suas permissões, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
### <a name="options"></a>Opções  
 **SourceConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<New connection...>** para criar uma conexão com o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<New connection...>** para criar uma conexão com o servidor de destino.  
  
 **TransferAllJobs**  
 Selecione se a tarefa deve copiar todas ou apenas os trabalhos de Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificados do servidor de origem para o servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Verdadeiro**|Copia todas as tarefas.|  
|**Falso**|Copia apenas os trabalhos especificados.|  
  
 **JobsList**  
 Clique no botão Procurar **(...)** para selecionar os trabalhos a serem copiados. Pelo menos um trabalho deve ser selecionado.  
  
> [!NOTE]  
>  Especifique a **SourceConnection** antes de selecionar trabalhos para copiar.  
  
 A opção **JobsList** não estará disponível quando **TransferAllJobs** for definido como **True**.  
  
 **IfObjectExists**  
 Selecione como a tarefa deve tratar trabalhos que tenham o mesmo nome já existente no servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**FailTask**|A tarefa irá falhar se já existirem trabalhos com o mesmo nome no servidor de destino.|  
|**Overwrite**|A tarefa irá substituir trabalhos de mesmo nome no servidor de destino.|  
|**Ignorar**|A tarefa irá ignorar os trabalhos de mesmo nome que existem no servidor de destino.|  
  
 **EnableJobsAtDestination**  
 Selecione se os trabalhos copiados para o servidor de destino devem ser habilitados.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Verdadeiro**|Habilita trabalhos no servidor de destino.|  
|**Falso**|Desabilita trabalhos no servidor de destino.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
