---
title: "Criar hierarquias definidas pelo usuário | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user-defined hierarchies [Analysis Services]
ms.assetid: 16715b85-0630-4a8e-99b0-c0d213cade26
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51e4bcb074da0b11587d8783008fd250fa8867fe
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="user-defined-hierarchies---create"></a>Criar hierarquias definidas pelo usuário-
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite a criação de hierarquias definidas pelo usuário. Uma hierarquia é uma coleção de níveis com base em atributos. Por exemplo, uma hierarquia de tempo pode conter níveis de Ano, Trimestre, Mês, Semana e Dia. Em algumas hierarquias, cada atributo de membro implica exclusivamente o atributo do membro acima dele. Algumas vezes, isso é chamado de hierarquia natural. Uma hierarquia pode ser usada por usuários finais para procurar dados do cubo. Defina hierarquias usando o painel Hierarquias do Designer de Dimensão em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando você cria uma hierarquia definida pelo usuário, a hierarquia pode ficar *desbalanceada*. Uma hierarquia desbalanceada é local em que o membro pai lógico de pelo menos um membro não está no nível imediatamente acima do membro. Se você tiver uma hierarquia desbalanceada, existem configurações que controlam se os membros ausentes estão visíveis e como exibi-los. Para obter mais informações, consulte [Hierarquias desbalanceadas](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre problemas de desempenho relacionadas ao design e à configuração de hierarquias definidas pelo usuário, consulte o [Guia de desempenho do Analysis Services do SQL Server 2005 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades de hierarquia do usuário](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Propriedades de nível - hierarquias de usuário](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [Dimensões pai-filho](../../analysis-services/multidimensional-models/parent-child-dimension.md)  
  
  

