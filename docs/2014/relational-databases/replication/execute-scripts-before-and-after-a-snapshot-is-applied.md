---
title: Executar Scripts antes e depois que um instantâneo é aplicado (SQL Server Management Studio) | Microsoft Docs
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
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
caps.latest.revision: 37
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1e22987419706c6449ca7dd501d1ee26f43aa14a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020676"
---
# <a name="execute-scripts-before-and-after-a-snapshot-is-applied-sql-server-management-studio"></a>Executar scripts antes e depois de um instantâneo ser aplicado (SQL Server Management Studio)
  Especifique um script opcional para ser executado antes ou depois da aplicação do instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
> [!NOTE]  
>  Essas opções não estarão disponíveis se a opção **Formato do instantâneo** estiver definida como **Caractere**.  
  
### <a name="to-execute-a-script-before-or-after-a-snapshot-is-applied"></a>Para executar um script antes ou depois de um instantâneo ser aplicado  
  
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**:  
  
    -   Para especificar um script a ser executado antes de o instantâneo ser aplicado, clique em **Procurar** para navegar até o script ou insira um caminho para o script na caixa de texto **Antes de aplicar o instantâneo, executar este script** .  
  
        > [!NOTE]  
        >  O Agente de Distribuição ou Agente de Mesclagem devem ter permissões de leitura para o diretório especificado. Se forem usadas assinaturas pull, você deverá especificar um diretório compartilhado como um caminho UNC, como \\\computername\scripts\myscript.sql.  
  
    -   Para especificar um script a ser executado depois de o instantâneo ser aplicado, clique em **Procurar** para navegar até o script ou insira um caminho UNC para o script na caixa de texto **Após aplicar o instantâneo, executar este script** .  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de Replicação&#41;](publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Alterar propriedades da publicação e do artigo](publish/change-publication-and-article-properties.md)   
 [Executar scripts antes e depois da aplicação do instantâneo](execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md)  
  
  