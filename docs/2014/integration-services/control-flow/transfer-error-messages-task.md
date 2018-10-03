---
title: Tarefa Transferir Mensagens de Erro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfererrormessagestask.f1
helpviewer_keywords:
- Transfer Error Messages task [Integration Services]
ms.assetid: da702289-035a-4d14-bd74-04461fbfee1b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7b5f1089c48d4a3ebc844bf01644407b138ce265
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48098406"
---
# <a name="transfer-error-messages-task"></a>Tarefa Transferir Mensagens de Erro
  A tarefa Transferir Mensagens de Erro transfere uma ou mais mensagens de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definidas pelo usuário entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mensagens definidas pelo usuário são mensagens com um identificador igual ou maior que 50000. Mensagens com identificador menor que 50000 são mensagens de erro do sistema e não podem ser transferidas usando-se a tarefa Transferir Mensagens de Erro.  
  
 A tarefa Transferir Mensagens de Erro pode ser configurada para transferir todas as mensagens de erro ou só as mensagens de erro especificadas. Mensagens de erro definidas pelo usuário podem estar disponíveis em vários idiomas diferentes e a tarefa pode ser configurada para só transferir mensagens em idiomas selecionados. Uma versão us_english da mensagem, que usa a página de código 1033, deve estar no servidor de destino para que você possa transferir versões em outro idioma da mensagem para esse servidor.  
  
 A tabela sysmessages no banco de dados mestre contém todas as mensagens de erro, tanto as de sistema como as definidas pelo usuário, que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa.  
  
 As mensagens definidas pelo usuário a serem transferidas já podem existir no destino. Uma mensagem de erro estará definida como mensagem de erro duplicada se o identificador e o idioma forem os mesmos. A tarefa Transferir Mensagens de Erro pode ser configurada para controlar mensagens de erro da seguinte maneira:  
  
-   Substituir mensagens de erro existentes.  
  
-   Interromper a tarefa quando houver mensagens duplicadas.  
  
-   Ignorar mensagens de erro duplicadas.  
  
 No tempo de execução, a tarefa Transferir Mensagens de Erro conecta-se aos servidores de origem e de destino usando um ou dois gerenciadores de conexões SMO. O gerenciador de conexões SMO é configurado separadamente da tarefa Transferir Mensagens de Erro e, depois, é consultado na tarefa Transferir Mensagens de Erro. O gerenciador de conexões SMO especifica o servidor e o modo de autenticação a ser usado ao acessar o servidor. Para obter mais informações, consulte [SMO Connection Manager](../connection-manager/smo-connection-manager.md).  
  
 A tarefa Transferir Mensagens de Erro dá suporte a uma origem e a um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Não há nenhuma restrição quanto à versão a ser usada como origem ou destino.  
  
## <a name="events"></a>Eventos  
 A tarefa gera  um evento de informações que informa o número de mensagens de erro que foram transferidas.  
  
 A tarefa Transferir Mensagens de Erro não informa o progresso incremental da transferência de mensagem de erro; informa somente conclusão 0% e 100 %.  
  
## <a name="execution-value"></a>Valor de execução  
 O valor de execução, definido na propriedade `ExecutionValue` da tarefa retorna o número de mensagens de erro que foram transferidas. Ao atribuir uma variável definida pelo usuário para o `ExecValueVariable` propriedade da tarefa transferir mensagens de erro, informações sobre a transferência de mensagem de erro pode se tornar disponível a outros objetos no pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Usar variáveis em pacotes](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Entradas de log  
 A tarefa Transferir Mensagens de Erro inclui as seguintes entradas de log personalizadas:  
  
-   TransferErrorMessagesTaskStartTransferringObjects   Essa entrada de log informa que a transferência foi iniciada. A entrada do log contém a hora de início.  
  
-   TransferErrorMessagesTaskFinishedTransferringObjects    Essa entrada de log informa que a transferência foi concluída. A entrada do log contém a hora de término.  
  
 Além disso, uma entrada de log para o `OnInformation` evento informa o número de mensagens de erro que foram transferidas e uma entrada de log para o `OnWarning event` é gravada para cada mensagem de erro no destino que será substituído.  
  
## <a name="security-and-permissions"></a>Segurança e permissões  
 Para criar novas mensagens de erro, o usuário que executa o pacote deve ser um membro do sysadmin ou ter função de servidor  serveradmin no servidor de destino.  
  
## <a name="configuration-of-the-transfer-error-messages-task"></a>Configuração da tarefa Transferir Mensagens de Erro  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor de tarefa de mensagens de erro de transferência &#40;página geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de tarefa de mensagens de erro de transferência &#40;página de mensagens&#41;](../transfer-error-messages-task-editor-messages-page.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferErrorMessagesTask.TransferErrorMessagesTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Integration Services](integration-services-tasks.md)   
 [Fluxo de Controle](control-flow.md)  
  
  
