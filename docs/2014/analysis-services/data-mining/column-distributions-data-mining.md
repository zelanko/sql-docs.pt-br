---
title: Distribuições de coluna (mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- normal distribution type [data mining]
- uniform distribution type [data mining]
- columns [data mining], distributions
- log normal distribution type [data mining]
- continuous columns
- distributions [data mining]
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c7eab32f251b9622c6ac77febf2c004806c024b
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78174533"
---
# <a name="column-distributions-data-mining"></a>Distribuições de colunas (mineração de dados)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode definir distribuições de coluna em uma estrutura de mineração para afetar como os algoritmos processam os dados nessas colunas quando você cria modelos de mineração. Com relação a certos algoritmos, é útil definir a distribuição de colunas contínuas antes de processar o modelo, principalmente quando se sabe que as colunas contêm distribuições comuns de valores. Se as distribuições não estiverem definidas, os modelos de mineração resultantes poderão produzir previsões menos precisas do que se as distribuições estiverem definidas, uma vez que os algoritmos terão menos informações com as quais interpretar dados.

 Os algoritmos que estão disponíveis em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornecem suporte aos seguintes tipos de distribuição:

 `Normal`Os valores para a coluna contínua formam um histograma com uma distribuição normal.

 ![Histograma com distribuição normal](../media/normal-distribution.gif "Histograma com distribuição normal")

 `Log Normal`Os valores da coluna contínua formam um histograma, em que a curva é alongada na extremidade superior e é distorcida em direção à extremidade inferior.

 ![Histograma com distribuição normal de log](../media/log-normal-distribution.gif "Histograma com distribuição normal de log")

 `Uniform`Os valores para a coluna contínua formam uma curva plana, na qual todos os valores são igualmente prováveis.

 ![Histograma com distribuição uniforme](../media/uniform-distribution.gif "Histograma com distribuição uniforme")

 Para obter mais informações sobre os algoritmos fornecidos pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Algoritmos de Data Mining &#40;Analysis Services – Data Mining&#41;](data-mining-algorithms-analysis-services-data-mining.md).

## <a name="see-also"></a>Consulte Também
 [Tipos de conteúdo &#40;data mining&#41;](content-types-data-mining.md) [estruturas de mineração &#40;Analysis Services-Data Mining&#41;](mining-structures-analysis-services-data-mining.md) [métodos discretização &#40;](discretization-methods-data-mining.md) [distribuições](/sql/dmx/distributions-dmx)&#41;de mineração de dados &#40;[colunas da estrutura de mineração](mining-structure-columns.md) do DMX&#41;


