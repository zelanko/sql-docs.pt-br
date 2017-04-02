---
title: "Especificar a ordem de processamento dos artigos de mesclagem | Microsoft Docs"
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
  - "artigos [replicação do SQL Server], ordem de processamento"
  - "replicação de mesclagem [replicação do SQL Server], artigo sobre ordem de processamento"
ms.assetid: d151e2c5-cf50-4cb3-a829-8f32455dbd66
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Especificar a ordem de processamento dos artigos de mesclagem
  Começando com [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], é possível substituir a ordem padrão de processamento para publicações de mesclagem do artigo. Isso é útil, por exemplo, se você definir a integridade referencial por meio de gatilhos e esses gatilhos precisarem ser acionados em uma determinada ordem.  
  
 **Para especificar a ordem de processamento dos artigos**  
  
-   Programação Transact-SQL de replicação: [especificar o processamento de ordem de mesclar artigos de tabela & #40. Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/publish/specify the processing order of merge table articles.md)  
  
## Como a ordem de processamento é determinada  
 Durante a sincronização da mesclagem, os artigos são, por padrão, processados na ordem exigida pelas dependências entre objetos, incluindo as limitações de integridade referencial declarativa (DRI) definidas nas tabelas de base. O processamento envolve a enumeração das alterações em uma tabela e depois a aplicação dessas alterações. Se não houver DRI presente, mas existirem filtros de junção ou registros lógicos entre artigos de tabela, os artigos serão processados na ordem exigida pelos filtros e registros lógicos. Artigos não relacionado a nenhum outro artigo por meio de DRI, filtros de junção, registros lógicos ou outras dependências serão processadas segundo o apelido do artigo no [sysmergearticles & #40. O Transact-SQL e 41;](../../../relational-databases/system-tables/sysmergearticles-transact-sql.md) tabela do sistema.  
  
 Considere uma publicação que inclui as tabelas **SalesOrderHeader** e **SalesOrderDetail** com uma coluna de chave primária **SalesOrderID** no **SalesOrderHeader** coluna de chave de tabela e um estrangeira correspondente **SalesOrderID** no **SalesOrderDetail** tabela. Durante a sincronização, a replicação de mesclagem impede violações de chave estrangeira ao inserir as novas linhas no **SalesOrderHeader** antes de inserir linhas associadas em **SalesOrderDetail**. Da mesma forma, as linhas são excluídas de **SalesOrderDetail** antes que a linha associada é excluída do **SalesOrderHeader**.  
  
 Porém, em alguns aplicativos a integridade referencial é imposta por meio de gatilhos de banco de dados, ou no nível do aplicativo, e não por meio de DRI. Considerando a publicação descrita acima, em vez de DRI, a **SalesOrderDetail** tabela poderia ter um gatilho insert que garante que a linha associada no **SalesOrderHeader** tabela existe antes de permitir uma inserção. **SalesOrderHeader** pode ter um gatilho de exclusão que garante que não há nenhuma linha associada em **SalesOrderDetail** antes de permitir uma exclusão. A replicação de mesclagem não leva em conta os gatilhos ao determinar a ordem de processamento de artigos porque não pode determinar qual será o resultado do gatilho até que ele tenha sido acionado. Do mesmo modo, a replicação não pode levar em conta as restrições definidas no nível do aplicativo.  
  
 Quando a integridade referencial é mantida por meio de gatilhos ou no nível do aplicativo, você deve especificar a ordem em que os artigos devem ser processados. O exemplo com gatilhos, você deve especificar que o **SalesOrderHeader** tabela deve ser processada antes **SalesOrderDetail**, pois a ordenação de artigos se baseia na ordem de inserção. A replicação de mesclagem inverterá a ordem automaticamente para as exclusões. A replicação de mesclagem não apresentará falha sem a ordenação de artigos, porque o Merge Agent continua a processar os artigos se houver uma violação de restrição; depois do processamento de todos os outros artigos, ele tenta novamente as operações que apresentaram falha. Especificar a ordem de artigos simplesmente evita as novas tentativas e o processamento adicional associado a elas. Se você especificar uma ordem incorreta (por exemplo, uma que faça com que os registros detalhados sejam processados antes dos registros do cabeçalho), a replicação de mesclagem irá tentar o processamento repetidamente, até obter êxito.  
  
## Consulte também  
 [Opções de artigo para replicação de mesclagem](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Agrupar alterações a linhas relacionadas com registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)   
 [Filtros de junção](../../../relational-databases/replication/merge/join-filters.md)  
  
  