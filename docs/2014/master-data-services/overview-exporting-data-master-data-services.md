---
title: Exportando dados (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data [Master Data Services]
- subscription views [Master Data Services]
- subscription views [Master Data Services], about subscription views
ms.assetid: 8b74409a-ea70-45f8-84c7-da6905e4901a
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3e7a228062035772b9c394a246de0452f36239b1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158636"
---
# <a name="exporting-data-master-data-services"></a>Exportando dados (Master Data Services)
  Você pode exportar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] dados para sistemas de assinatura com a criação de exibições de assinaturas. Qualquer sistema assinante pode exibir os dados publicados no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para obter mais informações sobre exibições, consulte [exibições](../relational-databases/views/views.md).  
  
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
|Criar uma exibição de assinatura de seus dados mestre.|[Criar uma exibição de assinatura &#40;Master Data Services&#41;](create-a-subscription-view-to-export-data-master-data-services.md)|  
|Excluir uma exibição de assinatura existente.|[Excluir uma exibição de assinatura &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-subscription-view-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Formatos de exibição de assinatura &#40;Master Data Services&#41;](../../2014/master-data-services/subscription-view-formats-master-data-services.md)  
  
-   [exibições](../relational-databases/views/views.md)  
  
  
