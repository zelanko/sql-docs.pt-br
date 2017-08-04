---
title: Tarefa transferir logons | Microsoft Docs
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
- sql13.dts.designer.transferloginstask.f1
helpviewer_keywords:
- Transfer Logins task [Integration Services]
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 02215c15fbbbcb4f7fd5ee5638afa4e0092e86c9
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-logins-task"></a>Tarefa Transferir Logons
  A tarefa Transferir Logons transfere um ou mais logons entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="transfer-logins-between-instances-of-sql-server"></a>Transfer logons entre instâncias do SQL Server  
 A tarefa Transferir Logons dá suporte a uma origem e a um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventos  
 A tarefa gera um evento de informação com o número de logons transferidos e um evento de aviso quando um logon é substituído.  
  
 A tarefa Transferir Logons não informa o progresso incremental da transferência de logons; informa só 0% e 100% concluídos.  
  
## <a name="execution-value"></a>Valor de execução  
 O valor de execução, definido na propriedade da tarefa **ExecutionValue** retorna o número de logons que são transferidos. Ao atribuir uma variável definida pelo usuário à propriedade **ExecValueVariable** da tarefa Transferir Logons, informações sobre a transferência de logons podem se tornar disponíveis a outros objetos no pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Entradas de log  
 A tarefa Transferir Logons inclui as seguintes entradas de log personalizadas:  
  
-   TransferLoginsTaskStarTransferringObjects    Essa entrada de log informa que a transferência foi iniciada. A entrada do log contém a hora de início.  
  
-   TransferLoginsTaskFinishedTransferringObjects   Essa entrada de log informa que a transferência foi concluída. A entrada do log contém a hora de término.  
  
 Além disso, uma entrada de log para o evento **OnInformation** informa o número de logons que foram transferidos e uma entrada de log para o evento **OnWarning** é gravada para cada logon no destino que for substituído.  
  
## <a name="security-and-permissions"></a>Segurança e permissões  
 Para procurar logons no servidor de origem e criar logons no servidor de destino, o usuário deve ser um membro da função de sysadmin em ambos os servidores.  
  
## <a name="configuration-of-the-transfer-logins-task"></a>Configuração da tarefa Transferir Logons  
 A tarefa Transferira Logons pode ser configurada para transferir todos os logons, só os logons especificados ou todos os logons que só têm acesso a bancos de dados especificados. O logon do sa não pode ser transferido. O logon sa pode ser renomeado; porém, o logon sa renomeado não pode ser transferido.  
  
 Você também pode indicar se a tarefa deve copiar os SIDs (identificadores de segurança) associados aos logons. Se a tarefa Transferir Logons for usada junto com a tarefa Transferir Banco de Dados, os SIDs deverão ser copiados para o destino; caso contrário, os logons transferidos não serão reconhecidos pelo banco de dados de destino.  
  
 No destino, os logons transferidos são desabilitados e senhas aleatórias são atribuídas a eles. Um membro da função de sysadmin no servidor de destino deve alterar as senhas e habilitar os logons antes de os logons poderem ser usados.  
  
 Os logons a serem transferidos já podem existir no destino. A tarefa Transferir Logons pode ser configurada para manipular os logons existentes dos modos a seguir:  
  
-   Substituir os logons existentes.  
  
-   Interromper a tarefa quando houver logons duplicados.  
  
-   Ignorar logons duplicados.  
  
 No tempo de execução, a tarefa Transferir Logons conecta-se aos servidores de origem e de destino usando dois gerenciadores de conexões SMO. Os gerenciadores de conexões SMO são configurados separadamente da tarefa Transferir Logons e depois são referenciados na tarefa Transferir Logons. Os gerenciadores de conexões SMO especificam o servidor e o modo de autenticação a serem usados ao acessar o servidor. Para obter mais informações, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor da Tarefa Transferir Logons &#40;Página Geral&#41;](../../integration-services/control-flow/transfer-logins-task-editor-general-page.md)  
  
-   [Editor da Tarefa Transferir Logons &#40;Página Logons&#41;](../../integration-services/control-flow/transfer-logins-task-editor-logins-page.md)  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-logins-task"></a>Configuração programática da tarefa Transferir Logons  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
  
