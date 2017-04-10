---
title: "Tarefa Transferir Procedimentos Armazenados Mestres | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.transfermasterspstask.f1"
helpviewer_keywords: 
  - "Tarefa Transferir Procedimentos Armazenados Mestre [Integration Services]"
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# Tarefa Transferir Procedimentos Armazenados Mestres
  A tarefa Transferir Procedimentos Armazenados Mestres transfere um ou mais procedimentos armazenados definidos pelo usuário entre bancos de dados **mestre** em instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para transferir um procedimento armazenado do banco de dados **mestre**, o proprietário do procedimento deve ser dbo.  
  
 A tarefa Transferir Procedimentos Armazenados Mestres pode ser configurada para transferir todos os procedimentos armazenados ou apenas procedimentos armazenados específicos. Essa tarefa não copia procedimentos armazenados do sistema.  
  
 Os procedimentos armazenados mestres a serem transferidos podem já existir no destino. A tarefa Transferir Procedimentos Armazenados Mestres pode ser configurada para lidar com procedimentos já existentes armazenados das seguintes maneiras:  
  
-   Substituir procedimentos armazenados existentes.  
  
-   Interromper a tarefa quando existirem procedimentos armazenados duplicados.  
  
-   Ignorar procedimentos armazenados duplicados.  
  
 Em tempo de execução, a tarefa Transferir Procedimentos Armazenados Mestres conecta-se aos servidores de origem e de destino usando dois gerenciadores de conexões SMO. Os gerenciadores de conexões SMO são configurados separadamente a partir da tarefa Transferir Procedimentos Armazenados Mestres e depois referenciados na tarefa Transferir Procedimentos Armazenados Mestres. Os gerenciadores de conexões SMO especificam o servidor e o modo de autenticação a serem usados ao acessar o servidor. Para obter mais informações, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
## Transferindo procedimentos armazenados entre instâncias do SQL Server  
 A tarefa Transferir Procedimentos Armazenados Mestres dá suporte a uma origem e a um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Eventos  
 A tarefa gera um evento de informações que informa o número de procedimentos armazenados transferidos e um evento de aviso quando um procedimento armazenado é substituído.  
  
 A tarefa Transferir Procedimentos Armazenados Mestres não informa o progresso incremental da transferência de logon; ela apenas informa 0% e 100% de conclusão.  
  
## Valor de execução  
 O valor de execução definido na propriedade **ExecutionValue** da tarefa retorna o número de procedimentos armazenados transferidos. Atribuindo uma variável definida pelo usuário à propriedade **ExecValueVariable** da tarefa Transferir Procedimentos Armazenados Mestres, as informações sobre a transferência de procedimentos armazenados podem ser disponibilizadas para outros objetos do pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](../Topic/Use%20Variables%20in%20Packages.md).  
  
## Entradas de log  
 A tarefa Transferir Procedimentos Armazenados Mestres inclui as seguintes entradas de log personalizadas:  
  
-   TransferStoredProceduresTaskStartTransferringObjects Essa entrada de log informa que a transferência foi iniciada. A entrada do log contém a hora de início.  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects Essa entrada de log informa que a transferência foi concluída. A entrada do log contém a hora de término.  
  
 Além disso, uma entrada de log para o evento **OnInformation** informa o número de procedimentos armazenados que foram transferidos e uma entrada de log para o evento **OnWarning** é gravada para cada procedimento armazenado no destino que é substituído.  
  
## Segurança e permissões  
 O usuário deve ter permissão para exibir a lista do procedimento armazenado no banco de dados **mestre** na origem e deve ser um membro da função de servidor sysadmin ou ter permissão para procedimentos armazenados criados no banco de dados **mestre** no servidor de destino.  
  
## Configuração da tarefa Transferir Procedimentos Armazenados Mestres  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos tópicos a seguir:  
  
-   [Editor da Tarefa Transferir Procedimentos Armazenados Mestres &#40;página Geral&#41;](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-general-page.md)  
  
-   [Editor da Tarefa Transferir Procedimentos Armazenados Mestres &#40;Página Procedimentos Armazenados&#41;](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-stored-procedures-page.md)  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### Configurando a tarefa Transferir Procedimentos Armazenados Mestres programaticamente  
  
## Tarefas relacionadas  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Consulte também  
 [Tarefa Transferir Objetos do SQL Server](../../integration-services/control-flow/transfer-sql-server-objects-task.md)   
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  