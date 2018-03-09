---
title: "Introdução a Tabelas Temporais com Controle da Versão do Sistema | Microsoft Docs"
ms.custom: 
ms.date: 03/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d431f216-82cf-4d97-825e-bb35d3d53a45
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 456602d6543527b1826dc21f93859f75629fd1a1
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="getting-started-with-system-versioned-temporal-tables"></a>Introdução a Tabelas Temporais com Controle da Versão do Sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Dependendo do cenário, você pode criar novas tabelas temporais com controle da versão do sistema ou modificar as existentes adicionando atributos temporais ao esquema de tabela existente.   
Quando os dados na tabela temporal forem modificados, o sistema criará o histórico de versão de forma transparente para os aplicativos e os usuários finais. Como resultado, trabalhar com tabelas temporais com controle da versão do sistema não exigirá qualquer alteração na forma como a tabela é modificada ou como o último estado (real) dos dados é consultado.   
Além do DML e das consultas regulares, a tabela temporal também oferece maneiras fáceis e convenientes de obter informações do histórico de dados por meio da sintaxe estendida do Transact-SQL.   
Todas as tabelas com controle da versão do sistema têm uma tabela de histórico atribuída, mas isso é completamente transparente para os usuários, a menos que eles queiram otimizar o desempenho de carga de trabalho ou o volume de armazenamento criando índices adicionais ou escolhendo opções diferentes de armazenamento.    
O seguinte diagrama ilustra um fluxo de trabalho típico com tabelas temporais com controle de versão do sistema:   
![Introdução ao Temporal](../../relational-databases/tables/media/getting-started-with-temporal.png "Introdução ao Temporal")  
  
 Este tópico foi dividido em cinco subtópicos:  
  
-   [Como criar uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)  
  
-   [Modificando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)  
  
-   [Consultando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)  
  
-   [Alterando o esquema de uma tabela temporal com versão do sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)  
  
-   [Parando o controle de versão do sistema de uma tabela temporal com versão do sistema](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
## <a name="did-this-article-help-you-were-listening"></a>Este artigo foi útil para você? Estamos atentos  
 Quais são as informações que você está procurando? Você as localizou? Estamos atentos aos seus comentários para aprimorar o conteúdo. Envie seus comentários para [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Getting%20Started%20with%20System-Versioned%20Temporal%20Tables%20page)  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Particionamento de Tabelas Temporais](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Considerações e limitações da tabela temporal](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Segurança da tabela temporal](../../relational-databases/tables/temporal-table-security.md)   
 [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
