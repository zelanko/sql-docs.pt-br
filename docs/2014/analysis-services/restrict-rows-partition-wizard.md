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
manager: craigg
ms.openlocfilehash: 59bff3eac690b7352b75d02bd7b266dfa8f303f8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070208"
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
  
  
