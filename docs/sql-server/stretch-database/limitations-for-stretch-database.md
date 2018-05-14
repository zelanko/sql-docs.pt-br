---
title: Limitações do Stretch Database | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: stretch-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, limitations
- Stretch Database, blocking issues
- limitations (Stretch Database)
- blocking issues (Stretch Database)
ms.assetid: 2b1fbec1-7859-44fc-8417-724fc57a59c0
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3a6802b180c123f708c23ab657ce8064a0a3384b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="limitations-for-stretch-database"></a>Limitações para o Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


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
  
## <a name="see-also"></a>Consulte Também  
 [Identificar bancos de dados e tabelas para o Stretch Database executando o supervisor do Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Habilitar o Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
