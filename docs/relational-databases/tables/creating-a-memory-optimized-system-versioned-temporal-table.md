---
title: Criando uma tabela temporal com controle da versão do sistema com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 1c1fc682-bf5b-4096-a0ff-3235d71c205a
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e852dcc87d5660889f30ad6d528ca08d53059913
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554832"
---
# <a name="creating-a-memory-optimized-system-versioned-temporal-table"></a>Criação de uma tabela temporal com controle da versão do sistema com otimização de memória

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

Assim como acontece com a criação de uma tabela de histórico baseada em disco, é possível criar uma tabela temporal com otimização de memória de várias maneiras.

> [!NOTE]
> Para criar tabelas com otimização de memória, você deve primeiro criar [O grupo de arquivos com otimização de memória](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md).

A criação de uma tabela temporal com uma tabela de histórico padrão é uma opção conveniente quando você deseja controlar a nomenclatura e ainda depende do sistema para criar a tabela de histórico com a configuração padrão. No exemplo a seguir, uma nova tabela temporal com controle da versão do sistema e com otimização de memória é vinculada a uma nova tabela de histórico com base em disco.

```sql
CREATE SCHEMA History
GO
CREATE TABLE dbo.Department
   (  
      DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,
      DepartmentName varchar(50) NOT NULL,
      ManagerID int NULL,
      ParentDepartmentNumber char(10) NULL,
      SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
      SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
      PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
   )
WITH
   (
       MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA,
          SYSTEM_VERSIONING = ON ( HISTORY_TABLE = History.DepartmentHistory )
    );
```

A criação de uma tabela temporal vinculada a uma tabela de histórico existente é útil quando você deseja adicionar o controle da versão do sistema usando uma tabela existente, por exemplo, quando você deseja migrar uma solução temporal personalizada para suporte interno. No exemplo a seguir, uma nova tabela temporal é criada e vinculada a uma tabela de histórico existente.

```sql
--Existing table
CREATE TABLE Department_History
   (
      DepartmentNumber char(10) NOT NULL,
      DepartmentName varchar(50) NOT NULL,
      ManagerID int NULL,
      ParentDepartmentNumber char(10) NULL,
      SysStartTime datetime2 NOT NULL, SysEndTime datetime2 NOT NULL
   )
;
--Temporal table
CREATE TABLE Department
   (
      DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,
      DepartmentName varchar(50) NOT NULL,
      ManagerID INT NULL,
      ParentDepartmentNumber char(10) NULL,
      SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
      SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
      PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
   )
WITH
   (
      SYSTEM_VERSIONING = ON
         (  
            HISTORY_TABLE = dbo.Department_History
            , DATA_CONSISTENCY_CHECK = ON
         )  
      , MEMORY_OPTIMIZED = ON
      , DURABILITY = SCHEMA_AND_DATA
   )
;
```

## <a name="see"></a>Consulte

- [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Trabalhando com tabelas temporais com controle da versão do sistema e otimização de memória](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)
- [Monitorando tabelas temporais com controle da versão do sistema e otimização de memória](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)
- [Considerações sobre desempenho com tabelas temporais com controle de versão do sistema e otimização de memória](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)
- [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)
- [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Gerenciar a retenção de dados históricos em tabelas temporais com controle de versão do sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
