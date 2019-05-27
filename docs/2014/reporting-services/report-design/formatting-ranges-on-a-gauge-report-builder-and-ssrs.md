---
title: Formatando intervalos de um medidor (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ffdec8ca-3e95-41cd-850b-9e8c83be4b49
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 29574c58eef6f18d685b48dd8d695a5fc42c3e6e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105806"
---
# <a name="formatting-ranges-on-a-gauge-report-builder-and-ssrs"></a>Formatando intervalos de um medidor (Construtor de Relatórios e SSRS)
  Um intervalo de medidor é uma zona ou área na escala de medidor que indica uma subseção importante de valores no medidor. Usando um intervalo de medidor, é possível indicar visualmente quando o valor de ponteiro entrou em um determinado conjunto de valores. Intervalos são definidos por um valor inicial e um valor final.  
  
 Você também pode usar intervalos para definir seções diferentes de um medidor. Por exemplo, em um medidor com valores entre 0 e 10, é possível definir um intervalo vermelho com valor entre 0 e 3, um amarelo com intervalo entre 4 e 7 e um verde com intervalo entre 8 e 10. Caso o valor inicial especificado seja maior que o valor final, os valores são trocados para que o inicial seja o final e vice-versa.  
  
 É possível posicionar o intervalo da mesma forma que posiciona ponteiros em uma escala. As propriedades **Posição** e **Distância da escala** determinam a posição do intervalo. Para obter mais informações, consulte [Medidores &#40;Construtor de Relatórios e SSRS&#41;](gauges-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Formatando escalas em um medidor &#40;Construtor de Relatórios e SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formatando ponteiros de um medidor &#40;Construtor de Relatórios e SSRS&#41;](formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Definir mínimo ou máximo em um medidor &#40;Construtor de Relatórios e SSRS&#41;](set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)   
 [Tutorial: Adicionar um KPI ao relatório &#40;Construtor de Relatórios&#41;](../tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
