---
title: Configurar o nível (All) para hierarquias de atributo | Microsoft Docs
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
- All members
- IsAggregatable property
- topmost levels [Analysis Services]
- (All) levels
- AttributeAllMemberName property
- levels [Analysis Services]
- members [Analysis Services], All
- AllMemberName property
ms.assetid: 0cb35e6f-b10f-483d-b893-78f6ca3979fd
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e61b7606ab4a7c2418294133ad7c4f3b03672df1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122267"
---
# <a name="configure-the-all-level-for-attribute-hierarchies"></a>Configurar o nível (All) para hierarquias de atributo
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o nível (All) é um nível opcional gerado pelo sistema. Contém apenas um membro, cujo valor é a agregação de valores de todos os membros do nível imediatamente subordinado. Este membro é chamado de membro All. Trata-se de um membro gerado pelo sistema e que não é incluído na tabela de dimensões. Como o membro do nível (All) está no topo da hierarquia, seu valor é a agregação consolidada dos valores de todos os membros da hierarquia. Geralmente, o membro All funciona como membro padrão de uma hierarquia.  
  
 A presença de um nível (All) em uma hierarquia de atributo depende de `IsAggregatable` depende de configuração de propriedade para o atributo e a presença de um nível (All) em uma hierarquia definida pelo usuário a `IsAggregatable` propriedade do atributo no nível mais alto de hierarquia definida pelo usuário. Se a propriedade `IsAggregatable` for definida como `True`, existirá um nível (All). A hierarquia não terá um nível (All) se a propriedade `IsAggregatable` estiver configurada como `False`.  
  
## <a name="establishing-the-topmost-level"></a>Estabelecendo o nível mais alto  
 Se a propriedade `IsAggregatable` estiver configurada como `False` no atributo de origem de um nível da hierarquia, nenhum nível agregável pode aparecer acima dele na hierarquia. Um nível não agregável deve ser o nível mais alto de qualquer hierarquia ou a propriedade `IsAggregatable` dos atributos de origem de todos os níveis acima dele também deve ser configurada como `False`.  
  
## <a name="all-member-and-all-level"></a>Membro e nível (All)  
 O único membro do nível (All) é chamado de membro All. O `AttributeAllMemberName`propriedade em uma dimensão especifica o nome do membro All para atributos em uma dimensão. A propriedade `AllMemberName` em uma hierarquia especifica o nome do membro All para seus atributos.  
  
## <a name="see-also"></a>Consulte também  
 [Definir um membro padrão](attribute-properties-define-a-default-member.md)  
  
  