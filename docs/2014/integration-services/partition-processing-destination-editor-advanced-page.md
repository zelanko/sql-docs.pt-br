---
title: Editor de destino de processamento de partições (página Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partprocessingtransformation.advanced.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 2039ee0f-069d-479d-90b2-2a12481b1162
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e3eee8a69013975f7bfe9febcfa85d8143dcef68
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62889964"
---
# <a name="partition-processing-destination-editor-advanced-page"></a>Editor de Destino de Processamento de Partições (página Avançado)
  Use a página **Avançado** da caixa de diálogo **Editor de Destino de Processamento de Partições** para configurar a manipulação de erros.  
  
 Para saber mais sobre o destino de Processamento de Partições, consulte [Partition Processing Destination](data-flow/partition-processing-destination.md).  
  
> [!NOTE]  
>  As tarefas descritas aqui não se aplicam a modelos de tabela do Analysis Services.  Você não pode mapear colunas de entrada para as colunas de partição em modelos de tabela. Você pode usar a tarefa Executar DDL do Analysis Services [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md) para processar a partição.  
  
## <a name="options"></a>Opções  
 **Usar configuração de erro padrão.**  
 Especifique se a manipulação de erros padrão do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] deve ser usada. Por padrão, esse valor está definido como `True`.  
  
 **Ação de erro de chave**  
 Especifique como manipular registros que possuem valores de chave inaceitáveis.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**ConvertToUnknown**|Converta o valor de chave inaceitável em um valor Desconhecido.|  
|**DiscardRecord**|Descarte o registro.|  
  
 **Ignorar erros**  
 Especifique se os erros devem ser ignorados.  
  
 **Parar se houver erro**  
 Especifique se o processamento deve parar quando ocorrer erro.  
  
 **Número de erros**  
 Especifique o limite de erros em que o processamento deve ser interrompido, caso tenha selecionado **Parar se houver erro**.  
  
 **Ação se houver erro**  
 Especifique a ação a ser tomada quando o limite de erros for atingido, caso tenha selecionado **Parar se houver erro**.  
  
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
 Especifique a ação a ser tomada quando uma chave nula foi convertida no valor Desconhecido. Por padrão, esse valor é **IgnoreError**.  
  
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
 Digite o caminho do log de erros ou selecione um destino usando o botão Procurar **(...)** .  
  
 **Procurar (...)**  
 Selecione um caminho para o log de erros.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Destino de Processamento de Partições &#40;Página Mapeamentos&#41;](../../2014/integration-services/partition-processing-destination-editor-mappings-page.md)  
  
  
