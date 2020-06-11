---
title: Restringir linhas (Assistente para partições) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.typefilterexpression.f1
ms.assetid: eec8da8f-eab4-4ac4-a81d-995c814f88ca
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4207f617b4f6fafde5392fdea013196c54501314
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547428"
---
# <a name="restrict-rows-partition-wizard"></a>Restringir linhas (Assistente para Partições)
  Use a página **Restringir Linhas** para restringir as linhas que serão recuperadas da tabela especificada e agregadas e incluídas na partição.  
  
> [!NOTE]  
>   Essa página será exibida apenas se você tiver selecionado uma única tabela na página **Especificar Informações sobre a Origem** .  
  
> [!CAUTION]  
>   Se você tiver especificado uma tabela em **Tabelas Disponíveis** na página **Especificar Informações sobre a Origem** que seja usada por outra partição, deverá fornecer uma consulta na página **Restringir Linhas** ou arriscar a duplicação de dados no cubo.  
  
## <a name="options"></a>Opções  
 **Especificar uma consulta para restringir linhas**  
 Selecione para inserir uma consulta que restrinja linhas na caixa **Consulta** .  
  
 Se o campo **Fornecer uma cláusula WHERE** estiver vazio quando essa opção for selecionada, essa opção será preenchida com uma instrução SQL que recupera todas as linhas da tabela selecionada anteriormente.  
  
 **Consulta**  
 Digite ou modifique a instrução SQL usada ao recuperar linhas da tabela quando a partição é processada.  
  
> [!IMPORTANT]  
>  Ao especificar uma cláusula WHERE, um subconjunto de registros pode ser usado para esta partição. Isso é essencial para evitar duplicação de dados quando várias partições estiverem baseadas em uma única tabela de fatos.  
  
 **Verificação**  
 Verifica se a instrução em **Consulta** é uma instrução SQL válida.  
  
## <a name="see-also"></a>Consulte Também  
 [Partições &#40;Analysis Services – Dados Multidimensionais&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
