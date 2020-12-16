---
description: Introdução a Tabelas Temporais com Controle da Versão do Sistema
title: Introdução a Tabelas Temporais com Controle da Versão do Sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: d431f216-82cf-4d97-825e-bb35d3d53a45
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1d62bbb6d38da6b60179f723e4bb363dec6ad225
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440531"
---
# <a name="getting-started-with-system-versioned-temporal-tables"></a>Introdução a tabelas temporais com controle da versão do sistema


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


Dependendo do cenário, você pode criar novas tabelas temporais com controle da versão do sistema ou modificar as existentes adicionando atributos temporais ao esquema de tabela existente. Quando os dados na tabela temporal forem modificados, o sistema criará o histórico de versão de forma transparente para os aplicativos e os usuários finais. Como resultado, trabalhar com tabelas temporais com controle da versão do sistema não exigirá qualquer alteração na forma como a tabela é modificada ou como o último estado (real) dos dados é consultado.

Além do DML e das consultas regulares, a tabela temporal também oferece maneiras fáceis e convenientes de obter informações do histórico de dados por meio da sintaxe estendida do Transact-SQL. Todas as tabelas com controle da versão do sistema têm uma tabela de histórico atribuída, mas isso é completamente transparente para os usuários, a menos que eles queiram otimizar o desempenho de carga de trabalho ou o volume de armazenamento criando índices adicionais ou escolhendo opções diferentes de armazenamento.

O seguinte diagrama ilustra um fluxo de trabalho típico com tabelas temporais com controle de versão do sistema: ![Introdução ao Temporal](../../relational-databases/tables/media/getting-started-with-temporal.png "Introdução ao Temporal")

Este tópico foi dividido em cinco subtópicos:

- [Criando uma tabela temporal com controle de versão do sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [Modificando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [Consultando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [Alterando o esquema de uma tabela temporal com versão do sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
- [Interrompendo o controle de versão do sistema em uma tabela temporal com controle de versão do sistema](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)

## <a name="next-steps"></a>Próximas etapas

- [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)
- [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Particionamento com tabelas temporais](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [Considerações e limitações da tabela temporal](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [Segurança da tabela temporal](../../relational-databases/tables/temporal-table-security.md)
- [Gerenciar a retenção de dados históricos em tabelas temporais com controle de versão do sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
