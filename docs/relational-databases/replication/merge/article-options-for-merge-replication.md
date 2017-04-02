---
title: "Op&#231;&#245;es de artigo para replica&#231;&#227;o de mesclagem | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicação de mesclagem [replicação do SQL Server], opções do artigo"
  - "artigos [replicação do SQL Server], opções de replicação de mesclagem"
ms.assetid: 670abd41-d204-4cd7-a371-7664e603a0ce
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Op&#231;&#245;es de artigo para replica&#231;&#227;o de mesclagem
  Há muitas opções para a mesclagem de artigos de tabela que lhe possibilitam personalizar o comportamento de replicação para as necessidades de seus aplicativos. Usando a replicação de mesclagem, você pode fazer o seguinte:  
  
-   Usar filtros de linha, filtros de junção e filtros de coluna. Filtrar artigos de tabela lhe permite criar partições de dados a serem publicados. Para obter mais informações, consulte [Filtrar dados publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
-   Especificar se as alterações feitas ao Assinante foram carregadas no Publicador. Para aplicativos nos quais alguns ou todos os dados deverão ser somente leitura no Assinante, artigos de somente download melhoram o desempenho. Para obter mais informações, consulte [otimizar o desempenho de replicação de mesclagem com artigos Download-Only](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
-   Especificar quais exclusões para um ou mais artigos não deveriam ser rastreados por gatilhos de replicação e tabelas do sistema. Esta opção pode ser útil em muitos cenários de aplicativo. Estes, incluem cenários que usam exclusões de lote que não precisem ser reproduzidos. Para obter mais informações, consulte [otimizar desempenho de replicação de mesclagem com o controle condicional de excluir](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md).  
  
-   Especificar a ordem de processamento dos artigos para garantir que os artigos sejam processados na ordem requerida pelo seu aplicativo. Para obter mais informações, consulte [especificar o processamento de ordem de mesclar artigos](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
-   Especificar que um conjunto de relatórios relacionados deva ser processado como uma unidade (por padrão, replicação de mesclagem processa alterações nas tabelas de linha a linha). Para obter mais informações, consulte [grupo alterações nas linhas relacionadas com registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
-   Usar detecção de conflito e resolução para casos em que os mesmos dados possam ser alterados em mais de um nó na topologia. Para obter mais informações, consulte [Detect and Resolve Merge Replication Conflicts](../../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md).  
  
-   Especificar opções de esquema se as restrições e os gatilhos são copiados para o Assinante. Para obter mais informações, consulte [especificar opções de esquema](../../../relational-databases/replication/publish/specify-schema-options.md).  
  
-   Use um manipulador de lógica de negócios para responder a muitas condições durante a sincronização. Que incluem alterações de dados, conflitos e erros. Para obter mais informações, consulte [executar lógica de negócios durante a sincronização direta](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
## Consulte também  
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  