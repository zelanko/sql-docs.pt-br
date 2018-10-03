---
title: Classificado colunas (mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content types [data mining]
- STDEV column
- VARIANCE column
- PROBABLILITY column
- PROBABILITY_STDEV column
- columns [data mining], classified
- classified columns [data mining]
- PROBABILITY_VARIANCE column
- SUPPORT column
ms.assetid: 68bf3b78-dc12-497c-898f-b43a45646123
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d4a0fc7a0eeb0cabd07a38f77d5024aac0eaebb8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193746"
---
# <a name="classified-columns-data-mining"></a>Colunas classificadas [mineração de dados]
  Quando você define uma coluna classificada, cria uma relação entre a coluna atual e outra coluna na estrutura de mineração. Os dados na coluna da estrutura de mineração que você designa como a coluna classificada contém informações categóricas que descrevem os valores em outra coluna na estrutura de mineração.  
  
 Por exemplo, suponha que você tenha duas colunas com dados numéricos: uma coluna, [Compras Anuais], contém as compras anuais totais por cliente durante um ano civil específico e a outra coluna, [Desvios Padrão], contém os desvios padrão para obter esses valores. Neste caso, você pode designar a coluna [Compras Anuais] como a coluna classificada e o modelo poderia usar esta relação na análise.  
  
> [!NOTE]  
>  Os algoritmos fornecidos no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não dão suporte ao uso de colunas classificadas; este recurso é fornecido para uso na criação de algoritmos personalizados.  
  
## <a name="defining-a-classified-column"></a>Definindo uma coluna classificada  
 O tipo de dados de uma coluna classificada deve ser `Long` ou `Double`.  
  
 A lista a seguir descreve os tipos de conteúdo para os quais o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte para colunas classificadas.  
  
 **PROBABILITY**  
 O valor na coluna é a probabilidade do valor associado e é um número entre 0 e 1.  
  
 **VARIANCE**  
 O valor na coluna é a variância do valor associado.  
  
 **STDEV**  
 O valor na coluna é o desvio padrão do valor associado.  
  
 **PROBABILITY_VARIANCE**  
 O valor na coluna é a variância da probabilidade para o valor associado.  
  
 **PROBABILITY_STDEV**  
 O valor na coluna é o desvio padrão da probabilidade para o valor associado.  
  
 **SUPPORT**  
 O valor na coluna é o peso ou o fator de replicação do caso do valor associado.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de conteúdo &#40;mineração de dados&#41;](content-types-data-mining.md)   
 [Estruturas de mineração &#40;Analysis Services - mineração de dados&#41;](mining-structures-analysis-services-data-mining.md)   
 [Tipos de dados &#40;mineração de dados&#41;](data-types-data-mining.md)  
  
  
