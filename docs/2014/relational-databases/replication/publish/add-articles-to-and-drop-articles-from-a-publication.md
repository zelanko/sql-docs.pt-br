---
title: Adicionar e descartar artigos de uma publicação (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ea3c32da50b3ec5e2a2eb3d3bf58fad1e0323f10
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009329"
---
# <a name="add-articles-to-and-drop-articles-from-a-publication-sql-server-management-studio"></a>Adicionar e descartar artigos em uma publicação (SQL Server Management Studio)
  Inicialmente, adicione os artigos a uma publicação ao criá-la no Assistente para Nova Publicação. Para obter mais informações sobre como usar esse assistente, consulte [Criar uma publicação](create-a-publication.md).  
  
 Após a criação da publicação, adicione e exclua artigos na página **Artigos** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](view-and-modify-publication-properties.md). Para obter informações sobre as considerações para adicionar e remover artigos, consulte [Adicionar e remover artigos de publicações existentes](add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### <a name="to-add-an-article-after-a-publication-is-created"></a>Para adicionar um artigo após a criação de uma publicação  
  
1.  Na página **Artigos** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**, desmarque a caixa de seleção **Mostrar somente os objetos marcados na lista**. Isso permitirá ver os objetos não publicados, no banco de dados de publicação.  
  
2.  Marque a caixa de seleção próxima a cada artigo que você quer adicionar.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-an-article"></a>Para excluir um artigo  
  
1.  Na página **Artigos** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**, desmarque a caixa de seleção ao lado de cada artigo que deseja excluir.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Definir um Artigo](define-an-article.md)   
 [Publicar dados e objetos de banco de dados](publish-data-and-database-objects.md)  
  
  