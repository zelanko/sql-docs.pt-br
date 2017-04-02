---
title: "Introdu&#231;&#227;o a Tabelas Temporais com Controle da Vers&#227;o do Sistema | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/28/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: d431f216-82cf-4d97-825e-bb35d3d53a45
caps.latest.revision: 12
author: "CarlRabeler"
ms.author: "carlrab"
manager: "jhubbard"
caps.handback.revision: 12
---
# Introdu&#231;&#227;o a Tabelas Temporais com Controle da Vers&#227;o do Sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Dependendo do cenário, você pode criar novas tabelas temporais com controle da versão do sistema ou modificar as existentes adicionando atributos temporais ao esquema de tabela existente.   
Quando os dados na tabela temporal forem modificados, o sistema criará o histórico de versão de forma transparente para os aplicativos e os usuários finais. Como resultado, trabalhar com tabelas temporais com controle da versão do sistema não exigirá qualquer alteração na forma como a tabela é modificada ou como o último estado (real) dos dados é consultado.   
Além do DML e das consultas regulares, a tabela temporal também oferece maneiras fáceis e convenientes de obter informações do histórico de dados por meio da sintaxe estendida do Transact-SQL.   
Todas as tabelas com controle da versão do sistema têm uma tabela de histórico atribuída, mas isso é completamente transparente para os usuários, a menos que eles queiram otimizar o desempenho de carga de trabalho ou o volume de armazenamento criando índices adicionais ou escolhendo opções diferentes de armazenamento.    
O seguinte diagrama ilustra um fluxo de trabalho típico com tabelas temporais com controle de versão do sistema:   
![Getting Started with Temporal](../../relational-databases/tables/media/getting-started-with-temporal.png "Getting Started with Temporal")  
  
 Este tópico foi dividido em cinco subtópicos:  
  
-   [Como criar uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)  
  
-   [Modificando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)  
  
-   [Consultando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)  
  
-   [Alterando o esquema de uma tabela temporal com versão do sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)  
  
-   [Parando o controle de versão do sistema de uma tabela temporal com versão do sistema](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
## Este artigo foi útil para você? Estamos atentos  
 Quais são as informações que você está procurando? Você as localizou? Estamos atentos aos seus comentários para aprimorar o conteúdo. Envie seus comentários para [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Getting%20Started%20with%20System-Versioned%20Temporal%20Tables%20page)  
  
## Consulte também  
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Particionamento de Tabelas Temporais](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Considerações e limitações da tabela temporal](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Segurança da tabela temporal](../../relational-databases/tables/temporal-table-security.md)   
 [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  