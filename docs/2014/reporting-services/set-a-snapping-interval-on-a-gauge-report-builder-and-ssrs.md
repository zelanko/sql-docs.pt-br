---
title: Definir um intervalo de ajuste em um medidor (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0ece7297-6e2f-47fb-835d-b9e9cce53fe2
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 4ce2f81ddb04c088c909e07f6d842f53c35b3974
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019780"
---
# <a name="set-a-snapping-interval-on-a-gauge-report-builder-and-ssrs"></a>Definir um intervalo de ajuste em um medidor (Construtor de Relatórios e SSRS)
  Um intervalo de ajuste define o múltiplo para o qual os valores são arredondados. Por padrão, o medidor apontará para o valor exato do campo especificado no painel de dados. No entanto, você talvez queira arredondar o valor exato para cima ou para baixo, para que o ponteiro se ajuste a um intervalo predefinido. Por exemplo, se o valor em seu medidor for 34,2 e você especificar um intervalo de ajuste de 5, o ponteiro do medidor apontará para 35. Se o valor em seu medidor for 31,2 e você especificar um intervalo de ajuste de 5, o ponteiro do medidor apontará para 30.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-snapping-interval-on-a-gauge"></a>Para definir um intervalo de ajuste em um medidor  
  
1.  Clique em qualquer parte dos números do medidor para realçar a escala.  
  
2.  Abra o painel Propriedades.  
  
    > [!NOTE]  
    >  Se você não vir o painel Propriedades, clique no **exibição** guia e, em seguida, selecione o **propriedades** caixa de seleção.  
  
3.  No **ponteiros** propriedade, clique no botão (…). O Editor de Coleção de Ponteiros é aberto.  
  
4.  Definir o **SnappingEnabled** propriedade `True`.  
  
5.  Definir o **SnappingInterval** para um valor que representa o intervalo de ajuste. O ponteiro será ajustado para o múltiplo de arredondamento mais próximo do valor especificado.  
  
## <a name="see-also"></a>Consulte também  
 [Formatando escalas em um medidor &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formatando ponteiros de um medidor &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  