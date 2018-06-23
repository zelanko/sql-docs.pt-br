---
title: Criar hierarquias definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- user-defined hierarchies [Analysis Services]
ms.assetid: 16715b85-0630-4a8e-99b0-c0d213cade26
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dad60d5fb8da346dfd6961274f872640843176a7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012787"
---
# <a name="create-user-defined-hierarchies"></a>Criar hierarquias definidas pelo usuário
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite a criação de hierarquias definidas pelo usuário. Uma hierarquia é uma coleção de níveis com base em atributos. Por exemplo, uma hierarquia de tempo pode conter níveis de Ano, Trimestre, Mês, Semana e Dia. Em algumas hierarquias, cada atributo de membro implica exclusivamente o atributo do membro acima dele. Algumas vezes, isso é chamado de hierarquia natural. Uma hierarquia pode ser usada por usuários finais para procurar dados do cubo. Defina hierarquias usando o painel Hierarquias do Designer de Dimensão em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando você cria uma hierarquia definida pelo usuário, a hierarquia pode ficar *desbalanceada*. Uma hierarquia desbalanceada é local em que o membro pai lógico de pelo menos um membro não está no nível imediatamente acima do membro. Se você tiver uma hierarquia desbalanceada, existem configurações que controlam se os membros ausentes estão visíveis e como exibi-los. Para obter mais informações, consulte [Hierarquias desbalanceadas](user-defined-hierarchies-ragged-hierarchies.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre problemas de desempenho relacionadas ao design e à configuração de hierarquias definidas pelo usuário, consulte o [Guia de desempenho do Analysis Services do SQL Server 2005 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades de hierarquia de usuário](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Propriedades de nível &#91;Paved Over&#93;](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [Hierarquia pai-filho](parent-child-dimension.md)  
  
  