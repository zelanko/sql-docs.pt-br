---
title: "Colunas classificadas [minera&#231;&#227;o de dados] | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "tipos de conteúdo (mineração de dados)"
  - "Coluna STDEV"
  - "Coluna VARIANCE"
  - "Coluna PROBABLILITY"
  - "Coluna PROBABILITY_STDEV"
  - "colunas [mineração de dados], classificadas"
  - "colunas classificadas [mineração de dados]"
  - "Coluna PROBABILITY_VARIANCE"
  - "Coluna SUPPORT"
ms.assetid: 68bf3b78-dc12-497c-898f-b43a45646123
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 26
---
# Colunas classificadas [minera&#231;&#227;o de dados]
  Quando você define uma coluna classificada, cria uma relação entre a coluna atual e outra coluna na estrutura de mineração. Os dados na coluna da estrutura de mineração que você designa como a coluna classificada contém informações categóricas que descrevem os valores em outra coluna na estrutura de mineração.  
  
 Por exemplo, suponha que você tenha duas colunas com dados numéricos: uma coluna, [Compras Anuais], contém as compras anuais totais por cliente durante um ano civil específico e a outra coluna, [Desvios Padrão], contém os desvios padrão para obter esses valores. Neste caso, você pode designar a coluna [Compras Anuais] como a coluna classificada e o modelo poderia usar esta relação na análise.  
  
> [!NOTE]  
>  Os algoritmos fornecidos no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não dão suporte ao uso de colunas classificadas; este recurso é fornecido para uso na criação de algoritmos personalizados.  
  
## Definindo uma coluna classificada  
 O tipo de dados de uma coluna classificada deve ser **Long** ou **Double**.  
  
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
  
## Consulte também  
 [Tipos de conteúdo &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Tipos de dados &#40;Mineração de dados&#41;](../../analysis-services/data-mining/data-types-data-mining.md)  
  
  