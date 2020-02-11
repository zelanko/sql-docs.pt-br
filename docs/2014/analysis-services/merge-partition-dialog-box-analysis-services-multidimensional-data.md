---
title: Caixa de diálogo partição de mesclagem (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.mergepartition.f1
ms.assetid: 1c94e250-ee18-4f98-b112-985f6346102a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26751f2cc00330716f160c115d0e839cc6d9527a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66077824"
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
  
 **Partições de Origem**  
 Exibe uma grade contendo as partições de origem que podem ser mescladas na partição de destino.  
  
> [!NOTE]  
>  Somente partições no mesmo grupo de medidas que compartilham o mesmo design de agregação podem ser mescladas.  
  
 A grade contém as seguintes colunas:  
  
|Coluna|DESCRIÇÃO|  
|------------|-----------------|  
|**Mesclagem**|Selecione para mesclar a partição de origem na partição de destino.|  
|**Nome da partição**|Exibe o nome da partição de origem.|  
|**Último Processamento**|Exibe a data e a hora nas quais a partição de origem foi processada pela última vez.|  
  
## <a name="see-also"></a>Consulte Também  
 [Partições &#40;Analysis Services de dados multidimensionais&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Mesclar partições em Analysis Services &#40;SSAS –&#41;multidimensional](multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  
