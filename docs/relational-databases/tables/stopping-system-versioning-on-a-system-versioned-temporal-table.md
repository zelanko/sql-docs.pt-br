---
title: Parando o controle de versão do sistema de uma tabela temporal com versão do sistema | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dddd707e-bfb1-44ff-937b-a84c5e5d1a94
caps.latest.revision: 10
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9e44f6d1b808b5ed1a02cad7d9c6b1c7e14eb7c6
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43063509"
---
# <a name="stopping-system-versioning-on-a-system-versioned-temporal-table"></a>Parando o controle de versão do sistema de uma tabela temporal com versão do sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  É aconselhável parar o controle de versão em sua tabela temporal temporariamente ou permanentemente.   
Você pode fazer isso definindo a cláusula **SYSTEM_VERSIONING** como **OFF**.  
  
## <a name="setting-systemversioning--off"></a>Falha ao definir SYSTEM_VERSIONING = OFF  
 Pare o controle de versão de sistema se quiser realizar operações de manutenção específicas na tabela temporal ou se não precisar mais de uma tabela com controle de versão. Como resultado dessa operação, você obterá duas tabelas independentes:  
  
-   Tabela atual com a definição do período  
  
-   Tabela de histórico como uma tabela normal  
  
### <a name="important-remarks"></a>Observações importantes  
  
-   Não acontece nenhuma perda de dados quando você define  **SYSTEM_VERSIONING = OFF** ou remove o período **SYSTEM_TIME** .  
  
-   Quando você define **SYSTEM_VERSIONING = OFF** e não remove o período **SYSTEM_TIME** , o sistema continuará a atualizar as colunas de período para cada operação de inserção e atualização. Exclusões na tabela atual serão permanentes.  
  
-   Remova o período **SYSTEM_TIME** para remover as colunas de período completamente.  
  
-   Quando você define **SYSTEM_VERSIONING = OFF**, todos os usuários com permissões suficientes poderão modificar o esquema e o conteúdo da tabela de histórico ou até mesmo excluir permanentemente a tabela de histórico.  
  
### <a name="permanently-remove-systemversioning"></a>Remover permanentemente o SYSTEM_VERSIONING  
 Este exemplo remove permanentemente o SYSTEM_VERSIONING e as colunas de período completamente. A remoção das colunas de período é opcional.  
  
```  
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);   
/*Optionally, DROP PERIOD if you want to revert temporal table to a non-temporal*/   
ALTER TABLE dbo.Department   
DROP PERIOD FOR SYSTEM_TIME;  
  
```  
  
### <a name="temporarily-remove-systemversioning"></a>Remover temporariamente o SYSTEM_VERSIONING  
 Esta é a lista de operações que requer que a versão do sistema seja definida como **OFF**:  
  
-   Removendo dados desnecessários do histórico (**DELETE** ou **TRUNCATE**)  
  
-   Removendo dados da tabela atual sem controle de versão (**DELETE**, **TRUNCATE**)  
  
-   Partição **SWITCH OUT** da tabela atual  
  
-   Partição **SWITCH IN** para a tabela de histórico  
  
 Este exemplo interrompe temporariamente o SYSTEM_VERSIONING para permitir que você execute operações de manutenção específicas. Se parar temporariamente o controle de versão como um pré-requisito para a manutenção da tabela, é altamente recomendável fazer isso dentro de uma transação para manter a consistência dos dados.  
  
```  
BEGIN TRAN   
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);   
TRUNCATE TABLE [History].[DepartmentHistory]   
WITH (PARTITIONS (1,2))   
ALTER TABLE dbo.Department SET    
(   
SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.DepartmentHistory)   
);   
COMMIT ;  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Introdução a Tabelas Temporais com Controle da Versão do Sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Como criar uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [Modificando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [Consultando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [Alterando o esquema de uma tabela temporal com versão do sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)  
  
  
