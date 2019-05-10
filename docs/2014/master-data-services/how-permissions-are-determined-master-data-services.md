---
title: Como as permissões são determinadas (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], determining permissions
ms.assetid: 1dc0b43a-d023-4e7d-b027-8b1459fd058c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2f92a270bb599c84f5d0b2bd85e713c3f406f81b
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479523"
---
# <a name="how-permissions-are-determined-master-data-services"></a>Como as permissões são determinadas (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], a maneira mais simples de configurar a segurança é atribuir permissões de objeto modelo a um grupo do qual o usuário é membro.  
  
 A segurança se torna mais complexa quando:  
  
-   As permissões de objeto modelo e de membro da hierarquia são atribuídas.  
  
-   O usuário pertence a grupos e a permissão é atribuída ao usuário e aos grupos.  
  
-   O usuário pertence a grupos e a permissão é atribuída a vários grupos.  
  
## <a name="permissions-assigned-to-a-single-group-or-user"></a>Permissões atribuídas a um único grupo ou usuário  
 Se você atribuir permissões a um único grupo ou usuário, as permissões serão determinadas com base no seguinte fluxo de trabalho.  
  
 ![mds_conc_security_no_overlap](../../2014/master-data-services/media/mds-conc-security-no-overlap.gif "mds_conc_security_no_overlap")  
  
### <a name="step-1-effective-attribute-permissions-are-determined"></a>Etapa 1: As permissões de atributo efetivas são determinadas.  
 A lista a seguir descreve como as permissões de atributo efetivas são determinadas:  
  
-   As permissões atribuídas a objetos modelo determinam quais atributos um usuário pode acessar.  
  
-   Todos os objetos modelo herdam automaticamente a permissão do objeto mais próximo em um nível alto da estrutura do modelo.  
  
-   Qualquer objeto no mesmo nível da entidade é negado implicitamente.  
  
-   Qualquer objeto em um nível mais alto recebe acesso de navegação. Para obter mais informações sobre o acesso de navegação, consulte [acesso de navegação &#40;Master Data Services&#41;](navigational-access-master-data-services.md).  
  
 Neste exemplo, **somente leitura** permissão é atribuída a uma entidade e essa permissão é herdada por seu atributo, que está em um nível inferior na estrutura do modelo. O modelo fornece acesso de navegação a essa entidade e seu atributo. A outra entidade no modelo não tem nenhuma permissão explícita atribuída e não herda nenhuma permissão, portanto, é negada implicitamente.  
  
 ![mds_conc_inheritance_model](../../2014/master-data-services/media/mds-conc-inheritance-model.gif "mds_conc_inheritance_model")  
  
### <a name="step-2-if-hierarchy-member-permissions-are-assigned-effective-member-permissions-are-determined"></a>Etapa 2: Se as permissões de membro de hierarquia forem atribuídas, as permissões de membro efetivas serão determinadas.  
 A lista a seguir descreve como as permissões de membro da hierarquia efetivas são determinadas:  
  
-   As permissões atribuídas a nós da hierarquia determinam quais membros um usuário pode acessar.  
  
-   Todos os nós de uma hierarquia herdam automaticamente a permissão do objeto mais próximo em um nível alto da estrutura da hierarquia.  
  
-   Qualquer nó no mesmo nível é negado implicitamente.  
  
-   Qualquer nó em níveis mais altos que não tenha permissões atribuídas é negado implicitamente.  
  
 Neste exemplo, **somente leitura** permissão é atribuída a um nó da hierarquia e essa permissão é herdada por um nó em um nível inferior na estrutura da hierarquia. A raiz não tem nenhuma permissão atribuída, portanto é negada implicitamente. O outro nó na estrutura da hierarquia não tem nenhuma permissão explícita atribuída e não herda nenhuma permissão, portanto, é negado implicitamente.  
  
 ![mds_conc_inheritance_hierarchy](../../2014/master-data-services/media/mds-conc-inheritance-hierarchy.gif "mds_conc_inheritance_hierarchy")  
  
### <a name="step-3-the-intersection-of-attribute-and-member-permissions-is-determined"></a>Etapa 3: A interseção das permissões de atributo e de membro é determinada.  
 Se as permissões de atributo efetivas forem diferentes das permissões de membro efetivas, as permissões deverão ser determinadas para cada valor de atributo individual. Para obter mais informações, consulte [Sobrepondo permissões de modelo e membro &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-model-and-member-permissions-master-data-services.md).  
  
## <a name="permissions-assigned-to-multiple-groups"></a>Permissões atribuídas a vários grupos  
 Se um usuário pertencer a um ou mais grupos e as permissões forem atribuídas ao usuário e aos grupos, o fluxo de trabalho se tornará mais complexo.  
  
 ![mds_conc_security_group_overlap](../../2014/master-data-services/media/mds-conc-security-group-overlap.gif "mds_conc_security_group_overlap")  
  
 Nesse caso, a sobreposição das permissões do usuário e do grupo deve ser resolvida antes das permissões do objeto modelo e do membro da hierarquia poderem ser comparadas. Para obter mais informações, consulte [Sobrepondo permissões de usuário e grupo &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-user-and-group-permissions-master-data-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Sobrepondo permissões de usuário e grupo &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-user-and-group-permissions-master-data-services.md)   
 [Sobrepondo permissões de modelo e membro &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-model-and-member-permissions-master-data-services.md)  
  
  
