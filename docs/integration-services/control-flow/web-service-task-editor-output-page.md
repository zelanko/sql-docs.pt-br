---
title: "Editor da tarefa serviço da Web (página saída) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f4bd03a4844548b7dfbc976224c09c47f0ab2a4f
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="web-service-task-editor-output-page"></a>Editor da Tarefa Serviço da Web (página Saída)
  Use a página **Saída** da caixa de diálogo **Editor da Tarefa Serviço da Web** para especificar onde armazenar o resultado retornado pelo método Web.  
  
 Para saber mais sobre essa tarefa, consulte [Tarefa Serviço da Web](../../integration-services/control-flow/web-service-task.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **OutputType**  
 Selecione o tipo de armazenamento a usar para os resultados. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**File Connection**|Armazene os resultados em um arquivo. A seleção deste valor exibe a opção dinâmica **File**.|  
|**Variável**|Armazene os resultados em uma variável. A seleção deste valor exibe a opção dinâmica **Variable**.|  
  
## <a name="outputtype-dynamic-options"></a>Opções dinâmicas de OutputType  
  
### <a name="outputtype--file-connection"></a>OutputType = File Connection  
 **Arquivo**  
 Selecione um Gerenciador de conexão de arquivo na lista ou clique em \< **nova Conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="outputtype--variable"></a>OutputType = Variable  
 **Variável**  
 Selecione uma variável na lista ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa serviço da Web &#40; Página geral &#41;](../../integration-services/control-flow/web-service-task-editor-general-page.md)   
 [Web Editor da tarefa de serviço &#40; entrada página &#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
  
