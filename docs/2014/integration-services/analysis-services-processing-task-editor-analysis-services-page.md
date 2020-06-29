---
title: Editor da tarefa de processamento de Analysis Services (página Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asprocessingtask.as.f1
helpviewer_keywords:
- Analysis Services Processing Task Editor
ms.assetid: 5612be78-57cf-4e4e-92cf-6bfa9f971040
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0ab462b751215ed6573de20764f3dee0715e5f33
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439463"
---
# <a name="analysis-services-processing-task-editor-analysis-services-page"></a>Editor da Tarefa Processamento do Analysis Services (página Analysis Services)
  Use a página **Analysis Services** da caixa de diálogo **Editor da Tarefa Processamento do Analysis Services** para especificar um gerenciador de conexões do Analysis Services, selecione os objetos analíticos a serem processados e defina as opções de processamento e manipulação de erros.  
  
 Lembre-se do seguinte quando for processar modelos tabulares:  
  
1.  Você não pode executar a análise de impacto em modelos tabulares.  
  
2.  Algumas opções de processamento para modo tabular não são expostas, como Processar Desfragmentação e Processar Recálculo. Você pode executar essas funções usando a tarefa Executar DDL.  
  
3.  Algumas opções de processamento fornecidas, como índices de processo, não são apropriadas para modelos tabulares e não devem ser usadas.  
  
4.  As configurações de lote para modelos tabulares são ignoradas.  
  
 Para obter informações sobre essa tarefa, consulte [Analysis Services Processing Task](control-flow/analysis-services-processing-task.md).  
  
## <a name="options"></a>Opções  
 **Gerenciador de conexões Analysis Services**  
 Selecione na lista um gerenciador de conexões do Analysis Services existente ou clique em **Novo** para criar um novo gerenciador de conexões.  
  
 **Novo**  
 Cria um novo gerenciador de conexões do Analysis Services  
  
 **Tópicos relacionados:** [Analysis Services Connection Manager](connection-manager/analysis-services-connection-manager.md), [Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **Lista de objetos**  
 |Propriedade|Descrição|  
|--------------|-----------------|  
|**Object Name**|Lista os nomes de objeto especificados.|  
|**Tipo**|Lista os tipos dos objetos especificados.|  
|**Opções de Processo**|Selecione uma opção de processamento na lista.<br /><br /> **Tópicos relacionados**: [processamento de objeto de modelo multidimensional](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services)|  
|**Configurações**|Lista configurações de processamento para os objetos especificados.|  
  
 **Adicionar**  
 Adicione à lista um objeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 **Removerr**  
 Selecione um objeto e clique em **Excluir**.  
  
 **Análise de Impacto**  
 Execute uma análise de impacto no objeto selecionado.  
  
 **Tópicos relacionados:** [Caixa de diálogo Análise de Impacto &#40;Analysis Services – Dados Multidimensionais&#41;](../../2014/analysis-services/impact-analysis-dialog-box-analysis-services-multidimensional-data.md)  
  
 **Resumo de Configurações de Lote**  
 |Propriedade|Descrição|  
|--------------|-----------------|  
|**Ordem de processamento**|Especifica se os objetos são processados em sequência ou em um lote; se for usado o processamento paralelo, especifica o número de objetos a serem processados simultaneamente.|  
|**Modo de transação**|Especifica o modo da transação para processamento sequencial.|  
|**Erros de dimensão**|Especifica o comportamento da tarefa quando ocorrem erros.|  
|**Caminho do log de erros da chave de dimensão**|Especifica o caminho do arquivo no qual são feitos logs de erros.|  
|**Objetos afetados pelo processo**|Indica se também são processados objetos dependentes ou afetados.|  
  
 **Alterar configurações**  
 Altere as opções de processamento e a manipulação de erros em chaves de dimensão.  
  
 **Tópicos relacionados:** [Caixa de diálogo Alterar Configurações &#40;Analysis Services – Dados Multidimensionais&#41;](../../2014/analysis-services/change-settings-dialog-box-analysis-services-multidimensional-data.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa de processamento de Analysis Services &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Tarefa Executar DDL do Analysis Services](control-flow/analysis-services-execute-ddl-task.md)  
  
  
