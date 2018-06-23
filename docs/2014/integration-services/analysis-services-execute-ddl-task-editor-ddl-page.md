---
title: Analysis Services Execute DDL Editor da tarefa (página DDL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL Task Editor
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9499537bdb59778ab4dc5d511c16e3fb4cb9be08
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018961"
---
# <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Editor da Tarefa Executar DDL do Analysis Services (Página DDL)
  Use a página **DDL** da caixa de diálogo **Editor da Tarefa Executar DDL do Analysis Services** para especificar uma conexão com um projeto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou um banco de dados [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e para fornecer informações sobre a origem das instruções DDL (linguagem de definição de dados).  
  
 Para saber mais sobre essa tarefa, consulte [Tarefa Executar DDL do Analysis Services](control-flow/analysis-services-execute-ddl-task.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Conexão**  
 Selecione um projeto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou um gerenciador de conexões [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] na lista ou clique em \<**Nova conexão...**> e use a caixa de diálogo **Adicionar Gerenciador de Conexões do Analysis Services** para criar uma nova conexão.  
  
 **Tópicos relacionados:** [Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Gerenciador de Conexão do Analysis Services](connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 Especifique a origem da instrução DDL. As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|Description|  
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
 Selecione uma conexão de Arquivo na lista ou clique em \<**Nova conexão...**> e use a caixa de diálogo **Adicionar Gerenciador de Conexões de Arquivos** para criar uma nova conexão.  
  
 **Tópicos relacionados:** [Gerenciador de conexões de arquivos](connection-manager/file-connection-manager.md)  
  
### <a name="sourcetype--variable"></a>SourceType = Variable  
 **Origem**  
 Selecione uma variável na lista ou clique em \<**Nova variável...**> e use a caixa de diálogo **Adicionar Variável** para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Analysis Services Execute DDL Editor da tarefa &#40;página geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Página expressões](expressions/expressions-page.md)   
 [Fluxo de controle](control-flow/control-flow.md)   
 [Linguagem de script do Analysis Services &#40;ASSL&#41; referência](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [XML for Analysis &#40;XMLA&#41; referência](../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  