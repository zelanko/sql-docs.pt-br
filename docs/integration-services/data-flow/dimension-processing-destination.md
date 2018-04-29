---
title: Destino de processamento de dimensões | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.dimensionprocessingdest.f1
- sql13.dts.designer.dimprocessingtransformation.connection.f1
- sql13.dts.designer.dimprocessingtransformation.mappings.f1
- sql13.dts.designer.dimprocessingtransformation.advanced.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0cd52f33fc861b5b59055fc9c1bbe8840e46fc81
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="dimension-processing-destination"></a>Destino de processamento de dimensões
  O Destino de Processamento de Dimensões carrega e processa uma dimensão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para obter mais informações sobre dimensões, consulte [Dimensões &#40;Analysis Services – Dados Multidimensionais&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md).  
  
 O Destino de Processamento de Dimensões inclui os seguintes recursos:  
  
-   Opções para executar o processamento incremental, completo ou atualizado.  
  
-   Configuração de erro, para especificar se o processamento de dimensões ignora erros ou é interrompido depois de um determinado número de erros.  
  
-   Mapeamento de colunas de entrada para colunas nas tabelas de dimensão.  
  
 Para obter mais informações sobre processamento de objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>Configuração do o destino Processamento de Dimensão  
 O Destino de Processamento de Dimensões usa um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para se conectar ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém as dimensões processadas pelo destino. Para obter mais informações, consulte [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Esse destino tem uma entrada. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="dimension-processing-destination-editor-connection-manager-page"></a>Editor de Destino de Processamento de Dimensões (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino de Processamento de Dimensões** para especificar uma conexão com um projeto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou com uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
### <a name="options"></a>Opções  
 **Connection manager**  
 Selecione um gerenciador de conexões existente na lista ou clique em **Novo** para criar um novo gerenciador de conexões.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Adicionar Gerenciador de Conexões do Analysis Services** .  
  
 **Lista de dimensões disponíveis**  
 Selecione a dimensão a processar.  
  
 **Método de processamento**  
 Selecione o método de processamento a aplicar à dimensão selecionada na lista. O valor padrão desta opção é **Completo**.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Adicionar (incremental)**|Execute um processamento com incremento da dimensão.|  
|**Completo**|Execute um processamento completo da dimensão.|  
|**Update (atualizar)**|Execute um processamento de atualização da dimensão.|  
  
## <a name="dimension-processing-destination-editor-mappings-page"></a>Editor de Destino de Processamento de Dimensões (página Mapeamentos)
  Use a página **Mapeamentos** da caixa de diálogo **Editor de Destino de Processamento de Dimensões** para mapear colunas de entrada para colunas de dimensão.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Exiba a lista das colunas de entrada disponíveis. Use uma operação de arrastar e soltar para mapear colunas de entrada disponíveis na tabela para as colunas de destino.  
  
 **Colunas de Destino Disponíveis**  
 Exiba a lista de colunas de destino disponíveis. Use uma operação de arrastar e soltar para mapear as colunas de destino disponíveis na tabela para as colunas de entrada.  
  
 **Coluna de Entrada**  
 Exibir colunas de entrada selecionadas na tabela acima. É possível alterar os mapeamentos usando a lista **Colunas de Entrada Disponíveis**.  
  
 **Coluna de Destino**  
 Exibe cada coluna de destino disponível, e se ela é mapeada ou não.  
  
## <a name="dimension-processing-destination-editor-advanced-page"></a>Editor de Destino de Processamento de Dimensões (página Avançado)
  Use a página **Avançado** da caixa de diálogo **Editor de Destino de Processamento de Dimensões** para configurar o tratamento de erros.  
  
### <a name="options"></a>Opções  
 **Usar configuração de erro padrão.**  
 Especifique se a manipulação de erros padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve ser usada. Por padrão, esse valor está definido como **True**.  
  
 **Ação de erro de chave**  
 Especifique como manipular registros que possuem valores de chave inaceitáveis.  
  
|Valor|Description|  
|-----------|-----------------|  
|**ConvertToUnknown**|Converta o valor de chave inaceitável em um valor **UnknownMember** .|  
|**DiscardRecord**|Descarte o registro.|  
  
 **Ignorar erros**  
 Especifique se os erros devem ser ignorados.  
  
 **Parar se houver erro**  
 Especifique se o processamento deve parar quando ocorrer erro.  
  
 **Número de erros**  
 Caso tenha selecionado **Parar se houver erro**, especifique o limite de erros sob o qual o processamento deve parar.  
  
 **Ação se houver erro**  
 Caso tenha selecionado **Parar se houver erro**, especifique a ação a ser tomada quando o limite de erros for atingido.  
  
|Valor|Description|  
|-----------|-----------------|  
|**StopProcessing**|Pare o processamento.|  
|**StopLogging**|Pare de registrar os erros.|  
  
 **Chave não encontrada**  
 Especifique a ação a ser tomada mediante erro de chave não encontrada. Por padrão, este valor é **ReportAndContinue**.  
  
|Valor|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignore o erro e continue o processamento.|  
|**ReportAndContinue**|Relate o erro e continue o processamento.|  
|**ReportAndStop**|Relate o erro e pare o processamento.|  
  
 **Chave duplicada**  
 Especifique a ação a ser tomada mediante erro de chave duplicada. Por padrão, esse valor é **IgnoreError**.  
  
|Valor|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignore o erro e continue o processamento.|  
|**ReportAndContinue**|Relate o erro e continue o processamento.|  
|**ReportAndStop**|Relate o erro e pare o processamento.|  
  
 **Chave nula convertida em desconhecida**  
 Especifique a ação a ser tomada quando uma chave nula foi convertida no valor **UnknownMember** . Por padrão, esse valor é **IgnoreError**.  
  
|Valor|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignore o erro e continue o processamento.|  
|**ReportAndContinue**|Relate o erro e continue o processamento.|  
|**ReportAndStop**|Relate o erro e pare o processamento.|  
  
 **Chave nula não permitida**  
 Especifique a ação a ser tomada quando chaves nulas não forem permitidas, e uma chave nula for encontrada. Por padrão, este valor é **ReportAndContinue**.  
  
|Valor|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignore o erro e continue o processamento.|  
|**ReportAndContinue**|Relate o erro e continue o processamento.|  
|**ReportAndStop**|Relate o erro e pare o processamento.|  
  
 **Caminho do log de erros**  
 Para selecionar um destino, digite o caminho do log de erros ou clique no botão **Procurar(…)** .  
  
 **Procurar (...)**  
 Selecione um caminho para o log de erros.  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
