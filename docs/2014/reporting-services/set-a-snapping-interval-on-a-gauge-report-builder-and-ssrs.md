---
title: Definir um intervalo de ajuste em um medidor (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0ece7297-6e2f-47fb-835d-b9e9cce53fe2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3e2a35e4d6fefb6830774ffd7b2c3bc13a5e097c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101372"
---
# <a name="set-a-snapping-interval-on-a-gauge-report-builder-and-ssrs"></a>Definir um intervalo de ajuste em um medidor (Construtor de Relatórios e SSRS)
  Um intervalo de ajuste define o múltiplo para o qual os valores são arredondados. Por padrão, o medidor apontará para o valor exato do campo especificado no painel de dados. No entanto, talvez você queira arredondar o valor exato para cima ou para baixo para que o ponteiro se encaixe em um intervalo predefinido. Por exemplo, se o valor em seu medidor for 34,2 e você especificar um intervalo de ajuste de 5, o ponteiro do medidor apontará para 35. Se o valor em seu medidor for 31,2 e você especificar um intervalo de ajuste de 5, o ponteiro do medidor apontará para 30.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-snapping-interval-on-a-gauge"></a>Para definir um intervalo de ajuste em um medidor  
  
1.  Clique em qualquer parte dos números do medidor para realçar a escala.  
  
2.  Abra o painel Propriedades.  
  
    > [!NOTE]  
    >  Se você não vir o painel Propriedades, clique na guia **Exibir** e, em seguida, marque a caixa de seleção **Propriedades** .  
  
3.  Na propriedade **ponteiros** , clique no botão (...). O Editor de Coleção de Ponteiros é aberto.  
  
4.  Defina a propriedade **SnappingEnabled** como `True`.  
  
5.  Defina o **SnappingInterval** para um valor que representa o intervalo de ajuste. O ponteiro será ajustado para o múltiplo de arredondamento mais próximo do valor especificado.  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando escalas em um medidor &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formatando ponteiros em um medidor &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  
