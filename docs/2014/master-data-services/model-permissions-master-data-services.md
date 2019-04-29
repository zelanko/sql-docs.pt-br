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
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a1d5b43b83102f822b64fdd5e4ebdc416f1de593
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62923466"
---
# <a name="model-permissions-master-data-services"></a>Permissões de modelo (Master Data Services)
  As permissões de modelo se aplicam a todas as entidades, hierarquias derivadas, hierarquias explícitas e coleções existentes dentro do modelo. As permissões atribuídas ao modelo podem ser substituídas para qualquer objeto individual.  
  
> [!NOTE]  
>  Se um usuário for administrador de modelo, o modelo será exibido em todas as áreas funcionais da interface do usuário. Caso contrário, o modelo será exibido apenas na área funcional **Gerenciador** . Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
|Permissão|Descrição|  
|----------------|-----------------|  
|**Somente leitura**|Na **Explorer**, o modelo é exibido, mas o usuário não é possível adicionar ou remover membros e não é possível atualizar valores de atributos, associações de hierarquia ou associações de coleção.|  
|**Update (atualizar)**|Na **Explorer**, o modelo é exibido e o usuário pode adicionar e remover membros, pode atualizar valores de atributos, associações de hierarquia e associações de coleção.|  
|**Deny**|O modelo não é exibido.|  
  
 Quando você atribui permissão a um modelo, o usuário obtém acesso a todas as versões do modelo. Não é possível atribuir permissão a uma versão individual.  
  
## <a name="see-also"></a>Consulte também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Permissões de entidade &#40;Master Data Services&#41;](../../2014/master-data-services/entity-permissions-master-data-services.md)   
 [Permissões de coleção &#40;Master Data Services&#41;](../../2014/master-data-services/collection-permissions-master-data-services.md)  
  
  
