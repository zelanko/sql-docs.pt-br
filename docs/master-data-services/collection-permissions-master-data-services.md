---
description: Permissões de coleção (Serviços de Dados Mestre)
title: Permissões de coleção
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services], permissions
- permissions [Master Data Services], collections
ms.assetid: 703e1bf5-4b4b-4830-8a5b-f979b09f677d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 04ffb34b92aa43c521a9a454a8068e74cf4fd615
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88390282"
---
# <a name="collection-permissions-master-data-services"></a>Permissões de coleção (Serviços de Dados Mestre)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  As permissões de coleção aplicam-se a todas as membros coleções de uma entidade. Você não pode dar permissão a uma coleção específica; as permissões se aplicam a todas as coleções.  
  
> [!NOTE]  
>  Essas permissões se aplicam apenas à área funcional **Explorer** da interface do usuário.  
  
|Permissão|Descrição|  
|----------------|-----------------|  
|**Ler**|O usuário pode ler membros da coleção e os atributos de membro.|  
|**Criar**|O usuário pode criar membros da coleção e atribuir valores de atributo.|  
|**Atualização**|O usuário pode atualizar membros da coleção, atributos e relacionamentos|  
|**Delete (excluir)**|O usuário pode excluir os membros da coleção.|  
|**Deny**|Negar todo acesso aos membros da coleção.|  
  
 As permissões Ler, Criar, Atualizar e Excluir podem ser combinadas. Ao atribuir Criar, Atualizar e Excluir, a permissão de leitura é atribuída automaticamente.  
  
## <a name="see-also"></a>Consulte Também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Coleções &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)  
  
  
