---
title: Definir uma relação Regular e propriedades de relação Regular | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9ee79742f919d7f47ae73968666d96622e3429bc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022273"
---
# <a name="define-a-regular-relationship-and-regular-relationship-properties"></a>Definir uma relação regular e propriedades de relação regular
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando você definir uma nova dimensão de cubo e um novo grupo de medidas, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tentará detectar se existe uma relação regular e, em seguida, definirá o uso da dimensão como **Regular**. É possível exibir ou editar uma relação de dimensão regular na guia **Uso da Dimensão** do Designer de Cubo.  
  
 Ao definir a relação de uma dimensão de cubo para um grupo de medidas, você pode especificar também a granularidade do atributo dessa relação. O atributo de granularidade define o nível mais detalhado disponível no cubo para essa dimensão, que, geralmente, é o atributo de chave da dimensão. Contudo, às vezes, convém definir a granularidade de uma determinada dimensão de cubo de um grupo de medidas em particular com outro nível de granularidade. Por exemplo, talvez você queira definir o atributo de granularidade da dimensão Tempo como Mês em vez de Dia se estiver usando o grupo de medidas Cotas de Vendas ou Orçamento. Ao especificar o atributo de granularidade com outro atributo que não seja o atributo de chave, você deve assegurar que todos os demais atributos da dimensão estejam direta ou indiretamente vinculados a esse outro atributo através de relações de atributo. Caso contrário, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não poderá agregar os dados corretamente.  
  
  
