---
title: Permissões de folha (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attribute groups [Master Data Services], permissions
- members [Master Data Services], leaf member permissions
- permissions [Master Data Services], leaf members
- leaf members [Master Data Services], attribute permissions
- attributes [Master Data Services], leaf member attribute permissions
ms.assetid: bde16e8c-bcd4-4041-8130-55c5450e5f72
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f53b15609a806c2814cce4e2767db8158aefcf5
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="leaf-permissions-master-data-services"></a>Permissões de folha (Serviços de Dados Mestre)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Permissões de folha se aplicam aos valores de atributos para todos os membros folha de uma entidade.  
  
 Para entidades sem hierarquias explícitas habilitadas, atribuir permissão a **Folha** é o mesmo que atribuir permissão à entidade.  
  
 **Observações:**  
  
-   As permissões de folha aplicam-se apenas à área funcional **Gerenciador** da interface do usuário.  
  
-   As permissões atribuídas aos atributos **Name** e **Code** não são impostas.  
  
|Permissão|Description|  
|----------------|-----------------|  
|**Leitura**|O usuário pode ler membros folha e atributos.|  
|**Criar**|O usuário pode criar membros folha e atribuir valores de atributo durante a criação.|  
|**Update (atualizar)**|O usuário pode atualizar membros folha e atributos.|  
|**Delete (excluir)**|O usuário pode excluir membros folha.|  
|**Deny**|Nega todo o acesso aos membros folha.|  
  
 As permissões Ler, Criar, Atualizar e Excluir podem ser combinadas. Ao atribuir Criar, Atualizar e Excluir, a permissão de leitura é atribuída automaticamente.  
  
## <a name="attribute-permissions"></a>Permissões de atributo  
 As permissões de atributo se aplicam aos valores de atributo da entidade específica. Os usuários apenas com permissões de atributo não podem adicionar ou remover membros.  
  
|Permissão|Description|  
|----------------|-----------------|  
|**Leitura**|O usuário pode ler atributos.|  
|**Criar**|O usuário pode atribuir valores ao criar membros.|  
|**Update (atualizar)**|O usuário pode atualizar atributos.|  
|**Delete (excluir)**|Nenhum efeito.|  
|**Deny**|O atributo não é exibido.<br /><br /> Observação: você não pode negar acesso explicitamente para os atributos Name e Code.|  
  
### <a name="example"></a>Exemplo  
 Para a entidade Product, atribua a permissão **Atualizar** ao atributo Subcategory. Negue permissão a todos os demais atributos.  
  
|Nome|Código|Subcategory (atualizar)|  
|----------|----------|----------------------------|  
|Mountain-100|BK-M101|\{5\} Mountain Bikes|  
|Mountain-100|BK-M201|\{5\} Mountain Bikes|  
  
 No **Gerenciador**, você pode atualizar qualquer valor de atributo na coluna Subcategory. Se você não tiver permissão a um atributo, ele não será exibido.  
  
> [!NOTE]  
>  Nesse exemplo, Subcategory é um atributo baseado em domínio, baseado na entidade SubcategoryList. Você pode selecionar uma subcategoria diferente para Mountain-100, mas não pode adicionar nem excluir os membros da entidade SubcategoryList.  
  
## <a name="see-also"></a>Consulte Também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
    
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Membros &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
