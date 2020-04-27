---
title: Editor da tarefa fila de mensagens (página Enviar) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.send.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 565aa079-ac44-4407-8efc-cddab839de30
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 66323ccdb91076496f9796245c368697d9ebc8c3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66057596"
---
# <a name="message-queue-task-editor-send-page"></a>Editor da Tarefa Fila de Mensagens (página Enviar)
  Use a página **Enviar** da caixa de diálogo **Editor da Tarefa Fila de Mensagens** para configurar uma tarefa de Fila de Mensagens para enviar mensagens de um pacote do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 Para obter informações sobre essa tarefa, consulte [Message Queue Task](control-flow/message-queue-task.md).  
  
## <a name="options"></a>Opções  
 **UseEncryption**  
 Indique se a mensagem deve ser criptografada. O padrão é `False`.  
  
 **EncryptionAlgorithm**  
 Se você escolher usar criptografia, especifique o nome do algoritmo de criptografia a ser utilizado. A tarefa Fila de Mensagens pode usar os algoritmos RC2 e RC4. O padrão é **RC2**.  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. Na versão atual do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
  
> [!IMPORTANT]  
>  Estes são os algoritmos de criptografia ao qual a tecnologia de serviço de Enfileiramento de Mensagens (também conhecido como MSMQ) oferece suporte. Atualmente, ambos algoritmos de criptografia são considerados criptograficamente fracos quando comparados a algoritmos mais novos, que não têm suporte no serviço de Enfileiramento de Mensagens. Então, você deve considerar cuidadosamente suas necessidades de criptografia ao enviar mensagens que usam a tarefa Fila de Mensagens.  
  
 **MessageType**  
 Selecione o tipo de mensagem. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Mensagem do arquivo de dados**|A mensagem é armazenada em um arquivo. Selecionar este valor faz com que seja exibida a opção dinâmica **DataFileMessage**.|  
|**Mensagem de variável**|A mensagem é armazenada em uma variável. Selecionar este valor faz com que seja exibida a opção dinâmica **VariableMessage**.|  
|**Mensagem de cadeia de caracteres**|A mensagem é armazenada em uma tarefa Fila de Mensagens. Selecionar este valor faz com que seja exibida a opção dinâmica **StringMessage**.|  
  
## <a name="messagetype-dynamic-options"></a>Opções dinâmicas de MessageType  
  
### <a name="messagetype--data-file-message"></a>MessageType = Mensagem de arquivo de dados  
 **DataFileMessage**  
 Digite o caminho do arquivo de dados ou clique nas reticências **(...)** e localize o arquivo.  
  
### <a name="messagetype--variable-message"></a>MessageType = Mensagem de variável  
 **VariableMessage**  
 Digite os nomes das variáveis ou clique nas reticências **(...)** e, em seguida, selecione as variáveis. As variáveis são separadas por vírgulas.  
  
 **Tópicos Relacionados:** Selecionar Variáveis  
  
### <a name="messagetype--string-message"></a>MessageType = Mensagem de cadeia de caracteres  
 **StringMessage**  
 Digite a mensagem de cadeia de caracteres ou clique nas reticências **(...)** e digite a mensagem na caixa de diálogo **Inserir mensagem de cadeia de caracteres** .  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa fila de mensagens &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor da tarefa fila de mensagens &#40;página receber&#41;](../../2014/integration-services/message-queue-task-editor-receive-page.md)   
 [Página Expressões](expressions/expressions-page.md)  
  
  
