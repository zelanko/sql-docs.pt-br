---
title: "Analysis Services Execute DDL Editor da tarefa (página DDL) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL Task Editor
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4bae07f66d84f8a692ad7b59ef61ee63d4a5fd62
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Editor da Tarefa Executar DDL do Analysis Services (Página DDL)
  Use a página **DDL** da caixa de diálogo **Editor da Tarefa Executar DDL do Analysis Services** para especificar uma conexão com um projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou um banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e para fornecer informações sobre a origem das instruções DDL (linguagem de definição de dados).  
  
 Para saber mais sobre essa tarefa, consulte [Tarefa Executar DDL do Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Conexão**  
 Selecione um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto ou um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Gerenciador de conexão na lista ou clique em \< **nova conexão...** > e use o **adicionar Gerenciador de Conexão do Analysis Services** caixa de diálogo para criar uma nova conexão.  
  
 **Tópicos relacionados:** [Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Gerenciador de Conexão do Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 Especifique a origem da instrução DDL. As opções desta propriedade estão listadas na seguinte tabela:  
  
|Value|Description|  
|-----------|-----------------|  
|**Direct Input**|Define a origem da instrução DDL armazenada na caixa de texto **SourceDirect** . A seleção deste valor exibe as opções dinâmicas na seção a seguir.|  
|**File Connection**|Define a origem para um arquivo que contém a instrução DDL. A seleção deste valor exibe as opções dinâmicas na seção a seguir.|  
|**Variável**|Define a origem para uma variável. A seleção deste valor exibe as opções dinâmicas na seção a seguir.|  
  
## <a name="dynamic-options"></a>Opções dinâmicas  
  
### <a name="sourcetype--direct-input"></a>SourceType = Entrada Direta  
 **Origem**  
 Digite as instruções DDL ou clique nas reticências **(…)** e digite as instruções na caixa de diálogo **Instruções DDL** .  
  
### <a name="sourcetype--file-connection"></a>SourceType = File Connection  
 **Origem**  
 Selecione uma conexão de arquivo na lista ou clique em \< **nova conexão...** > e use o **Gerenciador de Conexão de arquivo** caixa de diálogo para criar uma nova conexão.  
  
 **Tópicos relacionados:** [Adicionar Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md)  
  
### <a name="sourcetype--variable"></a>SourceType = Variable  
 **Origem**  
 Selecione uma variável na lista ou clique em \< **nova variável...** > e use o **Adicionar variável** caixa de diálogo para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa DDL &#40; executar do Analysis Services Página geral &#41;](../../integration-services/control-flow/analysis-services-execute-ddl-task-editor-general-page.md)   
 [Página expressões](../../integration-services/expressions/expressions-page.md)   
 [Fluxo de controle](../../integration-services/control-flow/control-flow.md)   
 [Linguagem de script do Analysis Services &#40;ASSL para XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [XML for Analysis &#40; XMLA &#41; Referência](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
