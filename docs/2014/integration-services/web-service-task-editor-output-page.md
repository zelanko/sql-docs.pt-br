---
title: Editor da tarefa serviço da Web (página saída) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7924570253bf2f805d91c4dfabc3d5facf44cccc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054467"
---
# <a name="web-service-task-editor-output-page"></a>Editor da Tarefa Serviço da Web (página Saída)
  Use a página **Saída** da caixa de diálogo **Editor da Tarefa Serviço da Web** para especificar onde armazenar o resultado retornado pelo método Web.  
  
 Para saber mais sobre essa tarefa, consulte [Tarefa Serviço da Web](control-flow/web-service-task.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **OutputType**  
 Selecione o tipo de armazenamento a usar para os resultados. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**File Connection**|Armazene os resultados em um arquivo. A seleção deste valor exibe a opção dinâmica **File**.|  
|**Variável**|Armazene os resultados em uma variável. A seleção deste valor exibe a opção dinâmica **Variable**.|  
  
## <a name="outputtype-dynamic-options"></a>Opções dinâmicas de OutputType  
  
### <a name="outputtype--file-connection"></a>OutputType = File Connection  
 **File**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…** > para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de conexões de arquivos](connection-manager/file-connection-manager.md), [Editor do Gerenciador de conexões de Arquivos](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="outputtype--variable"></a>OutputType = Variable  
 **Variável**  
 Selecione uma variável na lista ou clique em \<**Nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados:**  [Variáveis do Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa Serviço da Web &#40;Página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor da Tarefa Serviço da Web &#40;Página Entrada&#41;](../../2014/integration-services/web-service-task-editor-input-page.md)   
 [Página Expressões](expressions/expressions-page.md)  
  
  
