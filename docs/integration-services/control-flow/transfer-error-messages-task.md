---
title: "Transferência de mensagens de erro | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transfererrormessagestask.f1
helpviewer_keywords:
- Transfer Error Messages task [Integration Services]
ms.assetid: da702289-035a-4d14-bd74-04461fbfee1b
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3f13e3e6e22e2b4f3b74c80a249a098d93ad5b9f
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-error-messages-task"></a>Tarefa Transferir Mensagens de Erro
  A tarefa Transferir Mensagens de Erro transfere uma ou mais mensagens de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definidas pelo usuário entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mensagens definidas pelo usuário são mensagens com um identificador igual ou maior que 50000. Mensagens com identificador menor que 50000 são mensagens de erro do sistema e não podem ser transferidas usando-se a tarefa Transferir Mensagens de Erro.  
  
 A tarefa Transferir Mensagens de Erro pode ser configurada para transferir todas as mensagens de erro ou só as mensagens de erro especificadas. Mensagens de erro definidas pelo usuário podem estar disponíveis em vários idiomas diferentes e a tarefa pode ser configurada para só transferir mensagens em idiomas selecionados. Uma versão us_english da mensagem, que usa a página de código 1033, deve estar no servidor de destino para que você possa transferir versões em outro idioma da mensagem para esse servidor.  
  
 A tabela sysmessages no banco de dados mestre contém todas as mensagens de erro, tanto as de sistema como as definidas pelo usuário, que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa.  
  
 As mensagens definidas pelo usuário a serem transferidas já podem existir no destino. Uma mensagem de erro estará definida como mensagem de erro duplicada se o identificador e o idioma forem os mesmos. A tarefa Transferir Mensagens de Erro pode ser configurada para controlar mensagens de erro da seguinte maneira:  
  
-   Substituir mensagens de erro existentes.  
  
-   Interromper a tarefa quando houver mensagens duplicadas.  
  
-   Ignorar mensagens de erro duplicadas.  
  
 No tempo de execução, a tarefa Transferir Mensagens de Erro conecta-se aos servidores de origem e de destino usando um ou dois gerenciadores de conexões SMO. O gerenciador de conexões SMO é configurado separadamente da tarefa Transferir Mensagens de Erro e, depois, é consultado na tarefa Transferir Mensagens de Erro. O gerenciador de conexões SMO especifica o servidor e o modo de autenticação a ser usado ao acessar o servidor. Para obter mais informações, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 A tarefa Transferir Mensagens de Erro dá suporte a uma origem e a um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Não há nenhuma restrição quanto à versão a ser usada como origem ou destino.  
  
## <a name="events"></a>Eventos  
 A tarefa gera  um evento de informações que informa o número de mensagens de erro que foram transferidas.  
  
 A tarefa Transferir Mensagens de Erro não informa o progresso incremental da transferência de mensagem de erro; informa somente conclusão 0% e 100 %.  
  
## <a name="execution-value"></a>Valor de execução  
 O valor de execução, definido na propriedade **ExecutionValue** da tarefa retorna o número de mensagens de erro que foram transferidas. Ao atribuir uma variável definida pelo usuário à propriedade **ExecValueVariable** da tarefa Transferir Mensagem de Erro, as informações sobre a transferência de mensagem de erro podem se tornar disponíveis a outros objetos no pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Entradas de log  
 A tarefa Transferir Mensagens de Erro inclui as seguintes entradas de log personalizadas:  
  
-   TransferErrorMessagesTaskStartTransferringObjects   Essa entrada de log informa que a transferência foi iniciada. A entrada do log contém a hora de início.  
  
-   TransferErrorMessagesTaskFinishedTransferringObjects    Essa entrada de log informa que a transferência foi concluída. A entrada do log contém a hora de término.  
  
 Além disso, uma entrada de log para o evento **OnInformation** informa o número de mensagens de erro transferidas e uma entrada de log para **OnWarning event** é gravada para cada mensagem de erro no destino que for substituído.  
  
## <a name="security-and-permissions"></a>Segurança e permissões  
 Para criar novas mensagens de erro, o usuário que executa o pacote deve ser um membro do sysadmin ou ter função de servidor  serveradmin no servidor de destino.  
  
## <a name="configuration-of-the-transfer-error-messages-task"></a>Configuração da tarefa Transferir Mensagens de Erro  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor da Tarefa Transferir Mensagens de Erro &#40;Página Geral&#41;](../../integration-services/control-flow/transfer-error-messages-task-editor-general-page.md)  
  
-   [Editor da Tarefa Transferir Mensagens de Erro &#40;Página Mensagens&#41;](../../integration-services/control-flow/transfer-error-messages-task-editor-messages-page.md)  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferErrorMessagesTask.TransferErrorMessagesTask>  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
