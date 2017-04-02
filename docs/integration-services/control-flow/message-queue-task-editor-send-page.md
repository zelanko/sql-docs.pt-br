---
title: "Editor da Tarefa Fila de Mensagens (p&#225;gina Enviar) | Microsoft Docs"
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
  - "sql13.dts.designer.msgqueuetask.send.f1"
helpviewer_keywords: 
  - "Editor da Tarefa Fila de Mensagens"
ms.assetid: 565aa079-ac44-4407-8efc-cddab839de30
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# Editor da Tarefa Fila de Mensagens (p&#225;gina Enviar)
  Use a página **Enviar** da caixa de diálogo **Editor da Tarefa Fila de Mensagens** para configurar uma tarefa de Fila de Mensagens para enviar mensagens de um pacote do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Para obter informações sobre essa tarefa, consulte [Message Queue Task](../../integration-services/control-flow/message-queue-task.md).  
  
## Opções  
 **UseEncryption**  
 Indique se a mensagem deve ser criptografada. O padrão é **False**.  
  
 **EncryptionAlgorithm**  
 Se você escolher usar criptografia, especifique o nome do algoritmo de criptografia a ser utilizado. A tarefa Fila de Mensagens pode usar os algoritmos RC2 e RC4. O padrão é **RC2**.  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. Na versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
  
> [!IMPORTANT]  
>  Estes são os algoritmos de criptografia ao qual a tecnologia de serviço de Enfileiramento de Mensagens (também conhecido como MSMQ) oferece suporte. Atualmente, ambos algoritmos de criptografia são considerados criptograficamente fracos quando comparados a algoritmos mais novos, que não têm suporte no serviço de Enfileiramento de Mensagens. Então, você deve considerar cuidadosamente suas necessidades de criptografia ao enviar mensagens que usam a tarefa Fila de Mensagens.  
  
 **MessageType**  
 Selecione o tipo de mensagem. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Mensagem do arquivo de dados**|A mensagem é armazenada em um arquivo. Selecionar este valor faz com que seja exibida a opção dinâmica **DataFileMessage**.|  
|**Mensagem de variável**|A mensagem é armazenada em uma variável. Selecionar este valor faz com que seja exibida a opção dinâmica **VariableMessage**.|  
|**Mensagem de cadeia de caracteres**|A mensagem é armazenada em uma tarefa Fila de Mensagens. Selecionar este valor faz com que seja exibida a opção dinâmica **StringMessage**.|  
  
## Opções dinâmicas de MessageType  
  
### MessageType = Mensagem de arquivo de dados  
 **DataFileMessage**  
 Digite o caminho do arquivo de dados ou clique no botão de reticências **(…)** e localize o arquivo.  
  
### MessageType = Mensagem de variável  
 **VariableMessage**  
 Digite os nomes das variáveis ou clique no botão de reticências **(…)** e selecione as variáveis. As variáveis são separadas por vírgulas.  
  
 **Tópicos Relacionados:** Selecionar Variáveis  
  
### MessageType = Mensagem de cadeia de caracteres  
 **StringMessage**  
 Digite a mensagem de cadeia de caracteres ou clique no botão de reticências **(...)** e digite a mensagem na caixa de diálogo **Inserir Mensagem de Cadeia de Caracteres**.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa Fila de Mensagens &#40;Página Geral&#41;](../../integration-services/control-flow/message-queue-task-editor-general-page.md)   
 [Editor da Tarefa Fila de Mensagens &#40;Página Receber&#41;](../../integration-services/control-flow/message-queue-task-editor-receive-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
  