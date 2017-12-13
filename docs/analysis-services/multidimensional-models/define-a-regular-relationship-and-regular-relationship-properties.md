---
title: "Definir uma relação Regular e propriedades de relação Regular | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- granularity attribute
- relationships [Analysis Services], regular relationships
ms.assetid: 840280d8-20c3-46c0-99ea-62479469c36b
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 10025f3c362a0be45d782644ca36a41661e13c68
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="define-a-regular-relationship-and-regular-relationship-properties"></a>Definir uma relação regular e propriedades de relação regular
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Quando você define uma nova dimensão de cubo ou um novo grupo de medidas, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tentará detectar se existe uma relação regular e, em seguida, defina a configuração de uso de dimensão como **Regular**. É possível exibir ou editar uma relação de dimensão regular na guia **Uso da Dimensão** do Designer de Cubo.  
  
 Ao definir a relação de uma dimensão de cubo para um grupo de medidas, você pode especificar também a granularidade do atributo dessa relação. O atributo de granularidade define o nível mais detalhado disponível no cubo para essa dimensão, que, geralmente, é o atributo de chave da dimensão. Contudo, às vezes, convém definir a granularidade de uma determinada dimensão de cubo de um grupo de medidas em particular com outro nível de granularidade. Por exemplo, talvez você queira definir o atributo de granularidade da dimensão Tempo como Mês em vez de Dia se estiver usando o grupo de medidas Cotas de Vendas ou Orçamento. Ao especificar o atributo de granularidade com outro atributo que não seja o atributo de chave, você deve assegurar que todos os demais atributos da dimensão estejam direta ou indiretamente vinculados a esse outro atributo através de relações de atributo. Caso contrário, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não poderá agregar os dados corretamente.  
  
  
