---
title: Permissões de modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], permissions
- permissions [Master Data Services], models
ms.assetid: 210f440b-2cc1-4c49-94b1-3a97e2af7bc3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 733827ecace64ef86b54831f63fd8c2889203919
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65478961"
---
# <a name="model-permissions-master-data-services"></a>Permissões de modelo (Master Data Services)
  As permissões de modelo se aplicam a todas as entidades, hierarquias derivadas, hierarquias explícitas e coleções existentes dentro do modelo. As permissões atribuídas ao modelo podem ser substituídas para qualquer objeto individual.  
  
> [!NOTE]  
>  Se um usuário for administrador de modelo, o modelo será exibido em todas as áreas funcionais da interface do usuário. Caso contrário, o modelo será exibido apenas na área funcional **Gerenciador** . Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
|Permissão|DESCRIÇÃO|  
|----------------|-----------------|  
|**Somente leitura**|No **Explorer**, o modelo é exibido, mas o usuário não pode adicionar ou remover membros e não pode atualizar valores de atributo, associações de hierarquia ou associações de coleção.|  
|**Cumulativo**|No **Explorer**, o modelo é exibido e o usuário pode adicionar e remover membros, pode atualizar valores de atributo, associações de hierarquia e associações de coleção.|  
|**Deny**|O modelo não é exibido.|  
  
 Quando você atribui permissão a um modelo, o usuário obtém acesso a todas as versões do modelo. Não é possível atribuir permissão a uma versão individual.  
  
## <a name="see-also"></a>Consulte Também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Permissões de entidade &#40;Master Data Services&#41;](../../2014/master-data-services/entity-permissions-master-data-services.md)   
 [Permissões de coleção &#40;Master Data Services&#41;](../../2014/master-data-services/collection-permissions-master-data-services.md)  
  
  
