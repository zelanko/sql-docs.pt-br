---
title: Tarefa Transferir Trabalhos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferjobstask.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03913242246fcdaf11e9272e827cd8e06951a108
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829892"
---
# <a name="transfer-jobs-task"></a>Tarefa Transferir Trabalhos
  A tarefa Transferir Trabalhos transfere um ou mais trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A tarefa Transferir Trabalhos pode ser configurada para transferir todos os trabalhos ou só os trabalhos especificados. Você também pode indicar se os trabalhos transferidos são habilitados no destino.  
  
 Os trabalhos a ser transferidos já podem existir no destino. A tarefa Transferir Trabalhos pode ser configurada para manipular os trabalhos existentes dos modos a seguir:  
  
-   Substituir os trabalhos existentes.  
  
-   Interromper a tarefa quando houver trabalhos duplicados.  
  
-   Ignorar trabalhos duplicados.  
  
 No tempo de execução, a tarefa Transferir Trabalhos conecta-se aos servidores de origem e de destino usando um ou dois gerenciadores de conexões SMO. O gerenciador de conexões SMO é configurado separadamente da tarefa Transferir Trabalhos e depois é referenciado na tarefa Transferir Trabalhos. O gerenciador de conexões SMO especifica o servidor e o modo de autenticação a ser usado ao acessar o servidor. Para obter mais informações, consulte [SMO Connection Manager](../connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>Transferindo trabalhos entre instâncias do SQL Server  
 A tarefa Transferir Trabalhos dá suporte a uma origem e a um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Não há nenhuma restrição quanto à versão a ser usada como origem ou destino.  
  
## <a name="events"></a>Eventos  
 A tarefa Transferir Trabalhos gera um evento de informação com o número de trabalhos transferidos e um evento de aviso quando um trabalho é substituído. A tarefa não informa o progresso incremental da transferência de trabalhos; informa só 0% e 100% concluídos.  
  
## <a name="execution-value"></a>Valor de execução  
 O valor de execução, definido na propriedade `ExecutionValue` da tarefa retorna o número de trabalhos que são transferidos. Ao atribuir uma variável definida pelo usuário à propriedade `ExecValueVariable` da tarefa Transferir Trabalhos, informações sobre a transferência de trabalhos podem se tornar disponíveis a outros objetos no pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Usar variáveis em pacotes](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Entradas de log  
 A tarefa Transferir Trabalhos inclui as seguintes entradas de log personalizadas:  
  
-   TransferJobsTaskStarTransferringObjects   Essa entrada de log informa que a transferência foi iniciada. A entrada do log contém a hora de início.  
  
-   TransferJobsTaskFinishedTransferringObjects    Essa entrada de log informa que a transferência foi concluída. A entrada do log contém a hora de término.  
  
 Além disso, uma entrada de log para o evento `OnInformation` informa o número de trabalhos que foram transferidos e uma entrada de log para o evento `OnWarning` é gravada para cada trabalho no destino que for substituído.  
  
## <a name="security-and-permissions"></a>Segurança e permissões  
 Para transferir trabalhos, o usuário deve ser membro da função de servidor fixa sysadmin ou de uma das funções de banco de dados fixas Agent do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados msdb em ambas as instâncias de origem e de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>Configuração da tarefa Transferir Trabalhos  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos tópicos a seguir:  
  
-   [Editor da Tarefa Transferir Trabalhos &#40;Página Geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor da Tarefa Transferir Trabalhos &#40;página Trabalhos&#41;](../transfer-jobs-task-editor-jobs-page.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Integration Services](integration-services-tasks.md)   
 [Fluxo de Controle](control-flow.md)  
  
  
