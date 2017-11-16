---
title: "Especificar um local de pasta de instantâneo alternativa (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 9293f0eb-5531-47ec-b6e2-0392823ce5cc
caps.latest.revision: "42"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 78ea481b543fe74e8efb6231c75cd68822b5ee25
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="specify-an-alternate-snapshot-folder-location-sql-server-management-studio"></a>Especificar um local de pasta de instantâneo alternativa (SQL Server Management Studio)
  Especificar um local de instantâneo alternativo na página **Instantâneo** da caixa de diálogo **Propriedades de publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-specify-an-alternate-snapshot-location"></a>Para especificar um local de instantâneo alternativo  
  
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**:  
  
    1.  Selecione **Colocar os arquivos nesta pasta**, depois clique em **Procurar** para ir para o diretório ou para entrar no caminho de diretório em que os arquivos de instantâneo devem estar armazenados.  
  
        > [!NOTE]  
        >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se as assinaturas pull forem usadas, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\computername\snapshot. Para obter mais informações, consulte [Proteger a pasta de instantâneos](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
    2.  Desmarque **Colocar os arquivos na pasta padrão** , exceto se for necessário que os arquivos de instantâneo sejam gravados em ambos os locais.  
  
     Para compactar arquivos de instantâneo, selecione **Compactar arquivos de instantâneo neste local**. A compactação é usada normalmente para conexões de largura da banda baixa e locais de instantâneo alternativos em mídia removível, como um CD-ROM.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Locais da pasta de instantâneos alternativos](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de Replicação&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Especificar o local do instantâneo padrão &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Inicializar uma assinatura com um instantâneo](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
