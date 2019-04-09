---
title: Criar hierarquias definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined hierarchies [Analysis Services]
ms.assetid: 16715b85-0630-4a8e-99b0-c0d213cade26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c35749671caabd8c6c61249d39bb3336257b1b8a
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59242484"
---
# <a name="create-user-defined-hierarchies"></a>Criar hierarquias definidas pelo usuário
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lets you create user-defined hierarchies. A hierarchy is a colpermite a criação de hierarquias definidas pelo usuário.rUma hierarquia é uma coleção de níveis com base em atributos.,Por exemplo, uma hierarquia de tempo pode conter níveis de Ano, Trimestre, Mês, Semana e Dia.hEm algumas hierarquias, cada atributo de membro implica exclusivamente o atributo do membro acima dele.rAlgumas vezes, isso é chamado de hierarquia natural.iUma hierarquia pode ser usada por usuários finais para procurar dados do cubo. Defina hierarquias usando o painel Hierarquias do Designer de Dimensão em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando você cria uma hierarquia definida pelo usuário, a hierarquia pode ficar *desbalanceada*. Uma hierarquia desbalanceada é local em que o membro pai lógico de pelo menos um membro não está no nível imediatamente acima do membro. Se você tiver uma hierarquia desbalanceada, existem configurações que controlam se os membros ausentes estão visíveis e como exibi-los. Para obter mais informações, consulte [Hierarquias desbalanceadas](user-defined-hierarchies-ragged-hierarchies.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre problemas de desempenho relacionadas ao design e à configuração de hierarquias definidas pelo usuário, consulte o [Guia de desempenho do Analysis Services do SQL Server 2005 Analysis Services](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades de hierarquia do usuário](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Propriedades de nível &#91;Paved Over&#93;](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [Hierarquia pai-filho](parent-child-dimension.md)  
  
  
