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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c6d753b7ef37d515140a3fc32137dd4680fa3079
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439813"
---
# <a name="web-service-task-editor-output-page"></a>Editor da Tarefa Serviço da Web (página Saída)
  Use a página **Saída** da caixa de diálogo **Editor da Tarefa Serviço da Web** para especificar onde armazenar o resultado retornado pelo método Web.  
  
 Para saber mais sobre essa tarefa, consulte [Tarefa Serviço da Web](control-flow/web-service-task.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **OutputType**  
 Selecione o tipo de armazenamento a usar para os resultados. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Conexão de arquivo**|Armazene os resultados em um arquivo. A seleção deste valor exibe a opção dinâmica **File**.|  
|**Variável**|Armazene os resultados em uma variável. A seleção deste valor exibe a opção dinâmica **Variable**.|  
  
## <a name="outputtype-dynamic-options"></a>Opções dinâmicas de OutputType  
  
### <a name="outputtype--file-connection"></a>OutputType = File Connection  
 **Arquivo**  
 Selecione um Gerenciador de conexões de arquivo na lista ou clique \<**New Connection...**> para criar um novo Gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="outputtype--variable"></a>OutputType = Variable  
 **Variável**  
 Selecione uma variável na lista ou clique \<**New Variable...**> para criar uma nova variável.  
  
 **Tópicos relacionados:**  [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa serviço da Web &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor da tarefa serviço Web &#40;página de entrada&#41;](../../2014/integration-services/web-service-task-editor-input-page.md)   
 [Página Expressões](expressions/expressions-page.md)  
  
  
