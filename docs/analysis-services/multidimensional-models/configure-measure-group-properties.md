---
title: Configurar propriedades do grupo de medidas | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: properties [Analysis Services], measure groups
ms.assetid: fa66bdb6-60b8-413c-ac2a-00e4d09f60a2
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2f650fd897c68e10044a02d55c08f9545a0e6046
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="configure-measure-group-properties"></a>Configurar propriedades do grupo de medidas
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Grupos de medidas têm propriedades que permitem que você defina como função de grupos de medidas.  
  
## <a name="measure-group-properties"></a>Propriedades do grupo de medidas  
 As propriedades do grupo de medidas determinam o comportamento de todo o grupo de medidas e definem o comportamento padrão de determinadas propriedades das medidas de um grupo de medidas.  
  
|Propriedade|Definição|  
|--------------|----------------|  
|**AggregationPrefix**|Aplica-se ao armazenamento ROLAP. Atribui um prefixo comum às exibições indexadas no SQL Server, usado para armazenar agregações para as partições associadas a esse grupo de medidas.|  
|**DataAggregation**|Essa propriedade é reservada para uso futuro e atualmente não tem nenhum efeito. Portanto, é recomendável que você não modifique essa configuração.|  
|**Description**|Você pode usar essa propriedade para documentar o grupo de medidas.|  
|**ErrorConfiguration**|As definições configuráveis de tratamento de erros para tratamento de chaves duplicadas, chaves desconhecidas, chaves nulas, limites de erro, ação devido à detecção de erros, arquivo de log de erros. Consulte [Configuração de erros para cubo, partição e processamento da dimensão &#40;SSAS – multidimensional&#41;](../../analysis-services/multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md).|  
|**EstimatedRows**|Especifica o número de linhas estimado da tabela de fatos.|  
|**EstimatedSize**|Especifica o tamanho estimado (em bytes) do grupo de medidas.|  
|**ID**|Especifica o identificador do objeto.|  
|**IgnoreUnrelatedDimensions**|Determina se as dimensão não relacionadas são forçadas para seu nível superior quando os membros das dimensões que não estão relacionados ao grupo de medidas são incluídos em uma consulta. A configuração padrão é **True**.|  
|**Nome**|Nome da medida. Esta propriedade é somente leitura.|  
|**ProactiveCaching**|As definições configuráveis de tratamento de erros para tratamento de chaves duplicadas, chaves desconhecidas, chaves nulas, limites de erro, ação devido à detecção de erros, arquivo de log de erros.|  
|**ProcessingMode**|Indica se a indexação e a agregação devem ocorrer durante ou após o processamento. As opções são Regular e LazyAggregations. LazyAggregations pode ser usado para executar a agregação como uma tarefa em segundo plano.|  
|**ProcessingPriority**|Determina a prioridade de processamento do cubo durante as operações em segundo plano, como agregações lentas e indexação. O valor padrão é **0**.|  
|**StorageLocation**|O local de armazenamento do sistema de arquivos para o grupo de medidas. Se nenhum for especificado, o local será herdado do cubo que contém o grupo de medidas.|  
|**StorageMode**|O modo de armazenamento para o grupo de medidas. Os valores disponíveis são MOLAP, ROLAP ou HOLAP.|  
|**Tipo**|Especifica o tipo do grupo de medidas.|  
  
  
