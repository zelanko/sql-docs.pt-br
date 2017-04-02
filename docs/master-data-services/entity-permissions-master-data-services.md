---
title: "Permiss&#245;es de entidade (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "entidades [Master Data Services], permissões"
  - "permissões [Master Data Services], entidades"
ms.assetid: 22785062-4faf-46ee-bffa-01cbd6d5a5b3
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# Permiss&#245;es de entidade (Master Data Services)
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
  
## Consulte também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  