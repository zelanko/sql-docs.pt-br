---
title: Adicionar uma média móvel a um gráfico (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 166cf9c1-0750-4866-8381-542e4fbfe65a
caps.latest.revision: 5
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: a35eed078cf0b9317c7621f40ea3aaf51a836a41
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019075"
---
# <a name="add-a-moving-average-to-a-chart-report-builder-and-ssrs"></a>Adicionar uma média móvel a um gráfico (Construtor de Relatórios e SSRS)
  Uma média móvel é uma média dos dados na série, calculada em um período de tempo definido. A média móvel pode ser mostrada no gráfico para identificar tendências significativas.  
  
 A fórmula Média Móvel é o indicador de preço mais popular usado em análises técnicas. Muitas outras fórmulas, incluindo desvio médio, mediano e padrão, também podem ser derivadas de uma série no gráfico. Ao especificar uma média móvel, cada fórmula pode ter um ou mais parâmetros que devem ser especificados.  
  
 Quando uma fórmula de média móvel é adicionada em Modo de design, a série de linhas adicionada é apenas um espaço reservado visual. O gráfico calcula os pontos de dados de cada fórmula durante o processamento de relatório.  
  
 O suporte interno para linhas de tendência não está disponível no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-calculated-moving-average-to-a-series-on-the-chart"></a>Para adicionar uma média móvel calculada a uma série no gráfico  
  
1.  Clique com o botão direito do mouse na área **Valores** e clique em **Adicionar Série Calculada**. A caixa de diálogo **Propriedades da Série Calculada** é exibida.  
  
2.  Selecione a opção **Média Móvel** na lista suspensa **Fórmula** .  
  
3.  Especifique um valor inteiro para o **Período** que representa o período da média móvel.  
  
    > [!NOTE]  
    >  O período é o número de dias usado para calcular uma média móvel. Se os valores de data/hora não forem especificados no eixo x, o período será representado pelo número de pontos de dados usados para calcular uma média móvel. Se houver apenas um ponto de dados, a fórmula da média móvel não será calculada. A média móvel é calculada a partir do segundo ponto. Se a opção **Iniciar no primeiro ponto** estiver especificada, o gráfico iniciará a média móvel no primeiro ponto. Se houver apenas um ponto de dados, o ponto na média móvel calculada será idêntico ao primeiro ponto na série original.  
  
## <a name="see-also"></a>Consulte também  
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Adicionar pontos vazios ao gráfico &#40;SSRS e construtor de relatórios&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)  
  
  