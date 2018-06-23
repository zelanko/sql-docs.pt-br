---
title: Consolidados permissões (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes [Master Data Services], consolidated member attribute permissions
- consolidated members [Master Data Services], attribute permissions
- permissions [Master Data Services], consolidated members
- members [Master Data Services], consolidated member permissions
ms.assetid: 084055a3-5fd3-43f3-b620-ac6afab42a3d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a0436df9a9aa4f21d9a581172e2874ca2dad6aa6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115686"
---
# <a name="consolidated-permissions-master-data-services"></a>Permissões consolidadas (Serviços de Dados Mestre)
  Permissões consolidadas se aplicam aos valores de atributos para todos os membros consolidados de uma entidade.  
  
 As permissões consolidadas se aplicam apenas a entidades habilitadas para hierarquias explícitas e coleções.  
  
 **Observações:**  
  
-   As permissões de folha aplicam-se apenas à área funcional **Gerenciador** da interface do usuário.  
  
-   As permissões atribuídas aos atributos **Name** e **Code** não são impostas.  
  
|Permissão|Description|  
|----------------|-----------------|  
|**Somente leitura**|Os membros consolidados são exibidos, mas o usuário não pode adicionar, remover ou alterá-los.|  
|**Update (atualizar)**|Os membros consolidados são exibidos e o usuário pode adicionar, remover ou alterá-los.|  
|**Deny**|Os membros consolidados da entidade não são exibidos.|  
  
## <a name="attribute-permissions"></a>Permissões de atributo  
 As permissões de atributo se aplicam aos valores de atributo da entidade específica. Os usuários com permissões somente de atributo não podem adicionar ou remover membros.  
  
|Permissão|Description|  
|----------------|-----------------|  
|**Somente leitura**|O atributo é exibido, mas o usuário não pode alterar valores de atributo.|  
|**Update (atualizar)**|O atributo é exibido e o usuário pode alterar valores de atributo.|  
|**Deny**|O atributo não é exibido.<br /><br /> Observação: você não pode negar acesso explicitamente para os atributos Name e Code.|  
  
## <a name="see-also"></a>Consulte também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](assign-model-object-permissions-master-data-services.md)   
 [Permissões de folha &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [Permissões de objeto modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Membros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
  