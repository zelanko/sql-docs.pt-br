---
title: Agregar o Editor de transformação (guia Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.aggregationtransformation.advanced.f1
helpviewer_keywords:
- Aggregate Transformation Editor
ms.assetid: 186a9736-2554-40a0-9cb2-877a8db5fde8
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 917bffe5d88b30ffe5a3d56b7e8776c4e66c0051
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119986"
---
# <a name="aggregate-transformation-editor-advanced-tab"></a>Editor de Transformação Agregação (guia Avançado)
  Use a guia **Avançado** da caixa de diálogo **Editor de Transformação Agregação** para definir propriedades de componentes, especificar agregações e definir propriedades de colunas de entrada e saída.  
  
> [!NOTE]  
>  As opções de contagem de chaves, escala de chave, contagem de chaves distintas e escala de chave distinta são aplicadas em nível de componente quando especificado na guia **Avançado** , em nível de saída quando especificado na exibição avançada da guia **Agregações** e em nível de coluna quando especificado na lista de colunas na parte inferior da guia **Agregações** .  
>   
>  Na transformação Agregação, **Chaves** e **Escala de Chave** fazem referência ao número de grupos que são esperados como resultado de uma operação **Agrupar porz** . **Chaves de distinção de contagem** e **Escala de distinção de contagem** fazem referência ao número de valores distintos que são esperados como resultado de uma operação de **Contagem de distinção** .  
  
 Para obter mais informações sobre a transformação Agregação, consulte [Aggregate Transformation](data-flow/transformations/aggregate-transformation.md).  
  
## <a name="options"></a>Opções  
 **Escala de Chave**  
 Especifique, opcionalmente, o número aproximado de chaves que a agregação espera. A transformação usa estas informações para otimizar seu tamanho de cache inicial. Por padrão, o valor desta opção é **Não Especificado**. Se for especificada a **Escala de chave** e o **Número de chaves** , o **Número de chaves** terá precedência.  
  
|Valor|Description|  
|-----------|-----------------|  
|Não Especificado|A propriedade **Escala de chave** não é usada.|  
|Baixa|A agregação pode gravar aproximadamente 500.000 chaves.|  
|Média|A agregação pode gravar aproximadamente 5.000.000 de chaves.|  
|Alta|A agregação pode gravar mais de 25.000.000 de chaves.|  
  
 **Número de chaves**  
 Especifique, opcionalmente, o número exato de chaves que a agregação espera. A transformação usa estas informações para otimizar seu tamanho de cache inicial. Se for especificada a **Escala de chave** e o **Número de chaves** , o **Número de chaves** terá precedência.  
  
 **Escala de distinção de contagem**  
 Especifique, opcionalmente, o número aproximado de valores de distinção que a agregação pode gravar. Por padrão, o valor desta opção é **Não Especificado**. Se for especificada a **Escala de Distinção de Contagem** e as **Chaves de Distinção de Contagem** , as **Chaves de Distinção de Contagem** terão precedência.  
  
|Valor|Description|  
|-----------|-----------------|  
|Não Especificado|A propriedade Escala de Distinção de Contagem não é usada.|  
|Baixa|A agregação pode gravar aproximadamente 500.000 valores de distinção.|  
|Média|A agregação pode gravar aproximadamente 5.000.000 valores distintos.|  
|Alta|A agregação pode gravar mais de 25.000.000 de valores de distinção.|  
  
 **Chaves de distinção de contagem**  
 Especifique, opcionalmente, o número exato de valores de distinção que a agregação pode gravar. Se for especificada a **Escala de Distinção de Contagem** e as **Chaves de Distinção de Contagem** , as **Chaves de Distinção de Contagem** terão precedência.  
  
 **Estender fator automaticamente**  
 Use um valor entre 1 e 100 para especificar a porcentagem pela qual a memória pode ser estendida durante a agregação. Por padrão, o valor desta opção é **25%**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformação de agregação &#40;guia agregações&#41;](../../2014/integration-services/aggregate-transformation-editor-aggregations-tab.md)   
 [Agregar valores em um conjunto de dados por meio da transformação Agregação](data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
  