---
title: "Otimizar o desempenho da replica&#231;&#227;o de mesclagem com o controle de exclus&#227;o condicional | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "controle de exclusão condicional [replicação do SQL Server]"
  - "replicação de mesclagem [replicação do SQL Server], controle de exclusão condicional"
  - "artigos [replicação do SQL Server], controle de exclusão condicional"
ms.assetid: 58f120a3-ea3a-4e97-93f0-0eb4e580ecf2
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Otimizar o desempenho da replica&#231;&#227;o de mesclagem com o controle de exclus&#227;o condicional
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Com a replicação de mesclagem você pode especificar que as exclusões para um ou mais artigos não devem ser controladas pelos gatilhos de replicação e pelas tabelas do sistema. Se especificar essa opção para um artigo, as exclusões não serão controladas nem replicadas do Publicador ou de qualquer Assinante. Essa opção está disponível para dar suporte a vários cenários de aplicativos e para oferecer uma otimização de desempenho para os casos nos quais a replicação de exclusões não é necessária ou desejada. O desempenho é melhorado de três maneiras: os metadados para exclusões não são armazenados, as exclusões não são enumeradas durante a sincronização e as exclusões não são replicadas para nem aplicadas ao Assinante.  
  
> [!NOTE]  
>  Para usar artigos de somente download, o nível de compatibilidade da publicação deve ser pelo menos 90RTM.  
  
 A opção pode ser especificada na criação de uma publicação ou pode ser alternada para ativada e desativada se um aplicativo necessitar que algumas exclusões sejam replicadas e outras não, como as exclusões de lotes. Os exemplos a seguir ilustram os modos nos quais essa opção poderá ser usada em um aplicativo:  
  
-   O aplicativo para uma força de vendas móvel tem normalmente tabelas como **SalesOrderHeader**, **SalesOrderDetail** e **Produto**. Os pedidos são inseridos no Assinante e replicados para o Publicador, que, muitas vezes, fornece dados a um sistema de efetivação de pedidos. Vários trabalhadores externos usam dispositivos portáteis que têm um armazenamento limitado: após o pedido ser recebido no Publicador, ele pode ser excluído do Assinante. A exclusão não é propagada ao Publicador, pois o pedido continua ativo no sistema.  
  
     Nesse cenário, as exclusões não serão controladas para as tabelas **SalesOrderHeader** e **SalesOrderDetail** . As exclusões serão controladas na tabela **Produto** , pois se um produto for excluído no Publicador, a exclusão deverá ser enviada ao Assinante para manter a lista de produtos atualizada.  
  
-   Um aplicativo armazena os dados históricos em uma tabela como a **TransactionHistory**, que é limpa periodicamente para remover registros antigos com mais de um ano. A tabela pode ser filtrada de modo que os Assinantes recebam dados sobre transações dentro do mês atual. Exclusões mensais de lotes no Publicador que remove dados mais antigos não são relevantes para os Assinantes, mas poderão ser controladas e enumeradas por padrão.  
  
     Nesse cenário, antes de o processamento do lote ocorrer, a atividade pode ser interrompida no sistema e o aplicativo irá desabilitar o controle das exclusões. Após a conclusão do processamento, o controle poderá ser habilitado novamente.  
  
> [!IMPORTANT]  
>  Se uma outra atividade continuar no Publicador, você deverá garantir que as exclusões que deveriam ser propagadas para o Assinante não ocorram enquanto o controle das exclusões estiver desabilitado.  
  
 **Para especificar que as exclusões não devem ser controladas**  
  
-   Replicação [!INCLUDE[tsql](../../../includes/tsql-md.md)] programação: [especificar que exclui deve não ser rastreadas para mesclar artigos e 40; Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/publish/specify that deletes should not be tracked for merge articles.md)  
  
## Consulte também  
 [Opções de artigo para replicação de mesclagem](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Otimizar o desempenho de replicação de mesclagem com artigos de somente download](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)  
  
  