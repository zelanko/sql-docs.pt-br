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
ms.topic: conceptual
helpviewer_keywords:
- user-defined hierarchies [Analysis Services]
ms.assetid: 16715b85-0630-4a8e-99b0-c0d213cade26
caps.latest.revision: 21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0521dfa594668d4133cb3c64de539024e2f49c6c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37289752"
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
  
  
