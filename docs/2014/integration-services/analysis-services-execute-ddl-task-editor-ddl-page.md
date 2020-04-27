---
title: Editor da tarefa Executar DDL do Analysis Services (página DDL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL Task Editor
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2b57ad76be3811352bbfb8774fb56c748efa1ac8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66061613"
---
# <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Editor da Tarefa Executar DDL do Analysis Services (Página DDL)
  Use a página **DDL** da caixa de diálogo **Editor da Tarefa Executar DDL do Analysis Services** para especificar uma conexão com um projeto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou um banco de dados [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e para fornecer informações sobre a origem das instruções DDL (linguagem de definição de dados).  
  
 Para saber mais sobre essa tarefa, consulte [Tarefa Executar DDL do Analysis Services](control-flow/analysis-services-execute-ddl-task.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Conexão**  
 Selecione um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] projeto ou um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Gerenciador de conexões na lista ou clique em \< **nova conexão...**> e use a caixa de diálogo **Adicionar Gerenciador de conexões Analysis Services** para criar uma nova conexão.  
  
 **Tópicos relacionados:** [Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Gerenciador de Conexão do Analysis Services](connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 Especifique a origem da instrução DDL. As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada direta**|Define a origem da instrução DDL armazenada na caixa de texto **SourceDirect** . A seleção deste valor exibe as opções dinâmicas na seção a seguir.|  
|**Conexão de arquivo**|Define a origem para um arquivo que contém a instrução DDL. A seleção deste valor exibe as opções dinâmicas na seção a seguir.|  
|**Variável**|Define a origem para uma variável. A seleção deste valor exibe as opções dinâmicas na seção a seguir.|  
  
## <a name="dynamic-options"></a>Opções dinâmicas  
  
### <a name="sourcetype--direct-input"></a>SourceType = Entrada Direta  
 **Fonte**  
 Digite as instruções DDL ou clique nas reticências **(...)** e, em seguida, digite as instruções na caixa de diálogo **instruções DDL** .  
  
### <a name="sourcetype--file-connection"></a>SourceType = File Connection  
 **Fonte**  
 Selecione uma conexão de arquivo na lista ou clique em \< **nova conexão...**> e use a caixa de diálogo **Gerenciador de conexões de arquivos** para criar uma nova conexão.  
  
 **Tópicos relacionados:** [Adicionar Gerenciador de Conexões de Arquivos](connection-manager/file-connection-manager.md)  
  
### <a name="sourcetype--variable"></a>SourceType = Variable  
 **Fonte**  
 Selecione uma variável na lista ou clique em \< **nova variável...**> e use a caixa de diálogo **Adicionar variável** para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Analysis Services executar o editor da tarefa DDL &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Página de expressões](expressions/expressions-page.md)   
 [Fluxo de Controle](control-flow/control-flow.md)   
 [Analysis Services linguagem de script &#40;referência de&#41; do ASSL](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [Referência de XML for Analysis &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)  
  
  
