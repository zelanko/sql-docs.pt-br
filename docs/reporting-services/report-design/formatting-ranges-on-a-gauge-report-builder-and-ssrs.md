---
title: Formatando intervalos de um medidor (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: ffdec8ca-3e95-41cd-850b-9e8c83be4b49
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7b60a68faa90dc7fa6aa7a49ff55af799518784e
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43273380"
---
# <a name="formatting-ranges-on-a-gauge-report-builder-and-ssrs"></a>Formatando intervalos de um medidor (Construtor de Relatórios e SSRS)
 Em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , o intervalo do medidor é uma zona ou área na escala de medidor que indica uma subseção importante de valores no medidor. Usando um intervalo de medidor, é possível indicar visualmente quando o valor de ponteiro entrou em um determinado conjunto de valores. Intervalos são definidos por um valor inicial e um valor final.  
  
 Você também pode usar intervalos para definir seções diferentes de um medidor. Por exemplo, em um medidor com valores entre 0 e 10, é possível definir um intervalo vermelho com valor entre 0 e 3, um amarelo com intervalo entre 4 e 7 e um verde com intervalo entre 8 e 10. Caso o valor inicial especificado seja maior que o valor final, os valores são trocados para que o inicial seja o final e vice-versa.  
  
 É possível posicionar o intervalo da mesma forma que posiciona ponteiros em uma escala. As propriedades **Posição** e **Distância da escala** determinam a posição do intervalo. Para obter mais informações, consulte [Medidores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando escalas em um medidor &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formatando ponteiros de um medidor &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Definir mínimo ou máximo em um medidor &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)   
 [Tutorial: Adicionando um KPI ao relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
