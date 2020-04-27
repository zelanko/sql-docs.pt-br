---
title: Adicionar pontos vazios ao gráfico (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2b056119-439f-494f-83cf-ee0c05dc6487
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 59c79d4824c7df4709c571d5d46476fd89f3cbe4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106604"
---
# <a name="add-empty-points-to-the-chart-report-builder-and-ssrs"></a>Adicionar pontos vazios ao gráfico (Construtor de Relatórios e SSRS)
  Valores nulos são mostrados no gráfico como espaços vazios ou lacunas entre os pontos de dados em uma série. Pontos vazios são pontos de dados que podem ser inseridos em um espaço vazio criado por valores nulos.  
  
 Por padrão, pontos vazios são calculados pela média dos pontos de dados anteriores e seguintes que contêm um valor. Você pode alterar isso para que todos os pontos vazios sejam inseridos como zero.  
  
 Para obter mais informações, consulte [Pontos de dados vazios e nulos em gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-empty-points-on-a-chart"></a>Para especificar pontos vazios em um gráfico  
  
1.  Abra o painel Propriedades.  
  
2.  Na superfície de design, clique com o botão direito do mouse na série que contém valores nulos. As propriedades da série são exibidas no painel Propriedades.  
  
3.  Expanda o nó **EmptyPoint** .  
  
4.  Selecione um valor de cor para a propriedade Color.  
  
5.  No nó **EmptyPoint** , expanda o nó Marker.  
  
6.  Selecione um tipo de marcador para a propriedade MarkerType.  
  
    > [!NOTE]  
    >  Você deve selecionar um tipo de marcador para adicionar pontos vazios a um gráfico de barras, colunas ou de dispersão. No entanto, para gráficos de área, linha e radar, a seleção de um tipo de marcador é opcional porque o gráfico preenche o espaço vazio ou a lacuna sem precisar da especificação de um marcador.  
  
7.  Defina o valor do ponto vazio.  
  
    1.  No painel Propriedades, expanda o nó **CustomAttributes** .  
  
    2.  Defina a propriedade EmptyPointValue. Para inserir pontos vazios em uma média dos pontos de dados anteriores e seguintes, selecione **Média**. Para inserir pontos vazios em zero, selecione **Zero**.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Tipos de gráficos &#40;Construtor de Relatórios e SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [Adicionar quebras de escala a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](add-scale-breaks-to-a-chart-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
