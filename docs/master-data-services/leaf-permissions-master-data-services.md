---
title: "Permiss&#245;es de folha (Servi&#231;os de Dados Mestre) | Microsoft Docs"
ms.custom: ""
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "grupos de atributos [Master Data Services], permissões"
  - "membros [Master Data Services]. permissões de membro folha"
  - "permissões [Master Data Services], membros folha"
  - "membros folha [Master Data Services]. permissões de atributo"
  - "atributos [Master Data Services]. permissões de membro folha"
ms.assetid: bde16e8c-bcd4-4041-8130-55c5450e5f72
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# Permiss&#245;es de folha (Servi&#231;os de Dados Mestre)
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
  
## Permissões de atributo  
 As permissões de atributo se aplicam aos valores de atributo da entidade específica. Os usuários apenas com permissões de atributo não podem adicionar ou remover membros.  
  
|Permissão|Description|  
|----------------|-----------------|  
|**Leitura**|O usuário pode ler atributos.|  
|**Criar**|O usuário pode atribuir valores ao criar membros.|  
|**Update (atualizar)**|O usuário pode atualizar atributos.|  
|**Delete (excluir)**|Nenhum efeito.|  
|**Deny**|O atributo não é exibido.<br /><br /> Observação: você não pode negar acesso explicitamente para os atributos Name e Code.|  
  
### Exemplo  
 Para a entidade Product, atribua a permissão **Atualizar** ao atributo Subcategory. Negue permissão a todos os demais atributos.  
  
|Name|Código|Subcategory (atualizar)|  
|----------|----------|----------------------------|  
|Mountain-100|BK-M101|\{5\} Mountain Bikes|  
|Mountain-100|BK-M201|\{5\} Mountain Bikes|  
  
 No **Gerenciador**, você pode atualizar qualquer valor de atributo na coluna Subcategory. Se você não tiver permissão a um atributo, ele não será exibido.  
  
> [!NOTE]  
>  Nesse exemplo, Subcategory é um atributo baseado em domínio, baseado na entidade SubcategoryList. Você pode selecionar uma subcategoria diferente para Mountain-100, mas não pode adicionar nem excluir os membros da entidade SubcategoryList.  
  
## Consulte também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permissões consolidadas &#40;Master Data Services&#41;](../Topic/Consolidated%20Permissions%20\(Master%20Data%20Services\).md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Membros &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  