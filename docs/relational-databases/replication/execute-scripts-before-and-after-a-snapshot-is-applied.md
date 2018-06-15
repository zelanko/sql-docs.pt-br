---
title: Executar scripts antes e depois da aplicação do instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3d69aaefe439feea910c62b1aff36ebe38e402a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32956181"
---
# <a name="execute-scripts-before-and-after-a-snapshot-is-applied"></a>Executar scripts antes e depois da aplicação do instantâneo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Especifique um script opcional para ser executado antes ou depois da aplicação do instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
> [!NOTE]  
>  Essas opções não estarão disponíveis se a opção **Formato do instantâneo** estiver definida como **Caractere**.  
  
### <a name="to-execute-a-script-before-or-after-a-snapshot-is-applied"></a>Para executar um script antes ou depois de um instantâneo ser aplicado  
  
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**:  
  
    -   Para especificar um script a ser executado antes de o instantâneo ser aplicado, clique em **Procurar** para navegar até o script ou insira um caminho para o script na caixa de texto **Antes de aplicar o instantâneo, executar este script** .  
  
        > [!NOTE]  
        >  O Agente de Distribuição ou Agente de Mesclagem devem ter permissões de leitura para o diretório especificado. Se forem usadas assinaturas pull, você deverá especificar um diretório compartilhado como um caminho UNC, como \\\computername\scripts\myscript.sql.  
  
    -   Para especificar um script a ser executado depois de o instantâneo ser aplicado, clique em **Procurar** para navegar até o script ou insira um caminho UNC para o script na caixa de texto **Após aplicar o instantâneo, executar este script** .  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de Replicação&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Executar scripts antes e depois da aplicação do instantâneo](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
