---
description: Permissões de modelo (Master Data Services)
title: Permissões de modelo
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], permissions
- permissions [Master Data Services], models
ms.assetid: 210f440b-2cc1-4c49-94b1-3a97e2af7bc3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e195c4f2db244fa5cf647c19c0713f24840c3441
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461728"
---
# <a name="model-permissions-master-data-services"></a>Permissões de modelo (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  As permissões de modelo se aplicam a todas as entidades, hierarquias derivadas, hierarquias explícitas e coleções existentes dentro do modelo. As permissões atribuídas ao modelo podem ser substituídas para qualquer objeto individual.  
  
> [!NOTE]  
>  Se um usuário for administrador de modelo, o modelo será exibido em todas as áreas funcionais da interface do usuário. Caso contrário, o modelo será exibido apenas na área funcional **Gerenciador** . Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
|Permissão|Descrição|  
|----------------|-----------------|  
|**Ler**|O usuário pode ler membros, atributos, associações de hierarquia ou hierarquias de coleção.|  
|**Criar**|O usuário pode criar membros e atribuir valores de atributo durante a criação.|  
|**Atualização**|O usuário pode atualizar membros, atributos, associações de hierarquia ou hierarquias de coleção.|  
|**Delete (excluir)**|O usuário pode excluir membros.|  
|**Deny**|Nega todo o acesso ao modelo|  
|**Administrador**|Permissão de administrador no modelo. A permissão de administrador está disponível somente no nível do modelo.|  
  
 As permissões Ler, Criar, Atualizar e Excluir podem ser combinadas entre si. Ao atribuir permissões Criar, Atualizar e Excluir, a permissão Ler será atribuída automaticamente.  
  
## <a name="see-also"></a>Consulte Também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Permissões de entidade &#40;Master Data Services&#41;](../master-data-services/entity-permissions-master-data-services.md)   
 [Permissões de coleção &#40;Master Data Services&#41;](../master-data-services/collection-permissions-master-data-services.md)  
  
  
