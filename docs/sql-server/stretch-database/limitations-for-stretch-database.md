---
title: "Limitações do Stretch Database | Microsoft Docs"
ms.custom: 
ms.date: 06/14/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, limitations
- Stretch Database, blocking issues
- limitations (Stretch Database)
- blocking issues (Stretch Database)
ms.assetid: 2b1fbec1-7859-44fc-8417-724fc57a59c0
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d7cfb1568420f841cd8a2bba9349f19ad3dc01dc
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="limitations-for-stretch-database"></a>Limitações para o Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Aprenda sobre as limitações para tabelas habilitadas para Stretch e sobre as limitações que atualmente impedem que você habilite o Stretch para uma tabela.  
  
##  <a name="Caveats"></a> Limitações para tabelas habilitadas para o Stretch  
  
As tabelas habilitadas para o Stretch têm as seguintes limitações.  
  
### <a name="constraints"></a>Restrições  
-   Exclusividade não é imposta para restrições UNIQUE e restrições PRIMARY KEY em uma tabela do Azure que contém os dados migrados.  
  
### <a name="dml-operations"></a>Operações DML  
-   Você não pode executar o UPDATE ou DELETE de linhas que foram migradas ou linhas que são qualificadas para migração em uma tabela habilitada para Stretch ou em uma exibição que inclui tabelas habilitadas para Stretch.  
  
-   Você não pode executar o INSERT de linhas em uma tabela habilitada para o Stretch em um servidor vinculado.  
  
### <a name="indexes"></a>Índices  
-   Não é possível criar um índice para uma exibição que inclui tabelas habilitadas para o Stretch.  
  
-   Filtros em índices [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não são propagados para a tabela remota.  
  
##  <a name="Limitations"></a> Limitações que atualmente impedem que você habilite o Stretch para uma tabela  
   
 Os itens a seguir atualmente impedem que você habilite o Stretch para uma tabela.  
  
 ### <a name="table-properties"></a>Propriedades da tabela  
-   Tabelas que têm mais de 1.023 colunas ou mais de 998 índices  
  
-   FileTables ou tabelas que contêm dados FILESTREAM  
  
-   Tabelas que são replicadas ou que estão ativamente utilizando o Controle de Alterações ou a Captura de Dados de Alteração  
  
-   Tabelas com otimização de memória  
  
### <a name="data-types"></a>Tipos de dados  
-   text, ntext e image  
  
-   timestamp  
  
-   sql_variant  
  
-   XML  
  
-   Tipos de dados CLR, incluindo geometry, geography, hierarchyid e tipos CLR definidos pelo usuário  
  
 ### <a name="column-types"></a>Tipos de coluna  
 -   COLUMN_SET  
  
-   Colunas computadas  
  
### <a name="constraints"></a>Restrições  
-   Restrições padrão e restrições de verificação  
  
-   Restrições de chave estrangeira que referenciam a tabela. Em uma relação pai-filho (por exemplo, Order e Order_Detail), você pode habilitar o Stretch para a tabela filho (Order_Detail), mas não para a tabela pai (Order).  
  
### <a name="indexes"></a>Índices  
-   Índices de texto completo  
  
-   índices XML  
  
-   Índices espaciais  
  
-   Exibições indexadas que fazem referência à tabela  
  
## <a name="see-also"></a>Consulte também  
 [Identificar bancos de dados e tabelas para o Stretch Database executando o supervisor do Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [Habilitar o Stretch Database para um banco de dados](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Habilitar o Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
