---
title: "Editor da Tarefa Fila de Mensagens (p&#225;gina Receber) | Microsoft Docs"
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
  - "sql13.dts.designer.msgqueuetask.receive.f1"
helpviewer_keywords: 
  - "Editor da Tarefa Fila de Mensagens"
ms.assetid: 7028756d-1dcc-480c-bbcd-e9654f0772a0
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# Editor da Tarefa Fila de Mensagens (p&#225;gina Receber)
  Use a página **Receber** da caixa de diálogo **Editor da Tarefa Fila de Mensagens** para configurar uma tarefa Fila de Mensagens para receber mensagens do MSMQ (Serviço de Enfileiramento de Mensagens) [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 Para obter informações sobre essa tarefa, consulte [Message Queue Task](../../integration-services/control-flow/message-queue-task.md).  
  
## Opções  
 **RemoveFromMessageQueue**  
 Indique se a mensagem deve ser removida da fila depois de ser recebida. Por padrão, esse valor é definido como **False**.  
  
 **ErrorIfMessageTimeOut**  
 Indique se a tarefa falha quando a mensagem expira, exibindo uma mensagem de erro. O padrão é **False**.  
  
 **TimeoutAfter**  
 Se você optar por exibir uma mensagem de erro quando uma tarefa falha, especifique quantos segundos esperar antes de ser exibida a mensagem de tempo limite ultrapassado.  
  
 **MessageType**  
 Selecione o tipo de mensagem. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Mensagem do arquivo de dados**|A mensagem é armazenada em um arquivo. Selecionar este valor faz com que seja exibida a opção dinâmica **DataFileMessage**.|  
|**Mensagem de variável**|A mensagem é armazenada em uma variável. Selecionar este valor faz com que seja exibida a opção dinâmica **VariableMessage**.|  
|**Mensagem de cadeia de caracteres**|A mensagem é armazenada em uma tarefa Fila de Mensagens. Selecionar este valor faz com que seja exibida a opção dinâmica **StringMessage**.|  
|**Mensagem de cadeia de caracteres para variável**|A mensagem<br /><br /> Selecionar este valor faz com que seja exibida a opção dinâmica **StringMessage**.|  
  
## Opções dinâmicas de MessageType  
  
### MessageType = Mensagem de arquivo de dados  
 **SaveFileAs**  
 Digite o caminho do arquivo a ser utilizado ou clique no botão de reticências **(…)** e localize o arquivo.  
  
 **Overwrite**  
 Indique se os dados em um arquivo existente devem ser substituídos quando o conteúdo de uma mensagem de arquivo de dados é salvo. O padrão é **False**.  
  
 **Filtro**  
 Especifique se deve ser aplicado um filtro à mensagem. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Sem-filtro**|A tarefa não filtra as mensagens. Selecionar este valor faz com que seja exibida a opção dinâmica **IdentifierReadOnly**.|  
|**Do pacote**|A mensagem recebe somente mensagens do pacote especificado. Selecionar este valor faz com que seja exibida a opção dinâmica **Identifier**.|  
  
### Opções dinâmicas do filtro  
  
#### Filtrar = Sem-filtro  
 **IdentifierReadOnly**  
 Esta opção é somente leitura. Pode ser em branco ou conter o GUID de um pacote quando a propriedade Filtrar tiver sido definida anteriormente.  
  
#### Filtrar = Do pacote  
 **Identificador**  
 Se você optar por aplicar um filtro, digite o identificador exclusivo do pacote do qual podem ser recebidas mensagens ou clique no botão de reticências **(…)** e especifique o pacote.  
  
 **Tópicos relacionados:** [Selecionar um pacote](../../integration-services/control-flow/select-a-package.md)  
  
### MessageType = Mensagem de variável  
 **Filtro**  
 Especifique se deve ser aplicado um filtro às mensagens. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Sem-filtro**|A tarefa não filtra as mensagens. Selecionar este valor faz com que seja exibida a opção dinâmica **IdentifierReadOnly**.|  
|**Do pacote**|A mensagem recebe somente mensagens do pacote especificado. Selecionar este valor faz com que seja exibida a opção dinâmica **Identifier**.|  
  
 **Variável**  
 Digite o nome da variável ou clique em \<**Nova variável...**> e configure uma variável nova.  
  
 **Tópicos relacionados:** [Adicionar variável](../Topic/Add%20Variable.md)  
  
### Opções dinâmicas do filtro  
  
#### Filtrar = Sem-filtro  
 **IdentifierReadOnly**  
 Esta opção fica em branco.  
  
#### Filtrar = Do pacote  
 **Identificador**  
 Se você optar por aplicar um filtro, digite o identificador exclusivo do pacote do qual podem ser recebidas mensagens ou clique no botão de reticências **(…)** e especifique o pacote.  
  
 **Tópicos relacionados:** [Selecionar um pacote](../../integration-services/control-flow/select-a-package.md)  
  
### MessageType = Mensagem de cadeia de caracteres  
 **Comparar**  
 Especifique se deve ser aplicado um filtro às mensagens. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Nenhum.**|As mensagens não são comparadas.|  
|**Correspondência exata**|As mensagens devem corresponder exatamente à cadeia de caracteres na opção **CompareString** .|  
|**Ignora maiúsculas e minúsculas**|A mensagem deve corresponder à cadeia de caracteres da opção **CompareString** , mas a comparação não diferencia maiúsculas e minúsculas.|  
|**Contendo**|A mensagem deve conter a cadeia de caracteres na opção **CompareString** .|  
  
 **CompareString**  
 A menos que a opção **Comparar** esteja definida como **Nenhum**, forneça a cadeia de caracteres com a qual a mensagem é comparada.  
  
### MessageType = Mensagem de cadeia de caracteres para variável  
 **Comparar**  
 Especifique se deve ser aplicado um filtro às mensagens. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Nenhum.**|As mensagens não são comparadas.|  
|**Correspondência exata**|A mensagem deve corresponder exatamente à cadeia de caracteres na opção **CompareString** .|  
|**Ignora maiúsculas e minúsculas**|A mensagem deve corresponder à cadeia de caracteres da opção **CompareString** , mas a comparação não diferencia maiúsculas e minúsculas.|  
|**Contendo**|A mensagem deve conter a cadeia de caracteres na opção **CompareString** .|  
  
 **CompareString**  
 A menos que a opção **Comparar** esteja definida como **Nenhum**, forneça a cadeia de caracteres com a qual a mensagem é comparada.  
  
 **Variável**  
 Digite o nome da variável para manter a mensagem recebida ou clique em \<**Nova variável...**> e configure uma variável nova.  
  
 **Tópicos relacionados:** [Adicionar variável](../Topic/Add%20Variable.md)  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa Fila de Mensagens &#40;Página Geral&#41;](../../integration-services/control-flow/message-queue-task-editor-general-page.md)   
 [Editor da Tarefa Fila de Mensagens &#40;Página Enviar&#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)   
 [Tarefa Fila de Mensagens](../../integration-services/control-flow/message-queue-task.md)  
  
  