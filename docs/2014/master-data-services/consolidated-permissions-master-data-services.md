---
title: Consolidados permissões (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], consolidated member attribute permissions
- consolidated members [Master Data Services], attribute permissions
- permissions [Master Data Services], consolidated members
- members [Master Data Services], consolidated member permissions
ms.assetid: 084055a3-5fd3-43f3-b620-ac6afab42a3d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 66224262c88176fe0d0ddd1f4291b12213aed928
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054105"
---
# <a name="consolidated-permissions-master-data-services"></a>Permissões consolidadas (Serviços de Dados Mestre)
  Permissões consolidadas se aplicam aos valores de atributos para todos os membros consolidados de uma entidade.  
  
 As permissões consolidadas se aplicam apenas a entidades habilitadas para hierarquias explícitas e coleções.  
  
 **Observações:**  
  
-   As permissões de folha aplicam-se apenas à área funcional **Gerenciador** da interface do usuário.  
  
-   As permissões atribuídas aos atributos **Name** e **Code** não são impostas.  
  
|Permissão|Descrição|  
|----------------|-----------------|  
|**Somente leitura**|Os membros consolidados são exibidos, mas o usuário não pode adicionar, remover ou alterá-los.|  
|**Update (atualizar)**|Os membros consolidados são exibidos e o usuário pode adicionar, remover ou alterá-los.|  
|**Deny**|Os membros consolidados da entidade não são exibidos.|  
  
## <a name="attribute-permissions"></a>Permissões de atributo  
 As permissões de atributo se aplicam aos valores de atributo da entidade específica. Os usuários com permissões somente de atributo não podem adicionar ou remover membros.  
  
|Permissão|Descrição|  
|----------------|-----------------|  
|**Somente leitura**|O atributo é exibido, mas o usuário não pode alterar valores de atributo.|  
|**Update (atualizar)**|O atributo é exibido e o usuário pode alterar valores de atributo.|  
|**Deny**|O atributo não é exibido.<br /><br /> Observação: Você não pode negar acesso explicitamente para atributos Name e Code.|  
  
## <a name="see-also"></a>Consulte também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](assign-model-object-permissions-master-data-services.md)   
 [Permissões de folha &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Membros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
