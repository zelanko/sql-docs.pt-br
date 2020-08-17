---
description: Permissões de entidade (Master Data Services)
title: Permissões de entidade
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], permissions
- permissions [Master Data Services], entities
ms.assetid: 22785062-4faf-46ee-bffa-01cbd6d5a5b3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b71ffdf22c3a6758ee81d92f5f25300784d73fff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88389182"
---
# <a name="entity-permissions-master-data-services"></a>Permissões de entidade (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  As permissões de entidade se aplicam a:  
  
-   Todos os atributos da entidade, inclusive **Name** e **Code**, para os membros folha e consolidados.  
  
-   Todas as coleções da entidade.  
  
-   Associações de hierarquia explícitas e relações.  
  
 Quando tem permissão para uma entidade, você pode adicionar e remover membros da entidade, de suas hierarquias explícitas e de suas coleções.  
  
> [!NOTE]  
>  Essas permissões se aplicam apenas à área funcional **Explorer** da interface do usuário.  
  
|Permissão|Descrição|  
|----------------|-----------------|  
|**Ler**|O usuário pode ler membros, atributos, associações de hierarquia ou hierarquias de coleção.|  
|**Criar**|O usuário pode criar membros e atribuir valores de atributo durante a criação.|  
|**Atualização**|O usuário pode atualizar membros, atributos, associações de hierarquia ou hierarquias de coleção.|  
|**Delete (excluir)**|O usuário pode excluir membros.|  
|**Deny**|Nega todo o acesso à entidade.|  
  
 As permissões Ler, Criar, Atualizar e Excluir podem ser combinadas entre si. Ao atribuir permissões Criar, Atualizar e Excluir, a permissão Ler será atribuída automaticamente.  
  
## <a name="see-also"></a>Consulte Também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
