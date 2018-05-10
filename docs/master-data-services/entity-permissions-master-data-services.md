---
title: Permissões de entidade (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], permissions
- permissions [Master Data Services], entities
ms.assetid: 22785062-4faf-46ee-bffa-01cbd6d5a5b3
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 69ec91fb58dc323d264e167593f4117cba81eebf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="entity-permissions-master-data-services"></a>Permissões de entidade (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  As permissões de entidade se aplicam a:  
  
-   Todos os atributos da entidade, inclusive **Name** e **Code**, para os membros folha e consolidados.  
  
-   Todas as coleções da entidade.  
  
-   Associações de hierarquia explícitas e relações.  
  
 Quando tem permissão para uma entidade, você pode adicionar e remover membros da entidade, de suas hierarquias explícitas e de suas coleções.  
  
> [!NOTE]  
>  Essas permissões se aplicam apenas à área funcional **Explorer** da interface do usuário.  
  
|Permissão|Description|  
|----------------|-----------------|  
|**Leitura**|O usuário pode ler membros, atributos, associações de hierarquia ou hierarquias de coleção.|  
|**Criar**|O usuário pode criar membros e atribuir valores de atributo durante a criação.|  
|**Update (atualizar)**|O usuário pode atualizar membros, atributos, associações de hierarquia ou hierarquias de coleção.|  
|**Delete (excluir)**|O usuário pode excluir membros.|  
|**Deny**|Nega todo o acesso à entidade.|  
  
 As permissões Ler, Criar, Atualizar e Excluir podem ser combinadas entre si. Ao atribuir permissões Criar, Atualizar e Excluir, a permissão Ler será atribuída automaticamente.  
  
## <a name="see-also"></a>Consulte Também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
