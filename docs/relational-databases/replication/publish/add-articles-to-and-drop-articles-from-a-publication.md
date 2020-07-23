---
title: Adicionar e remover artigos de publicação (SSMS)
description: Descreve como adicionar artigos a uma publicação e remover artigos dela com o SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- dropping articles
- adding articles
- articles [SQL Server replication], adding
ms.assetid: d5a3e536-62d2-4473-a178-877ba52f7d7f
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 1a32aabcd7eb431498e54a828dcfdcf4e87480c1
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923679"
---
# <a name="add-articles-to-and-drop-articles-from-a-publication"></a>Adicionar e remover artigos de uma publicação
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Inicialmente, adicione os artigos a uma publicação ao criá-la no Assistente para Nova Publicação. Para obter mais informações sobre como usar esse assistente, consulte [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md).  
  
 Após a criação da publicação, adicione e exclua artigos na página **Artigos** da caixa de diálogo **Propriedades da Publicação – \<Publication>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md). Para obter informações sobre as considerações para adicionar e remover artigos, consulte [Adicionar e remover artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### <a name="to-add-an-article-after-a-publication-is-created"></a>Para adicionar um artigo após a criação de uma publicação  
  
1.  Na página **Artigos** da caixa de diálogo **Propriedades da Publicação – \<Publication>** , desmarque a caixa de seleção **Mostrar somente os objetos marcados na lista**. Isso permitirá ver os objetos não publicados, no banco de dados de publicação.  
  
2.  Marque a caixa de seleção próxima a cada artigo que você quer adicionar.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-an-article"></a>Para excluir um artigo  
  
1.  Na página **Artigos** da caixa de diálogo **Propriedades da Publicação – \<Publication>** , desmarque a caixa de seleção ao lado de cada artigo que deseja excluir.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
