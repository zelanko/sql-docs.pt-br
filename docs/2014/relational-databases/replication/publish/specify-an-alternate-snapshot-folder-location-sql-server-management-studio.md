---
title: Especificar um local de pasta de instantâneo alternativa (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 9293f0eb-5531-47ec-b6e2-0392823ce5cc
caps.latest.revision: 40
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ef44144a53ce16622bc834627aa800a42a65438b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007005"
---
# <a name="specify-an-alternate-snapshot-folder-location-sql-server-management-studio"></a>Especificar um local de pasta de instantâneo alternativa (SQL Server Management Studio)
  Especificar um local de instantâneo alternativo na página **Instantâneo** da caixa de diálogo **Propriedades de publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
### <a name="to-specify-an-alternate-snapshot-location"></a>Para especificar um local de instantâneo alternativo  
  
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**:  
  
    1.  Selecione **Colocar os arquivos nesta pasta**, depois clique em **Procurar** para ir para o diretório ou para entrar no caminho de diretório em que os arquivos de instantâneo devem estar armazenados.  
  
        > [!NOTE]  
        >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se as assinaturas pull forem usadas, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\computername\snapshot. Para obter mais informações, consulte [Proteger a pasta de instantâneos](../security/secure-the-snapshot-folder.md).  
  
    2.  Desmarque **Colocar os arquivos na pasta padrão** , exceto se for necessário que os arquivos de instantâneo sejam gravados em ambos os locais.  
  
     Para compactar arquivos de instantâneo, selecione **Compactar arquivos de instantâneo neste local**. A compactação é usada normalmente para conexões de largura da banda baixa e locais de instantâneo alternativos em mídia removível, como um CD-ROM.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Locais da pasta de instantâneos alternativos](../alternate-snapshot-folder-locations.md)   
 [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de Replicação&#41;](configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Especificar o local do instantâneo padrão &#40;SQL Server Management Studio&#41;](../specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md)   
 [Inicializar uma assinatura com um instantâneo](../initialize-a-subscription-with-a-snapshot.md)  
  
  