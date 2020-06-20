---
title: Editor de destino de processamento de dimensões (página avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimprocessingtransformation.advanced.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 2b30835a-2680-4d98-89a4-4f17e29e3818
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5bef21b424c401d77b9d8f3477de4061c3ff0f3d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966953"
---
# <a name="dimension-processing-destination-editor-advanced-page"></a>Editor de Destino de Processamento de Dimensões (página Avançado)
  Use a página **Avançado** da caixa de diálogo **Editor de Destino de Processamento de Dimensões** para configurar o tratamento de erros.  
  
 Para saber mais sobre o destino de Processamento de Dimensões, consulte [Dimension Processing Destination](data-flow/dimension-processing-destination.md).  
  
## <a name="options"></a>Opções  
 **Usar configuração de erro padrão.**  
 Especifique se a manipulação de erros padrão do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] deve ser usada. Por padrão, esse valor é `True`.  
  
 **Ação de erro de chave**  
 Especifique como manipular registros que possuem valores de chave inaceitáveis.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**ConvertToUnknown**|Converta o valor de chave inaceitável para o valor `UnknownMember`.|  
|**DiscardRecord**|Descarte o registro.|  
  
 **Ignorar erros**  
 Especifique se os erros devem ser ignorados.  
  
 **Parar se houver erro**  
 Especifique se o processamento deve parar quando ocorrer erro.  
  
 **Número de erros**  
 Caso tenha selecionado **Parar se houver erro**, especifique o limite de erros sob o qual o processamento deve parar.  
  
 **Ação se houver erro**  
 Caso tenha selecionado **Parar se houver erro**, especifique a ação a ser tomada quando o limite de erros for atingido.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**StopProcessing**|Pare o processamento.|  
|**StopLogging**|Pare de registrar os erros.|  
  
 **Chave não encontrada**  
 Especifique a ação a ser tomada mediante erro de chave não encontrada. Por padrão, este valor é **ReportAndContinue**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**IgnoreError**|Ignore o erro e continue o processamento.|  
|**ReportAndContinue**|Relate o erro e continue o processamento.|  
|**ReportAndStop**|Relate o erro e pare o processamento.|  
  
 **Chave duplicada**  
 Especifique a ação a ser tomada mediante erro de chave duplicada. Por padrão, esse valor é **IgnoreError**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**IgnoreError**|Ignore o erro e continue o processamento.|  
|**ReportAndContinue**|Relate o erro e continue o processamento.|  
|**ReportAndStop**|Relate o erro e pare o processamento.|  
  
 **Chave nula convertida em desconhecida**  
 Especifique a ação a ser tomada quando uma chave nula tiver sido convertida no valor `UnknownMember`. Por padrão, esse valor é **IgnoreError**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**IgnoreError**|Ignore o erro e continue o processamento.|  
|**ReportAndContinue**|Relate o erro e continue o processamento.|  
|**ReportAndStop**|Relate o erro e pare o processamento.|  
  
 **Chave nula não permitida**  
 Especifique a ação a ser tomada quando chaves nulas não forem permitidas, e uma chave nula for encontrada. Por padrão, este valor é **ReportAndContinue**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**IgnoreError**|Ignore o erro e continue o processamento.|  
|**ReportAndContinue**|Relate o erro e continue o processamento.|  
|**ReportAndStop**|Relate o erro e pare o processamento.|  
  
 **Caminho do log de erros**  
 Para selecionar um destino, digite o caminho do log de erros ou clique no botão **Procurar(...)**.  
  
 **Procurar (...)**  
 Selecione um caminho para o log de erros.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de processamento de dimensões &#40;página Gerenciador de conexões&#41;](../../2014/integration-services/dimension-processing-destination-editor-connection-manager-page.md)   
 [Editor de Destino de Processamento de Dimensões &#40;página Mapeamentos&#41;](../../2014/integration-services/dimension-processing-destination-editor-mappings-page.md)  
  
  
