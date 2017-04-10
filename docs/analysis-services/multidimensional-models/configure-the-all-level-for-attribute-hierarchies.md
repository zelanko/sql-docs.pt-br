---
title: "Configurar o n&#237;vel (All) para hierarquias de atributo | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Todos os membros"
  - "propriedade IsAggregatable"
  - "níveis mais altos [Analysis Services]"
  - "níveis (All)"
  - "propriedade AttributeAllMemberName"
  - "níveis [Analysis Services]"
  - "membros [Analysis Services], todos"
  - "propriedade AllMemberName"
ms.assetid: 0cb35e6f-b10f-483d-b893-78f6ca3979fd
caps.latest.revision: 33
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Configurar o n&#237;vel (All) para hierarquias de atributo
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o nível (All) é um nível opcional gerado pelo sistema. Contém apenas um membro, cujo valor é a agregação de valores de todos os membros do nível imediatamente subordinado. Este membro é chamado de membro All. Trata-se de um membro gerado pelo sistema e que não é incluído na tabela de dimensões. Como o membro do nível (All) está no topo da hierarquia, seu valor é a agregação consolidada dos valores de todos os membros da hierarquia. Geralmente, o membro All funciona como membro padrão de uma hierarquia.  
  
 A existência de um nível (All) em uma hierarquia de atributos depende da configuração da propriedade **IsAggregatable** do atributo e a existência de um nível (All) na hierarquia definida pelo usuário depende da propriedade **IsAggregatable** do atributo em seu nível mais alto. Se a propriedade **IsAggregatable** estiver definida como **True**, haverá um nível (All). Uma hierarquia não terá nenhum nível (All) se a propriedade **IsAggregatable** estiver definida como **False**.  
  
## Estabelecendo o nível mais alto  
 Se a propriedade **IsAggregatable** estiver definida como **False** no atributo de origem de um nível da hierarquia, nenhum nível agregável poderá aparecer acima dele na hierarquia. Um nível não agregável deve ser o nível mais alto de qualquer hierarquia ou a propriedade **IsAggregatable** dos atributos de origem de todos os níveis acima dele também deve ser definida como **False**.  
  
## Membro e nível (All)  
 O único membro do nível (All) é chamado de membro All. A propriedade **AttributeAllMemberName** em uma dimensão especifica o nome do membro All para os atributos em uma dimensão. A propriedade **AllMemberName** em uma hierarquia especifica o nome do membro All da hierarquia.  
  
## Consulte também  
 [Definir um membro padrão](../../analysis-services/multidimensional-models/define-a-default-member.md)  
  
  