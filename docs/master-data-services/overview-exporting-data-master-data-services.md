---
title: "Visão geral: Exportando dados (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exporting data [Master Data Services]
- subscription views [Master Data Services]
- subscription views [Master Data Services], about subscription views
ms.assetid: 8b74409a-ea70-45f8-84c7-da6905e4901a
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1d2a7c7eccfffebd6e3d4000b302c1f9241ddc9d
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2018
---
# <a name="overview-exporting-data-master-data-services"></a>Visão geral: exportando dados [Master Data Services]
  Este artigo apresenta os tipos de formatos de exibição de assinatura e como determinar quando as exibições precisam ser editadas devido a alterações em objetos de modelo.  
  
 Você cria uma exibição de assinatura para exportar dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para um sistema de assinatura, como [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Você usa o sistema de assinatura para exibir os dados no banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  Para obter informações sobre como criar a exibição de assinatura, consulte [Criar uma exibição de assinatura para exportar dados &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)  
  
 Para obter mais informações sobre exibições, consulte [exibições](../relational-databases/views/views.md).  
  
## <a name="subscription-view-formats"></a>Formatos de exibição da assinatura  
 Ao criar uma exibição do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], você faz escolhas em um conjunto de formatos de exibição padrão fornecido pelo [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Esses formatos podem ser usados para criar exibições que mostram:  
  
-   Todos os membros da folha e seus atributos.  
  
-   Todos os membros da folha consolidados e seus atributos.  
  
-   Todas as coleções e seus atributos.  
  
-   Os membros explicitamente adicionados a uma coleção.  
  
-   Os membros de uma hierarquia derivada, em formato pai-filho ou de nível.  
  
-   Os membros de todas as hierarquias explícitas de uma entidade, em formato pai-filho ou de nível.  
  
## <a name="subscription-views-can-become-out-of-date"></a>Exibições de assinatura podem se tornar desatualizadas  
 Depois de criar uma exibição de assinatura para uma entidade ou hierarquia, as alterações nos objetos modelo associados não são refletidas automaticamente na exibição. Talvez seja necessário gerar novamente uma exibição de assinatura no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para refletir as alterações nos objetos modelo. A coluna **Alterado** na página **Exportação** é atualizada para **True** quando objetos do modelo forem alterados. **True** indica que você deve editar e salvar a exibição de assinatura, o que gera novamente a exibição.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar uma exibição de assinatura de seus dados mestre.|[Criar uma exibição de assinatura para exportar dados &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|Excluir uma exibição de assinatura existente.|[Excluir uma exibição de assinatura &#40;Master Data Services&#41;](../master-data-services/delete-a-subscription-view-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Formatos de exibição de assinatura &#40;Master Data Services&#41;](../master-data-services/subscription-view-formats-master-data-services.md)  
  
-   [exibições](../relational-databases/views/views.md)  
  
  
