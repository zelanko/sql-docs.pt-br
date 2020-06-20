---
title: Editor da tarefa fila de mensagens (página receber) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.receive.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 7028756d-1dcc-480c-bbcd-e9654f0772a0
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b30a7863fe50843f4408931b2b766bcb520f3a2c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84950984"
---
# <a name="message-queue-task-editor-receive-page"></a>Editor da Tarefa Fila de Mensagens (página Receber)
  Use a página **Receber** da caixa de diálogo **Editor da Tarefa Fila de Mensagens** para configurar uma tarefa Fila de Mensagens para receber mensagens do MSMQ (Serviço de Enfileiramento de Mensagens) [!INCLUDE[msCoName](../includes/msconame-md.md)] .  
  
 Para obter informações sobre essa tarefa, consulte [Message Queue Task](control-flow/message-queue-task.md).  
  
## <a name="options"></a>Opções  
 **RemoveFromMessageQueue**  
 Indique se a mensagem deve ser removida da fila depois de ser recebida. Por padrão, esse valor é definido como `False`.  
  
 **ErrorIfMessageTimeOut**  
 Indique se a tarefa falha quando a mensagem expira, exibindo uma mensagem de erro. O padrão é `False`.  
  
 **TimeoutAfter**  
 Se você optar por exibir uma mensagem de erro quando uma tarefa falha, especifique quantos segundos esperar antes de ser exibida a mensagem de tempo limite ultrapassado.  
  
 **MessageType**  
 Selecione o tipo de mensagem. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Mensagem do arquivo de dados**|A mensagem é armazenada em um arquivo. Selecionar este valor faz com que seja exibida a opção dinâmica **DataFileMessage**.|  
|**Mensagem de variável**|A mensagem é armazenada em uma variável. Selecionar este valor faz com que seja exibida a opção dinâmica **VariableMessage**.|  
|**Mensagem de cadeia de caracteres**|A mensagem é armazenada em uma tarefa Fila de Mensagens. Selecionar este valor faz com que seja exibida a opção dinâmica **StringMessage**.|  
|**Mensagem de cadeia de caracteres para variável**|A mensagem<br /><br /> Selecionar este valor faz com que seja exibida a opção dinâmica **StringMessage**.|  
  
## <a name="messagetype-dynamic-options"></a>Opções dinâmicas de MessageType  
  
### <a name="messagetype--data-file-message"></a>MessageType = Mensagem de arquivo de dados  
 **SaveFileAs**  
 Digite o caminho do arquivo a ser usado ou clique no botão de reticências **(...)** e, em seguida, localize o arquivo.  
  
 **Overwrite**  
 Indique se os dados em um arquivo existente devem ser substituídos quando o conteúdo de uma mensagem de arquivo de dados é salvo. O padrão é `False`.  
  
 **Filter**  
 Especifique se deve ser aplicado um filtro à mensagem. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Sem-filtro**|A tarefa não filtra as mensagens. Selecionar este valor faz com que seja exibida a opção dinâmica **IdentifierReadOnly**.|  
|**Do pacote**|A mensagem recebe somente mensagens do pacote especificado. Selecionar este valor faz com que seja exibida a opção dinâmica **Identifier**.|  
  
### <a name="filter-dynamic-options"></a>Opções dinâmicas do filtro  
  
#### <a name="filter--no-filter"></a>Filtrar = Sem-filtro  
 **IdentifierReadOnly**  
 Esta opção é somente leitura. Pode ser em branco ou conter o GUID de um pacote quando a propriedade Filtrar tiver sido definida anteriormente.  
  
#### <a name="filter--from-package"></a>Filtrar = Do pacote  
 **ID**  
 Se você escolher aplicar um filtro, digite o identificador exclusivo do pacote do qual mensagens podem ser recebidas ou clique no botão de reticências **(…)** e especifique o pacote.  
  
 **Tópicos relacionados:** [Selecionar um pacote](control-flow/select-a-package.md)  
  
### <a name="messagetype--variable-message"></a>MessageType = Mensagem de variável  
 **Filter**  
 Especifique se deve ser aplicado um filtro às mensagens. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Sem-filtro**|A tarefa não filtra as mensagens. Selecionar este valor faz com que seja exibida a opção dinâmica **IdentifierReadOnly**.|  
|**Do pacote**|A mensagem recebe somente mensagens do pacote especificado. Selecionar este valor faz com que seja exibida a opção dinâmica **Identifier**.|  
  
 **Variável**  
 Digite o nome da variável ou clique em \<**New variable...**> e, em seguida, configure uma nova variável.  
  
 **Tópicos relacionados:** [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
### <a name="filter-dynamic-options"></a>Opções dinâmicas do filtro  
  
#### <a name="filter--no-filter"></a>Filtrar = Sem-filtro  
 **IdentifierReadOnly**  
 Esta opção fica em branco.  
  
#### <a name="filter--from-package"></a>Filtrar = Do pacote  
 **ID**  
 Se você escolher aplicar um filtro, digite o identificador exclusivo do pacote do qual mensagens podem ser recebidas ou clique no botão de reticências **(…)** e especifique o pacote.  
  
 **Tópicos relacionados:** [Selecionar um pacote](control-flow/select-a-package.md)  
  
### <a name="messagetype--string-message"></a>MessageType = Mensagem de cadeia de caracteres  
 **Comparar**  
 Especifique se deve ser aplicado um filtro às mensagens. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Nenhuma**|As mensagens não são comparadas.|  
|**Correspondência exata**|As mensagens devem corresponder exatamente à cadeia de caracteres na opção **CompareString** .|  
|**Ignora maiúsculas e minúsculas**|A mensagem deve corresponder à cadeia de caracteres da opção **CompareString** , mas a comparação não diferencia maiúsculas e minúsculas.|  
|**Contendo**|A mensagem deve conter a cadeia de caracteres na opção **CompareString** .|  
  
 **CompareString**  
 A menos que a opção **Comparar** esteja definida como **Nenhum**, forneça a cadeia de caracteres com a qual a mensagem é comparada.  
  
### <a name="messagetype--string-message-to-variable"></a>MessageType = Mensagem de cadeia de caracteres para variável  
 **Comparar**  
 Especifique se deve ser aplicado um filtro às mensagens. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Nenhuma**|As mensagens não são comparadas.|  
|**Correspondência exata**|A mensagem deve corresponder exatamente à cadeia de caracteres na opção **CompareString** .|  
|**Ignora maiúsculas e minúsculas**|A mensagem deve corresponder à cadeia de caracteres da opção **CompareString** , mas a comparação não diferencia maiúsculas e minúsculas.|  
|**Contendo**|A mensagem deve conter a cadeia de caracteres na opção **CompareString** .|  
  
 **CompareString**  
 A menos que a opção **Comparar** esteja definida como **Nenhum**, forneça a cadeia de caracteres com a qual a mensagem é comparada.  
  
 **Variável**  
 Digite o nome da variável para armazenar a mensagem recebida ou clique em \<**New variable...**> e, em seguida, configure uma nova variável.  
  
 **Tópicos relacionados:** [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa fila de mensagens &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor da tarefa fila de mensagens &#40;Enviar página&#41;](../../2014/integration-services/message-queue-task-editor-send-page.md)   
 [Página de expressões](expressions/expressions-page.md)   
 [Message Queue Task](control-flow/message-queue-task.md)  
  
  
