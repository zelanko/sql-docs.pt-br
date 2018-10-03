---
title: Caixa de diálogo de partição (Analysis Services - dados multidimensionais) de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.mergepartition.f1
ms.assetid: 1c94e250-ee18-4f98-b112-985f6346102a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c18ffdaa50c6ee48896f2d2e6e65db46c8fe3349
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117410"
---
# <a name="merge-partition-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Partição de Mesclagem (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Partição de Mesclagem** no **SQL Server Management Studio** para mesclar partições para um grupo de medidas em um cubo. É possível exibir a caixa de diálogo **Partição de Mesclagem** clicando com o botão direito do mouse na pasta Partições ou em uma partição no **Explorador de Objetos** e selecionando **Partições de Mesclagem** no menu de contexto.  
  
## <a name="options"></a>Opções  
 **Servidor**  
 Selecione o nome da instância do Analysis Services que contém a partição de destino.  
  
 **Nome**  
 Selecione o nome de uma partição existente a ser usada como a partição de destino.  
  
 **Pasta**  
 Exibe o nome da pasta que contém a partição de destino, se a partição selecionada em Nome não usar a pasta padrão da instância do Analysis Services.  
  
 **Partições de origem**  
 Exibe uma grade contendo as partições de origem que podem ser mescladas na partição de destino.  
  
> [!NOTE]  
>  Somente partições no mesmo grupo de medidas que compartilham o mesmo design de agregação podem ser mescladas.  
  
 A grade contém as seguintes colunas:  
  
|coluna|Description|  
|------------|-----------------|  
|**Mesclagem**|Selecione para mesclar a partição de origem na partição de destino.|  
|**Nome da Partição**|Exibe o nome da partição de origem.|  
|**Último processamento**|Exibe a data e a hora nas quais a partição de origem foi processada pela última vez.|  
  
## <a name="see-also"></a>Consulte também  
 [Partições &#40;Analysis Services - dados multidimensionais&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Mesclar partições no Analysis Services &#40;SSAS - Multidimensional&#41;](multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  
