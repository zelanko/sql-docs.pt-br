---
title: "Configurar o nível (All) para hierarquias de atributo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 46870a942fad5b41d91177772175e9cad43fad0a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="database-dimensions---configure-the-all-level-for-attribute-hierarchies"></a>Dimensões de banco de dados - Configure o nível (All) para hierarquias de atributo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o nível (All) é um nível opcional, gerado pelo sistema. Contém apenas um membro, cujo valor é a agregação de valores de todos os membros do nível imediatamente subordinado. Este membro é chamado de membro All. Trata-se de um membro gerado pelo sistema e que não é incluído na tabela de dimensões. Como o membro do nível (All) está no topo da hierarquia, seu valor é a agregação consolidada dos valores de todos os membros da hierarquia. Geralmente, o membro All funciona como membro padrão de uma hierarquia.  
  
 A existência de um nível (All) em uma hierarquia de atributos depende da configuração da propriedade **IsAggregatable** do atributo e a existência de um nível (All) na hierarquia definida pelo usuário depende da propriedade **IsAggregatable** do atributo em seu nível mais alto. Se a propriedade **IsAggregatable** estiver definida como **True**, haverá um nível (All). Uma hierarquia não terá nenhum nível (All) se a propriedade **IsAggregatable** estiver definida como **False**.  
  
## <a name="establishing-the-topmost-level"></a>Estabelecendo o nível mais alto  
 Se a propriedade **IsAggregatable** estiver definida como **False** no atributo de origem de um nível da hierarquia, nenhum nível agregável poderá aparecer acima dele na hierarquia. Um nível não agregável deve ser o nível mais alto de qualquer hierarquia ou a propriedade **IsAggregatable** dos atributos de origem de todos os níveis acima dele também deve ser definida como **False**.  
  
## <a name="all-member-and-all-level"></a>Membro e nível (All)  
 O único membro do nível (All) é chamado de membro All. A propriedade **AttributeAllMemberName**em uma dimensão especifica o nome do membro All para os atributos em uma dimensão. A propriedade **AllMemberName** em uma hierarquia especifica o nome do membro All da hierarquia.  
  
## <a name="see-also"></a>Consulte Também  
 [Definir um membro padrão](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
