---
title: "Editor de Destino de Processamento de Dimens&#245;es (p&#225;gina Avan&#231;ado) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.dimprocessingtransformation.advanced.f1"
helpviewer_keywords: 
  - "Editor de Destino de Processamento de Dimensões"
ms.assetid: 2b30835a-2680-4d98-89a4-4f17e29e3818
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Editor de Destino de Processamento de Dimens&#245;es (p&#225;gina Avan&#231;ado)
  Use a página **Avançado** da caixa de diálogo **Editor de Destino de Processamento de Dimensões** para configurar o tratamento de erros.  
  
 Para saber mais sobre o destino de Processamento de Dimensões, consulte [Dimension Processing Destination](../../integration-services/data-flow/dimension-processing-destination.md).  
  
## Opções  
 **Usar configuração de erro padrão.**  
 Especifique se a manipulação de erros padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve ser usada. Por padrão, esse valor está definido como **True**.  
  
 **Ação de erro de chave**  
 Especifique como manipular registros que possuem valores de chave inaceitáveis.  
  
|Value|Description|  
|-----------|-----------------|  
|**ConvertToUnknown**|Converta o valor de chave inaceitável em um valor **UnknownMember**.|  
|**DiscardRecord**|Descarte o registro.|  
  
 **Ignorar erros**  
 Especifique se os erros devem ser ignorados.  
  
 **Parar se houver erro**  
 Especifique se o processamento deve parar quando ocorrer erro.  
  
 **Número de erros**  
 Caso tenha selecionado **Parar se houver erro**, especifique o limite de erros sob o qual o processamento deve parar.  
  
 **Ação se houver erro**  
 Caso tenha selecionado **Parar se houver erro**, especifique a ação a ser tomada quando o limite de erros for atingido.  
  
|Value|Description|  
|-----------|-----------------|  
|**StopProcessing**|Pare o processamento.|  
|**StopLogging**|Pare de registrar os erros.|  
  
 **Chave não encontrada**  
 Especifique a ação a ser tomada mediante erro de chave não encontrada. Por padrão, este valor é **ReportAndContinue**.  
  
|Value|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignore o erro e continue o processamento.|  
|**ReportAndContinue**|Relate o erro e continue o processamento.|  
|**ReportAndStop**|Relate o erro e pare o processamento.|  
  
 **Chave duplicada**  
 Especifique a ação a ser tomada mediante erro de chave duplicada. Por padrão, esse valor é **IgnoreError**.  
  
|Value|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignore o erro e continue o processamento.|  
|**ReportAndContinue**|Relate o erro e continue o processamento.|  
|**ReportAndStop**|Relate o erro e pare o processamento.|  
  
 **Chave nula convertida em desconhecida**  
 Especifique a ação a ser tomada quando uma chave nula foi convertida no valor **UnknownMember**. Por padrão, esse valor é **IgnoreError**.  
  
|Value|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignore o erro e continue o processamento.|  
|**ReportAndContinue**|Relate o erro e continue o processamento.|  
|**ReportAndStop**|Relate o erro e pare o processamento.|  
  
 **Chave nula não permitida**  
 Especifique a ação a ser tomada quando chaves nulas não forem permitidas, e uma chave nula for encontrada. Por padrão, este valor é **ReportAndContinue**.  
  
|Value|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignore o erro e continue o processamento.|  
|**ReportAndContinue**|Relate o erro e continue o processamento.|  
|**ReportAndStop**|Relate o erro e pare o processamento.|  
  
 **Caminho do log de erros**  
 Para selecionar um destino, digite o caminho do log de erros ou clique no botão **Procurar(…)**.  
  
 **Procurar (...)**  
 Selecione um caminho para o log de erros.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Destino de Processamento de Dimensões &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/dimension-processing-destination-editor-connection-manager-page.md)   
 [Editor de Destino de Processamento de Dimensões &#40;página Mapeamentos&#41;](../../integration-services/data-flow/dimension-processing-destination-editor-mappings-page.md)  
  
  