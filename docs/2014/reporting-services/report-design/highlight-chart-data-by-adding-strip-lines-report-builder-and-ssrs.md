---
title: Realçar dados do gráfico adicionando faixas (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: addd6137-4b6e-4e88-a7e8-9600fcd1ccce
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c50d242c7528485d5d21aa10f2680094628b484b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105717"
---
# <a name="highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs"></a>Realçar dados do gráfico adicionando faixas (Construtor de Relatórios e SSRS)
  As faixas são intervalos horizontais ou verticais que sombreiam o plano de fundo do gráfico em intervalos regulares ou personalizados. É possível usar faixas para:  
  
-   Melhorar a legibilidade para pesquisar valores individuais no gráfico. Especificar faixas em intervalos regulares para ajudar a separar pontos de dados ao ler o gráfico.  
  
-   Realçar datas que ocorrem em intervalos regulares. Por exemplo, em um relatório de vendas você pode usar faixas para identificar pontos de dados de fins de semana.  
  
-   Realçar um intervalo de chaves específico. Usando o exemplo anterior, é possível usar uma faixa para realçar o intervalo mais alto de vendas que esteja entre $80 e 100.  
  
 As faixas não são aplicáveis aos tipos de gráficos de Formas ou Polares.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-interlaced-strip-lines-at-regular-intervals-on-a-chart"></a>Para exibir faixas entrelaçadas em intervalos regulares de um gráfico  
  
1.  Para mostrar faixas horizontais, clique com o botão direito do mouse em o eixo de gráfico vertical e clique em **Propriedades VerticalAxis**.  
  
     Para mostrar faixas verticais, clique com o botão direito do mouse em o eixo de gráfico horizontal e clique em **Propriedades do Eixo Vertical**.  
  
2.  Selecione a opção **Usar entrelaçamento** . Faixas cinza são exibidas no gráfico.  
  
3.  (Opcional) Especifique uma cor para as faixas usando a lista suspensa **Cor** adjacente.  
  
### <a name="to-display-interlaced-strip-lines-at-custom-intervals-on-a-chart"></a>Para exibir faixas entrelaçadas em intervalos personalizados em um gráfico  
  
1.  Para mostrar faixas horizontais, clique com o botão direito do mouse em o eixo de gráfico vertical e clique em **Propriedades VerticalAxis**.  
  
     Para mostrar faixas verticais, clique com o botão direito do mouse em o eixo de gráfico horizontal e clique em **Propriedades do Eixo Vertical**.  
  
     As propriedades do eixo são exibidas na janela Propriedades.  
  
2.  Na seção **Aparência** do painel Propriedades da propriedade StripLines, clique no botão Editar Coleção (…) para abrir o **Editor de Coleções ChartStripLine**.  
  
3.  Clique em **Adicionar** para adicionar uma nova faixa à coleção.  
  
4.  Clique em StripWidth para especificar a largura da faixa, medida em polegadas no relatório. Se você estiver realçando datas ou horas, clique em StripWidthType e selecione um intervalo de tempo.  
  
5.  Digite um valor ou expressão para o Intervalo para especificar a frequência com que a faixa se repete.  Por exemplo, se você especificar um intervalo de 10, e a largura da faixa for 5, as faixas serão exibidas em valores de 0 a 5, 15 a 20, 30 a 35 e assim por diante.  
  
> [!NOTE]  
>  Por padrão, o Intervalo é definido como Automático, o que significa que o gráfico não calcula um intervalo para faixas personalizadas. O gráfico calculará intervalos para faixas apenas se o valor de um intervalo estiver definido.  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando rótulos dos eixos de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Adicionar uma média móvel a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)  
  
  
