---
title: Configurar propriedades do grupo de medidas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- properties [Analysis Services], measure groups
ms.assetid: fa66bdb6-60b8-413c-ac2a-00e4d09f60a2
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 279452ac51b16d66a5825893a34a94c4900c689d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119006"
---
# <a name="configure-measure-group-properties"></a>Configurar propriedades do grupo de medidas
  Os grupos de medidas têm propriedades que lhe permitem definir como eles funcionam.  
  
## <a name="measure-group-properties"></a>Propriedades do grupo de medidas  
 As propriedades do grupo de medidas determinam o comportamento de todo o grupo de medidas e definem o comportamento padrão de determinadas propriedades das medidas de um grupo de medidas.  
  
|Propriedade|Definição|  
|--------------|----------------|  
|`AggregationPrefix`|Aplica-se ao armazenamento ROLAP. Atribui um prefixo comum às exibições indexadas no SQL Server, usado para armazenar agregações para as partições associadas a esse grupo de medidas.|  
|`DataAggregation`|Essa propriedade é reservada para uso futuro e atualmente não tem nenhum efeito. Portanto, é recomendável que você não modifique essa configuração.|  
|`Description`|Você pode usar essa propriedade para documentar o grupo de medidas.|  
|`ErrorConfiguration`|As definições configuráveis de tratamento de erros para tratamento de chaves duplicadas, chaves desconhecidas, chaves nulas, limites de erro, ação devido à detecção de erros, arquivo de log de erros. Consulte [Configuração de erros para cubo, partição e processamento da dimensão &#40;SSAS – multidimensional&#41;](error-configuration-for-cube-partition-and-dimension-processing.md).|  
|`EstimatedRows`|Especifica o número de linhas estimado da tabela de fatos.|  
|`EstimatedSize`|Especifica o tamanho estimado (em bytes) do grupo de medidas.|  
|`ID`|Especifica o identificador do objeto.|  
|`IgnoreUnrelatedDimensions`|Determina se as dimensão não relacionadas são forçadas para seu nível superior quando os membros das dimensões que não estão relacionados ao grupo de medidas são incluídos em uma consulta. Configuração padrão é `True`.|  
|`Name`|Nome da medida. Esta propriedade é somente leitura.|  
|`ProactiveCaching`|As definições configuráveis de tratamento de erros para tratamento de chaves duplicadas, chaves desconhecidas, chaves nulas, limites de erro, ação devido à detecção de erros, arquivo de log de erros.|  
|`ProcessingMode`|Indica se a indexação e a agregação devem ocorrer durante ou após o processamento. As opções são Regular e LazyAggregations. LazyAggregations pode ser usado para executar a agregação como uma tarefa em segundo plano.|  
|`ProcessingPriority`|Determina a prioridade de processamento do cubo durante as operações em segundo plano, como agregações lentas e indexação. O valor padrão é **0**.|  
|`StorageLocation`|O local de armazenamento do sistema de arquivos para o grupo de medidas. Se nenhum for especificado, o local será herdado do cubo que contém o grupo de medidas.|  
|`StorageMode`|O modo de armazenamento para o grupo de medidas. Os valores disponíveis são MOLAP, ROLAP ou HOLAP.|  
|`Type`|Especifica o tipo do grupo de medidas.|  
  
  