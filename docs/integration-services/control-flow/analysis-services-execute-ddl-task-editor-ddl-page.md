---
title: "Editor da Tarefa Executar DDL do Analysis Services (P&#225;gina DDL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.asexecuteddltask.ddl.f1"
helpviewer_keywords: 
  - "Editor da Tarefa Executar DDL do Analysis Services"
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Editor da Tarefa Executar DDL do Analysis Services (P&#225;gina DDL)
  Use a página **DDL** da caixa de diálogo **Editor da Tarefa Executar DDL do Analysis Services** para especificar uma conexão com um projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou um banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e para fornecer informações sobre a origem das instruções DDL (linguagem de definição de dados).  
  
 Para saber mais sobre essa tarefa, consulte [Tarefa Executar DDL do Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md).  
  
## Opções estáticas  
 **Conexão**  
 Selecione um projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou um gerenciador de conexões [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na lista ou clique em \<**Nova conexão...**> e use a caixa de diálogo **Adicionar Gerenciador de Conexões do Analysis Services** para criar uma nova conexão.  
  
 **Tópicos relacionados:** [Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Gerenciador de Conexão do Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 Especifique a origem da instrução DDL. As opções desta propriedade estão listadas na seguinte tabela:  
  
|Value|Description|  
|-----------|-----------------|  
|**Direct Input**|Define a origem da instrução DDL armazenada na caixa de texto **SourceDirect**. A seleção deste valor exibe as opções dinâmicas na seção a seguir.|  
|**File Connection**|Define a origem para um arquivo que contém a instrução DDL. A seleção deste valor exibe as opções dinâmicas na seção a seguir.|  
|**Variável**|Define a origem para uma variável. A seleção deste valor exibe as opções dinâmicas na seção a seguir.|  
  
## Opções dinâmicas  
  
### SourceType = Entrada Direta  
 **Origem**  
 Digite as instruções DDL ou clique nas reticências **(…)** e digite as instruções na caixa de diálogo **Instruções DDL**.  
  
### SourceType = File Connection  
 **Origem**  
 Selecione uma conexão de Arquivo na lista ou clique em \<**Nova conexão...**> e use a caixa de diálogo **Adicionar Gerenciador de Conexões de Arquivos** para criar uma nova conexão.  
  
 **Tópicos relacionados:** [Gerenciador de conexões de arquivos](../../integration-services/connection-manager/file-connection-manager.md)  
  
### SourceType = Variable  
 **Origem**  
 Selecione uma variável na lista ou clique em \<**Nova variável...**> e use a caixa de diálogo **Adicionar Variável** para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa Executar DDL do Analysis Services &#40;Página Geral&#41;](../../integration-services/control-flow/analysis-services-execute-ddl-task-editor-general-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)   
 [Linguagem de script do Analysis Services &#40;ASSL para XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [Referência de XML for Analysis &#40;XMLA&#41;](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  