---
title: Adicionar e remover artigos de uma publicação | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- dropping articles
- adding articles
- articles [SQL Server replication], adding
ms.assetid: d5a3e536-62d2-4473-a178-877ba52f7d7f
caps.latest.revision: 35
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d55157c66830d5a34517856381e39e2cccbef255
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="add-articles-to-and-drop-articles-from-a-publication"></a>Adicionar e remover artigos de uma publicação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Inicialmente, adicione os artigos a uma publicação ao criá-la no Assistente para Nova Publicação. Para obter mais informações sobre como usar esse assistente, consulte [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md).  
  
 Após a criação da publicação, adicione e exclua artigos na página **Artigos** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md). Para obter informações sobre as considerações para adicionar e remover artigos, consulte [Adicionar e remover artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### <a name="to-add-an-article-after-a-publication-is-created"></a>Para adicionar um artigo após a criação de uma publicação  
  
1.  Na página **Artigos** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**, desmarque a caixa de seleção **Mostrar somente os objetos marcados na lista**. Isso permitirá ver os objetos não publicados, no banco de dados de publicação.  
  
2.  Marque a caixa de seleção próxima a cada artigo que você quer adicionar.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-an-article"></a>Para excluir um artigo  
  
1.  Na página **Artigos** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**, desmarque a caixa de seleção ao lado de cada artigo que deseja excluir.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Definir um Artigo](../../../relational-databases/replication/publish/define-an-article.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
